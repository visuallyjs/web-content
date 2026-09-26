# Rendering Nodes

<!-- -->

<!-- -->

In VisuallyJs, you render your nodes using Svelte components, which you map to node types via a set of [SvelteNodeMapping]() objects in `viewOptions` prop on a `SurfaceComponent`. You can map components like this:

## Mapping components[​](#mapping-components "Direct link to Mapping components")

```html
<script lang="ts">
  import { DEFAULT } from "@visuallyjs/browser-ui"
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import MyNode from "./MyNode.svelte"
  import Type1Node from "./Type1Node.svelte"

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

<SurfaceComponent {viewOptions}/>

```

Here, nodes of type `type1` are mapped to `Type1Node`. Any other node type is mapped to the "default" mapping, which uses `MyNode`.

## Creating a component[​](#creating-a-component "Direct link to Creating a component")

You do not need to use the default mappings; in fact a more modular approach is to define components separately and then map those. Every component used to render a node should be defined in its own file. You can access the underlying model and node data by using the `$props` rune with `SvelteWrapperProps`.

**MyNode.svelte**

```html
<script lang="ts">
  import type { SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte"

  let { model, vertex, data }: SvelteWrapperProps = $props();
</script>

<div class="aNode">{data.id}</div>

```

For instance, this is the component for the mockup workflow node in the node/group overview page:

**IntroNode.svelte**

```html
<script lang="ts">
  import type { SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte"

  let { model, vertex, data }: SvelteWrapperProps = $props();
</script>

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
            {data.label || "New Task"}
        </div>
    </div>

    <div class="node-port"></div>
</div>

```

and which we mapped like this:

```html
<script lang="ts">
  import { DEFAULT } from "@visuallyjs/browser-ui"
  import IntroNode from "./IntroNode.svelte"

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

You can access the underlying model, vertex and UI from inside your component via the `props`. This is an object of type `SvelteWrapperProps`

**ContextNode.svelte**

```html
<script lang="ts">
  import type { SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte"

  let { model, vertex, data }: SvelteWrapperProps = $props();

  function countNodes() {
    alert(`There are ${model.getNodes().length} nodes in the dataset. My ID is ${data.id}.`)
  }
</script>

<div>
    <button onclick={countNodes}>Click me</button>
</div>

```

**********

The props passed in to your component are of type `SvelteWrapperProps`:

SvelteWrapperProps

The props that are passed in to a component used to render a node/group by a surface component.

This interface has no members

## Rendering content based on zoom[​](#rendering-content-based-on-zoom "Direct link to Rendering content based on zoom")

You might want to show more detail when zoomed in and less detail when zoomed out. VisuallyJs provides a `useZoom` reactive state object to assist you with this.

```html
<script lang="ts">
    import type { SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte";
    import { useZoom } from "@visuallyjs/browser-ui-svelte";

    // Receive props from VisuallyJS
    let p = $props() as SvelteWrapperProps;
    let { ui } = p;

    // Create the reactive zoom state
    const zoom = useZoom(ui);
</script>

<div style="background-color:blue; width:100%; height:100%;">
    {#if zoom.current > 1}
        <p>This is the detailed description visible at high zoom levels.</p>
    {:else}
        <p>Small description</p>
    {/if}
</div>

```

## Managing element size[​](#managing-element-size "Direct link to Managing element size")

The default behaviour of VisuallyJs is to render a <!-- -->node<!-- --> using whatever HTML is provided, and then after the element has been rendered, read back the size of the element from the DOM. For many types of applications this approach is really useful - you can draw whatever you like for your <!-- -->node<!-- -->s and VisuallyJs will figure out where any connected edges need to be placed, based on the size of the elements, which has been determined by their content and the CSS in your page.

In some applications, though, you'll want to give your users control over the size of <!-- -->node<!-- -->s, and VisuallyJs supports that too via the `useModelForSizes` rendering option.

### useModelForSizes[​](#usemodelforsizes "Direct link to useModelForSizes")

You can instruct VisuallyJs to extract `width` and `height` from your <!-- -->node<!-- --> data and to set the DOM element to these values, via the `useModelForSizes` flag:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const renderOptions = {
  useModelForSizes: true
}
</script>

<SurfaceComponent {renderOptions}/>

```

VisuallyJs will now set the width and height of rendered DOM elements from the `width` and `height` properties in their data. When either of those values are updated, VisuallyJs will update the size of the DOM element accordingly.

### Default size[​](#default-size "Direct link to Default size")

If a given <!-- -->node<!-- --> does not have width or height values in its data, VisuallyJs will use a default value, which you can specify in one of two places - either the `defaults` section of some render options:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
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

<SurfaceComponent {renderOptions}/>

```

<!-- -->

or inside a <!-- -->node<!-- --> definition in the view:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
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
  const viewOptions = {
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
</script>

<SurfaceComponent {renderOptions} {viewOptions}/>

```

<!-- -->

You can in fact provide values in both places - as shown above - and VisuallyJs will use the values from a <!-- -->node<!-- --> definition first. <!-- -->In the above example we see that `type1` has no default size set, so VisuallyJs will use `nodeSize` from the defaults block.<!-- -->

In the absence of any default values, VisuallyJs will <!-- -->render nodes with width 100 pixels and height 80 pixels<!-- -->.
