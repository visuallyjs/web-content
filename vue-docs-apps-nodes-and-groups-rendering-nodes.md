# Rendering Nodes

<!-- -->

<!-- -->

In VisuallyJs, you render your nodes using Vue components, which you map to node types via a set of [VueNodeMapping]() objects in `viewOptions` prop on a `SurfaceComponent`. You can map components like this:

## Mapping components[​](#mapping-components "Direct link to Mapping components")

```html
<script setup lang="ts">
import { DEFAULT } from "@visuallyjs/browser-ui"
import { SurfaceComponent } from "@visuallyjs/browser-ui-vue"
import MyNode from "./MyNode.vue"
import Type1Node from "./Type1Node.vue"

const viewOptions = {
  nodes: {
    [DEFAULT]: {
      component: MyNode
    },
    "type1": {
      component: Type1Node
    }
  }
}
</script>

<template>
  <SurfaceComponent :viewOptions="viewOptions"/>
</template>

```

Here, nodes of type `type1` are mapped to `Type1Node`. Any other node type is mapped to the "default" mapping, which uses `MyNode`.

## Creating a component[​](#creating-a-component "Direct link to Creating a component")

You do not need to use the default mappings; in fact a more modular approach is to define components separately and then map those. Every component used to render a node should be defined in its own file and use the `script setup` pattern. You can access the underlying model and node data by defining props using `VueWrapperProps`.

**MyNode.vue**

```html
<script setup lang="ts">
import { VueWrapperProps } from "@visuallyjs/browser-ui-vue"

const { model, obj } = defineProps<VueWrapperProps>()
</script>

<template>
  <div class="aNode">{{ obj.id }}</div>
</template>

```

For instance, this is the component for the mockup workflow node in the node/group overview page:

**IntroNode.vue**

```html
<script setup lang="ts">
import { VueWrapperProps } from "@visuallyjs/browser-ui-vue"

const { model, obj } = defineProps<VueWrapperProps>()
</script>

<template>
  <div class="workflow-node">
      <div class="node-header">
          <span class="node-type">TASK</span>
          <div class="node-status-dot"></div>
      </div>
      
      <div class="node-body">
          <div class="node-icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M12 2v20M2 12h20" />
              </svg>
          </div>
          <div class="node-label">
              {{ obj.label || "New Task" }}
          </div>
      </div>

      <div class="node-port"></div>
  </div>
</template>

```

and which we mapped like this:

```html
<script setup lang="ts">
import { DEFAULT } from "@visuallyjs/browser-ui"
import IntroNode from "./IntroNode.vue"

const viewOptions = {
  nodes: {
    [DEFAULT]: {
      component: IntroNode
    }
  }
}
</script>

```

You can encapsulate as much behaviour as you like inside the components you use to render your nodes.

## Accessing the context[​](#accessing-the-context "Direct link to Accessing the context")

You can access the underlying model, vertex and UI from inside your component via the `props`. This is an object of type `VueWrapperProps`

**ContextNode.vue**

```html
<script setup lang="ts">
import { VueWrapperProps } from "@visuallyjs/browser-ui-vue"

const { model, obj } = defineProps<VueWrapperProps>()

function countNodes() {
    alert(`There are ${model.getNodes().length} nodes in the dataset. My ID is ${obj.id}.`)
}
</script>

<template>
  <div>
      <button @click="countNodes">Click me</button>
  </div>
</template>

```

**********

The props passed in to your component are of type `VueWrapperProps`:

VueWrapperProps

The props that are passed in to a component used to render a node/group by a surface or paper component.

| Name   | Type               | Description                                       |
| ------ | ------------------ | ------------------------------------------------- |
| data   | [ObjectData]()     | Data that backs the object. Reactive.             |
| def    | any                | Definition for this node/group type               |
| el     | [BrowserElement]() | The underlying DOM element                        |
| model  | [BrowserUIModel]() | Underlying model.                                 |
| obj    | T                  | The vertex (node or group) that is being rendered |
| ui     | [BrowserUI]()      | Underlying UI                                     |
| vertex | T                  | The vertex (node or group) that is being rendered |

## Rendering content based on zoom[​](#rendering-content-based-on-zoom "Direct link to Rendering content based on zoom")

You might want to show more detail when zoomed in and less detail when zoomed out. VisuallyJs provides a `useZoom` composable to assist you with this.

```html
<script setup lang="ts">
import { useZoom } from '@visuallyjs/browser-ui-vue';
import { BrowserUI, Node } from '@visuallyjs/browser-ui';

const props = defineProps({
  vertex: Node,
  ui: BrowserUI
})

// 'zoom' is a reactive Ref<number>
const zoom = useZoom(props.ui)
</script>

<template>
  <div class="my-node">
    <!-- Show detailed view when zoomed in (zoom > 1) -->
    <section v-if="zoom > 1" class="detailed-view">
      <p>Detailed Information</p>
    </section>
    
    <!-- Show compact view when zoomed out -->
    <section v-else class="compact-view">
      <span>Compact View</span>
    </section>
  </div>
</template>

```

## Managing element size[​](#managing-element-size "Direct link to Managing element size")

The default behaviour of VisuallyJs is to render a <!-- -->node<!-- --> using whatever HTML is provided, and then after the element has been rendered, read back the size of the element from the DOM. For many types of applications this approach is really useful - you can draw whatever you like for your <!-- -->node<!-- -->s and VisuallyJs will figure out where any connected edges need to be placed, based on the size of the elements, which has been determined by their content and the CSS in your page.

In some applications, though, you'll want to give your users control over the size of <!-- -->node<!-- -->s, and VisuallyJs supports that too via the `useModelForSizes` rendering option.

### useModelForSizes[​](#usemodelforsizes "Direct link to useModelForSizes")

You can instruct VisuallyJs to extract `width` and `height` from your <!-- -->node<!-- --> data and to set the DOM element to these values, via the `useModelForSizes` flag:

```html
<script setup>

const renderOptions = {
  useModelForSizes: true
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

VisuallyJs will now set the width and height of rendered DOM elements from the `width` and `height` properties in their data. When either of those values are updated, VisuallyJs will update the size of the DOM element accordingly.

### Default size[​](#default-size "Direct link to Default size")

If a given <!-- -->node<!-- --> does not have width or height values in its data, VisuallyJs will use a default value, which you can specify in one of two places - either the `defaults` section of some render options:

```html
<script setup>

const renderOptions = {
  useModelForSizes: true,
  defaults: {
    nodeSize: {
      width: 150,
      height: 100
    }
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

<!-- -->

or inside a <!-- -->node<!-- --> definition in the view:

```html
<script setup>

import { DEFAULT } from "@visuallyjs/browser-ui"

const renderOptions = {
  useModelForSizes: true,
  defaults: {
    nodeSize: {
      width: 150,
      height: 100
    }
  }
}
function viewOptions() {
  return {
  nodes: {
    [DEFAULT]: {
      defaultSize: {
        width: 150,
        height: 100
      }
    },
    type1: {}
  }
}
    }

</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions"  :viewOptions="viewOptions()" />
</template>

```

<!-- -->

You can in fact provide values in both places - as shown above - and VisuallyJs will use the values from a <!-- -->node<!-- --> definition first. <!-- -->In the above example we see that `type1` has no default size set, so VisuallyJs will use `nodeSize` from the defaults block.<!-- -->

In the absence of any default values, VisuallyJs will <!-- -->render nodes with width 100 pixels and height 80 pixels<!-- -->.
