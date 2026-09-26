# Rendering Groups

Groups are declared inside a view alongside nodes and edges, and broadly follow the same syntax as node definitions - but there are a number of extra flags that can be set on a group definition.

In Vue, you render your groups using components that receive `VueWrapperProps` as props.

```html
<script setup lang="ts">
import { DEFAULT } from "@visuallyjs/browser-ui"
import { SurfaceComponent } from "@visuallyjs/browser-ui-vue"
import MyGroup from "./MyGroup.vue"

const viewOptions = {
  groups: {
    [DEFAULT]: {
      component: MyGroup
    }
  }
}
</script>

<template>
  <SurfaceComponent :viewOptions="viewOptions"/>
</template>

```

A typical group component looks like this:

**MyGroup.vue**

```html
<script setup lang="ts">
import { VueWrapperProps } from "@visuallyjs/browser-ui-vue"

const { model, obj } = defineProps<VueWrapperProps>()
</script>

<template>
  <div class="workflow-group">
      <div class="group-header">
          <span class="group-icon">📁</span>
          <span class="group-title">{{ obj.label || "Process Group" }}</span>
          <span class="vjs-toggle-group-collapse">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
                  <polyline points="18 15 12 9 6 15"></polyline>
              </svg>
          </span> 
      </div>

      <!-- The child nodes will be rendered inside this div -->
      <div class="group-content" data-vjs-group-content></div>

      <div class="group-footer">
          {{ obj.items?.length || 0 }} items
      </div>
  </div>
</template>

```

The component shown above is what we use for the example group on the node/group overview page, which - with a dash of CSS - looks like this:

**********

Try clicking the caret in the top right corner - the group collapses and expands. We discuss this [below](#collapse/expand).

## Specifying the canvas[​](#specifying-the-canvas "Direct link to Specifying the canvas")

It is not necessarily the case that you wish to use your entire group template as the parent of the group's members. To specify where in your group you want to host child nodes/groups, set a `data-vjs-group-content` attribute on an element - for instance, in the example above, we have this:

```html
<div class="group-content" data-vjs-group-content></div>

```

For complex group representations this is something you'll often want to use.

note

Whenever a group is resized by the [auto sizing code](#autosizing-groups) in the surface, the surface looks for an element in the group with this attribute, and if found, this is the element to which the surface applies the change of size. Otherwise the size is applied to the group's main element. Keep this in mind from a CSS perspective: your CSS should allow the size of the content area to mandate the size of its parent. Scroll/auto overflow is not supported inside a group element.

## Nested groups[​](#nested-groups "Direct link to Nested groups")

Groups may be nested to an arbitrary level:

**********

Depending on how your UI is configured (meaning how your CSS works to establish the size of the group elements in your UI), you may wish to switch on `autoSize` for your groups. In our example workflow group we set a `min-size` of `300px`, so we switched on `autoSize` (which is discussed [below](#autosizing-groups)) in order to get the parent group to expand:

```html
<script setup lang="ts">
import MyGroup from "./MyGroup.vue"

const viewOptions = { 
  groups:{
    default:{
      component: MyGroup,
      autoSize:true,
      padding:10
    }
  }
}
</script>

```

We also specified `padding:10` so that some space appears around the child group.

***

## Autosizing Groups[​](#autosizing-groups "Direct link to Autosizing Groups")

Groups can be configured to automatically resize themselves to encompass the extents of their child nodes/groups, via the `autoSize` flag on a group definition in a view:

```javascript
{
  groups:{
    "groupType1":{
      ...
      autoSize:true
      ...
    },
    "groupType2":{
      ...
      autoSize:true,
      maxSize:{width:600, height:600}
      ...
    }
  }
}

```

In this example, both group types are declared to auto size, but `groupType2` will grow to a maximum of 600 pixels in each axis.

Autosizing is run after a data load or when data exists in a model instance and it is rendered to some surface.

***

## Layouts[​](#layouts "Direct link to Layouts")

By default, every group has an [AbsoluteLayout]() assigned to it. If your node data has `left`/`top` properties in it, these values will automatically be used to place nodes/groups inside of their parent groups.

### Specifying in the view[​](#specifying-in-the-view "Direct link to Specifying in the view")

To specify the layout for a specific type of group, set it in that group's entry in your view:

```javascript
 {
    ...
    groups:{
      "someGroupType":{
        ...
        layout:{
            type:HierarchyLayout.type, 
            options:{
                orientation:"vertical"
            }
        }
      }
    }
 
    ...
 }

```

The format of the `layout` parameter is identical to the `layout` parameter in the root of the `view`.

#### Relationship to group size[​](#relationship-to-group-size "Direct link to Relationship to group size")

By default, a layout in a group will cause the auto size routine to be run for the group immediately afterwards.

***

## Collapse/Expand[​](#collapseexpand "Direct link to Collapse/Expand")

Groups can be collapsed and expanded. To add a control to your group to manage collapse/expand, you just need to add a CSS class of `.vjs-toggle-group-collapse` to some element.

```html
<span class="vjs-toggle-group-collapse">
  <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3">
    <polyline points="18 15 12 9 6 15"></polyline>
  </svg>
</span>

```

When you collapse a group, any edges from any of the member nodes/groups in the group to nodes/groups outside of the group are relocated to the group's container, and a CSS class is applied to the group's container, indicating the collapsed state. When you subsequently expand the group, the edges are placed back onto their appropriate nodes/groups.

It is important to note that when a group is collapsed, VisuallyJs does not hide the member nodes/groups automatically for you. But a CSS class of `vjs-group-collapsed` is added to the group's container, for you to handle this in your CSS.

The anchor to be used in the collapsed state can be specified in the group definition in the `viewOptions`:

```html
<script setup lang="ts">
import { AnchorLocations } from "@visuallyjs/browser-ui"
import MyGroup from "./MyGroup.vue"

const viewOptions = {
  groups:{
    "groupType1":{
      component: MyGroup,
      anchor:AnchorLocations.Continuous
    }
  } 
}
</script>

```

Any valid anchor can be used here.

### Collapsed Group Size[​](#collapsed-group-size "Direct link to Collapsed Group Size")

When you're using the model for your vertex sizes (ie. you're not relying on CSS to establish sizes), and a group is collapsed, the UI resolves the size to render it at by working through a chain of decision sources, from highest to lowest priority.

* `getGroupCollapsedSize`

An optional function `(group: Group, currentSize: Size) => Size` passed into the `renderOptions` of your `SurfaceComponent`. It is called first on every collapse. If it returns a non-null value, that value is used and the chain stops.

Return `null` or `undefined` to fall through to the next source. This is the right place for size logic that depends on runtime state or per-instance group data.

```html
<script setup>

const renderOptions = {
  getGroupCollapsedSize: (group, currentSize) => {
  return { width:200, height:60 }
}
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

* `collapsedSize`

A static `Size` value declared in the view definition for a group type. Used when `getGroupCollapsedSize` was not supplied or returned null. Applies uniformly to every group of that type.

```html
<script setup>

function viewOptions() {
  return {
  groups: {
    default: {
      collapsedSize: {
        width: 200,
        height: 60
      }
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

```

* `defaultCollapsedGroupSize`

A `Size` value passed when constructing the surface or UI instance. Acts as a global fallback for all groups when none of the above sources produce a value.

```html
<script setup>

const renderOptions = {
  defaultCollapsedGroupSize: {
    width: 200,
    height: 60
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

Lastly, if none of the previous sources returns a value, the built-in default of `{ width: 200, height: 150 }` is used.

Magnetizing when collapsed/expanded

By default, the surface widget will run the [Magnetizer](/vue/docs/apps/magnetizer.md) whenever a group is collapsed or expanded: when a group is expanded, surrounding elements are adjusted so as to ensure the group does not intersect with any other element. When a group is collapsed, the rest of the elements in the view are gathered in towards the collapsed group. This behaviour can be switched off - see the `afterGroupChange` flag in the [Surface widget magnetizer options](/vue/docs/apps/magnetizer.md#surface-widget)

***

## Elastic groups[​](#elastic-groups "Direct link to Elastic groups")

Elastic groups allow your users to dynamically resize a group by dragging its child elements around inside of it. To setup a group as elastic:

```javascript
{
    groups:{
        default:{
            elastic:true,
            minSize:{ width:250, height:250 }    // optional, but it does tend to help aesthetically to have a minSize.
        }
    }
}

```

Try dragging the node inside the group - you'll see the group displays a skeleton element showing how it would be resized to accommodate the node's new position. On mouseup the group is then resized:

**********

### Dragging elements out of an elastic group[​](#dragging-elements-out-of-an-elastic-group "Direct link to Dragging elements out of an elastic group")

To drag a child node out of an elastic group, hold down the Shift key prior to the drag.

### Suppressing resize[​](#suppressing-resize "Direct link to Suppressing resize")

Ordinarily, dragging a child vertex of an elastic group will cause the group to resize to fit its content. Holding the `shift` key can also be used to switch off elastic resize while an element is being dragged.

### Dragging the group and the node[​](#dragging-the-group-and-the-node "Direct link to Dragging the group and the node")

If you hold down the Meta key (Command on macs), you can drag child nodes/groups within their parent, and when the node reaches the bounds of the parent, the parent will relocate along with the child. It's easier to show this than explain it - try it on the canvas above.

### Nested elastic groups[​](#nested-elastic-groups "Direct link to Nested elastic groups")

Elastic groups which are themselves children of another elastic group will relay size changes during dragging to their parent, so that the user can see what changes will be made to all the groups.

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

## View options[​](#view-options "Direct link to View options")

The full list of options that are available on a group mapping is:

VueGroupMapping

Definition of a group in the view. If you provide a `component` here, VisuallyJs will use that component to render groups of the given type. Otherwise a default component will be used.

| Name                  | Type                                                             | Description                                                                                                                                                                                                                                                                                                                                                                                 |
| --------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| component?            | any                                                              | Component used to render this group type. If you do not supply this a default component will be used.                                                                                                                                                                                                                                                                                       |
| allowLoopback?        | boolean                                                          | Whether or not to allow edges from this vertex back to itself. Defaults to true. This flag will not prevent an edge from a port back to the node/group to which it belongs - for that, see `allowVertexLoopback`.                                                                                                                                                                           |
| allowVertexLoopback?  | boolean                                                          | Whether or not to allow edges from a port back to the vertex it belongs to. Defaults to true.                                                                                                                                                                                                                                                                                               |
| anchor?               | [AnchorSpec]()                                                   | Spec for the anchor to use for connections to children of the group when they are transferred to the group in its collapsed state.                                                                                                                                                                                                                                                          |
| anchorPositionFinder? | [AnchorPositionFinder\<any>]()                                   | Optional function to call on connection drop, to determine the location for the target anchor for the new connection. Returning null from this indicates no preference, and VisuallyJs will use its own computed value.                                                                                                                                                                     |
| anchorPositions?      | Array<[ObjectAnchorSpec]()>                                      | Optional array of anchor positions to use.                                                                                                                                                                                                                                                                                                                                                  |
| autoGrow?             | boolean                                                          | Defaults to false, meaning that the group will not be resized if an item addition/removal or drag causes the bounds of the child members to change and the new size is greater than the previous size.                                                                                                                                                                                      |
| autoShrink?           | boolean                                                          | False by default. If true indicates that if a child member is dragged/added/removed and the group's size is recalculated to be smaller than the previous size, the new size should be applied. This also works if the group needs to shrink from its left and/or top edge. If you don't want that behaviour, set `allowShrinkFromOrigin` to false.                                          |
| autoSize?             | boolean                                                          | False by default. This flag switches on both `autoShrink` and `autoGrow` and also enables support for shrinking a group from its left or top edge                                                                                                                                                                                                                                           |
| canDrop?              | (v:[Node]() \| [Group]()) => boolean                             | Optional interceptor that will be invoked to test whether a given node/group may be dropped onto this group.                                                                                                                                                                                                                                                                                |
| collapsedSize?        | [Size]()                                                         | The size to use for this group type when it is collapsed.                                                                                                                                                                                                                                                                                                                                   |
| constrain?            | boolean                                                          | False by default - nodes/groups may be dragged outside of the bounds of the group.                                                                                                                                                                                                                                                                                                          |
| defaultSize?          | [Size]()                                                         | Optional default size to use for the vertex. This is not used to set the size in the DOM for a vertex - it is used to insert `width` and `height` values into the backing data for any vertex of this type that does not have them set.                                                                                                                                                     |
| edgeType?             | string                                                           | Type to assign to edges connected to this vertex as a source.                                                                                                                                                                                                                                                                                                                               |
| elastic?              | boolean                                                          | Similar to autoGrow, but the UI shows a visual prompt when a group will be resized as a result of dragging a child.                                                                                                                                                                                                                                                                         |
| elementsDraggable?    | boolean                                                          | True by default - indicates that child members may be dragged around inside the group.                                                                                                                                                                                                                                                                                                      |
| events?               | [GroupEventOptions\<EL>]()                                       | Optional map of event bindings.                                                                                                                                                                                                                                                                                                                                                             |
| fitToGrid?            | boolean                                                          | When sizing the group, ensure it fits the underlying grid, if there is one.                                                                                                                                                                                                                                                                                                                 |
| ignore?               | boolean                                                          | If true, vertices of this type will be ignored by this UI and not rendered.                                                                                                                                                                                                                                                                                                                 |
| layout?               | {<br />  options:[LayoutParameters](),<br />  type:string<br />} | Options for the group's layout.                                                                                                                                                                                                                                                                                                                                                             |
| locked?               | boolean                                                          | Whether or not the group is locked.                                                                                                                                                                                                                                                                                                                                                         |
| maxConnections?       | number                                                           | Maximum number of connections this vertex supports. Default is 1. A value of -1 means no limit.                                                                                                                                                                                                                                                                                             |
| maxSize?              | [Size]()                                                         | Maximum size the group can grow to. If not specified the group can grow to an arbitrary size. Note that this behaviour can also be enforced via CSS.                                                                                                                                                                                                                                        |
| mergeStrategy?        | string                                                           | When merging a type description into its parent(s), values in the child for `connector`, `anchor` and `anchors` will always overwrite any such values in the parent. But other values, such as `overlays`, will be merged with their parent's entry for that key. You can force a child's type to override *every* corresponding value in its parent by setting `mergeStrategy:'override'`. |
| minSize?              | [Size]()                                                         | Minimum size the group can be.                                                                                                                                                                                                                                                                                                                                                              |
| padding?              | number                                                           | Optional padding to set inside a group when computing an auto size.                                                                                                                                                                                                                                                                                                                         |
| parent?               | string \| Array\<string>                                         | Optional ID of one or more edge definitions to include in this definition. The child definition is merged on top of the parent definition(s). Circular references are not allowed and will throw an error.                                                                                                                                                                                  |

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

## Managing element size[​](#managing-element-size "Direct link to Managing element size")

The default behaviour of VisuallyJs is to render a <!-- -->group<!-- --> using whatever HTML is provided, and then after the element has been rendered, read back the size of the element from the DOM. For many types of applications this approach is really useful - you can draw whatever you like for your <!-- -->group<!-- -->s and VisuallyJs will figure out where any connected edges need to be placed, based on the size of the elements, which has been determined by their content and the CSS in your page.

In some applications, though, you'll want to give your users control over the size of <!-- -->group<!-- -->s, and VisuallyJs supports that too via the `useModelForSizes` rendering option.

### useModelForSizes[​](#usemodelforsizes "Direct link to useModelForSizes")

You can instruct VisuallyJs to extract `width` and `height` from your <!-- -->group<!-- --> data and to set the DOM element to these values, via the `useModelForSizes` flag:

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

If a given <!-- -->group<!-- --> does not have width or height values in its data, VisuallyJs will use a default value, which you can specify in one of two places - either the `defaults` section of some render options:

<!-- -->

```html
<script setup>

const renderOptions = {
  useModelForSizes: true,
  defaults: {
    groupSize: {
      width: 300,
      height: 300
    }
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

or inside a <!-- -->group<!-- --> definition in the view:

<!-- -->

```html
<script setup>

import { DEFAULT } from "@visuallyjs/browser-ui"

const renderOptions = {
  useModelForSizes: true,
  defaults: {
    groupSize: {
      width: 300,
      height: 300
    }
  }
}
function viewOptions() {
  return {
  groups: {
    [DEFAULT]: {
      defaultSize: {
        width: 400,
        height: 400
      }
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions"  :viewOptions="viewOptions()" />
</template>

```

You can in fact provide values in both places - as shown above - and VisuallyJs will use the values from a <!-- -->group<!-- --> definition first. <!-- --><!-- -->In the example above, the default group definition does have a `defaultSize`, so that will be used for any groups that do not have width or height information in their backing data.

In the absence of any default values, VisuallyJs will <!-- -->render groups with a width and height of 300 pixels<!-- -->.
