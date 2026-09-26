# Dragging shapes

By default, all shapes in a Diagram will be made draggable, and the default behaviour of a draggable element is that it can be dragged to anywhere on the canvas. No special treatment is needed for touch devices - VisuallyJs abstracts that away.

## Controlling drag[​](#controlling-drag "Direct link to Controlling drag")

There are a few approaches to controlling which shapes may be dragged.

### Readonly diagrams[​](#readonly-diagrams "Direct link to Readonly diagrams")

If you mark a Diagram as `editable:false`, no shapes will be draggable:

```html
<script setup>


const options = {
  editable: false
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

### Switching off drag[​](#switching-off-drag "Direct link to Switching off drag")

You can disable dragging for all shapes in an editable diagram like this:

```html
<script setup>


const options = {
  cells: {
    draggable: false
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

### Selective disable[​](#selective-disable "Direct link to Selective disable")

if you want more fine-grained control over which shapes should be draggable, you can provide a [DiagramActionMediator]() to the Diagram, and implement the `canDrag` method:

The `canDrag` method is invoked when the user begins to drag a shape. It is passed the underlying vertex that is being dragged, the definition for the shape representing that vertex, and the SVG element from the DOM. Return `false` from this method if you wish to prevent drag.

```typescript
canDrag:(vertex: Vertex, shape: Shape, el: HTMLElement) => {
    return vertex.type !== "lane"
}

```

## Dragging on a grid[​](#dragging-on-a-grid "Direct link to Dragging on a grid")

When you declare a grid in your diagram options, the shapes in the diagram will be dragged on that grid:

```html
<script setup>


const options = {
  grid: {
    size: {
      width: 50,
      height: 50
    }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

The full list of options supported by grid are defined in the [GridOptions]() interface:

GridOptions

Options for a grid in the UI

| Name             | Type     | Description                                                                                                                               |
| ---------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| fitGroupsToGrid? | boolean  | Whether or not to ensure calculated group sizes (from auto sized groups) are a multiple of the grid size in each axis. Defaults to false. |
| size?            | [Grid]() | Width/height of the grid cells                                                                                                            |
| snap?            | boolean  | Whether or not to snap elements to the grid when dragging. Defaults to false.                                                             |

## Magnetizing[​](#magnetizing "Direct link to Magnetizing")

VisuallyJs has a built in "magnetizer", which provides a means to nudge elements around in your UI so that things don't overlap. There are a few different ways to use the magnetizer, and it is covered in full [on this page](/vue/docs/diagrams/magnetizer.md). In the canvas below we're using the magnetizer in `constant` mode, so that as you drag a vertex the other vertices are moved aside. We've also switched on `trackback`, which causes vertices to try to move back to their original position wherever possible.

```html
<script setup>


const options = {
  shapes: [BASIC_SHAPES],
  cells: {
    magnetizer: {
      constant: true,
      trackback: true
    }
  }
}
const data = {
  nodes:[
    {id:"1",x:50,y:50},
     {id:"2",x:350,y:60},
     {id:"3",x:50,y:250}
  ]
}
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

**********

## Z Index[​](#z-index "Direct link to Z Index")

Since a diagram is a pure SVG UI you cannot use CSS to manage z-index for your shapes. When a user drags a shape, VisuallyJs automatically moves that shape so that it is the last child in the SVG, which results in it being painted on top the other shapes.

## Auto pan[​](#auto-pan "Direct link to Auto pan")

VisuallyJs will auto pan a canvas when a shape is dragged outside of the visible bounds. This can be controlled with the `autoPan` flag in your diagram options:

```html
<script setup>


const options = {
  autoPan: false
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

## Identifying drop targets[​](#identifying-drop-targets "Direct link to Identifying drop targets")

By default, an element can be dragged to any position on the canvas, and into any group. You can use the `canDrop` option of a mediator to restrict where an element can be dropped:

```javascript
dragOptions:{
  canDrop:(candidate, target, onCanvas) => {
    // return true if the candidate can be dropped on the target
  }
}

```

The arguments passed to `canDrop` are:

* **candidate** The node or group being dragged.
* **target** The node, group, or canvas that is a potential drop target.
* **onCanvas** A boolean indicating if the target is the canvas.

VisuallyJs calls this function for every possible drop target when a drag starts. If you return `false` for a given target, VisuallyJs will not allow the candidate to be dropped there.

## Drag groups[​](#drag-groups "Direct link to Drag groups")

A `DragGroup` models a group of vertices that should be dragged together. You can have any number of drag groups in your canvas. When you assign a vertex to a drag group you indicate to VisuallyJs whether that vertex should be an `active` member - meaning that when it is dragged all of the other vertices in the drag group are also dragged - or that it should be a `passive` member - meaning that when it is dragged no other members should be dragged, but that it should be dragged whenever an `active` member is dragged.

### Assigning drag groups[​](#assigning-drag-groups "Direct link to Assigning drag groups")

To assign vertices to drag groups you need to configure `dragGroups` in your diagram options:

```html
<script setup>
import { DragGroupsPlugin, BASIC_SHAPES } from "@visuallyjs/browser-ui"

const options = {
  shapes: [BASIC_SHAPES],
  dragGroups: {
    assignDragGroup: (v) => {
          return { id:'dragGroup', active:v.main === true }
        }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

The key piece to note is the `assignDragGroup` function that you provide. In the above example our `assignDragGroup` function instructs VisuallyJs to add every vertex to a group called `"dragGroup"`, but that the vertex should only be an `active` member if it has a `main` of attribute with value `true`.

Consider this dataset:

```javascript
{
  nodes:[
    {"id":"1","x":50,"y":50,"width":180,"height":100,"type":"rectangle","main":true,"fill":"forestgreen"},
    {"id":"2","x":250,"y":160,"width":50,"height":30,"fill":"orangered","type":"rectangle"},
    {"id":"3","x":350,"y":100,"width":50,"height":30,"fill":"orangered","type":"rectangle"},
]

```

We have one `"main"` shape and two other shapes. In the canvas below, try dragging the large green box around. You'll see the two red boxes drag along with it. Now try dragging one of the red boxes - nothing else moves. This is because all of the nodes are inside a drag group, but the large green node is marked `active` and the red nodes are marked `passive`, due to the `assignDragGroup` function shown above:

**********

The key is the `assignDragGroup` function that we provide. In the implementation above we do two things:

* all vertices are assigned to a drag group called `"dragGroup"`
* The vertex whose `main` is `true` is marked `active:true`; the others are marked `active:false`

### Multiple drag groups[​](#multiple-drag-groups "Direct link to Multiple drag groups")

Our example above just used a single drag group, but we can have as many of these as we want. For instance, here's a canvas in which all the red elements are dragged in a single group, and all the green elements are dragged in a different group:

**********

This was an even simpler setup - we just use each node's `fill` to specify its drag group:

```html
<script setup>
import { DragGroupsPlugin, BASIC_SHAPES } from "@visuallyjs/browser-ui"

const options = {
  shapes: [BASIC_SHAPES],
  dragGroups: {
    assignDragGroup: (v) => {
          return v.data.fill
        }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

Every element in this example is marked `active` because that's the default if you do not specify it. All we had to do in this example is return the name of a drag group and VisuallyJs adds the vertex as an active participant to that group.

Our dataset in this example is:

```javascript
{
  nodes:[
    {"id":"1","x":50,"y":50,"fill":"forestgreen","type":"rectangle"},
    {"id":"2","x":150,"y":160,"fill":"orangered","type":"rectangle"},
    {"id":"3","x":200,"y":30,"fill":"orangered","type":"rectangle"},
    {"id":"4","x":280,"y":150,"fill":"forestgreen","type":"rectangle"},
]

```

### Example - annotating objects[​](#example---annotating-objects "Direct link to Example - annotating objects")

A good example of how this functionality is useful is the concept of annotating objects in a diagram - explanatory notes for some given vertex that you want to place near the vertex, but whose positioning you want to adjust in each case to suit the diagram. When you drag a vertex that has annotations you want the annotations to move with the vertex, but you want to be able to position the annotations without moving the vertex itself.

Consider this dataset:

```javascript
{
  nodes:[
    {"id":"1","type":"rectangle","x":50,"y":50,"fill":"forestgreen"},
    {"id":"2","type":"rectangle","x":300,"y":50,"fill":"forestgreen"},
    {"id":"3","type":"rectangle","label":"I belong to node 1","ref":"1","x":70,"y":-40,"width":80,"height":40,"fontSize":11,"annotation":true},
    {"id":"4","type":"rectangle","label":"I belong to node 1","ref":"1","x":-90,"y":120,"width":80,"height":40,"fontSize":11,"annotation":true},
    {"id":"5","type":"rectangle","label":"I belong to node 2","ref":"2","x":380,"y":160,"width":80,"height":40,"fontSize":11,"annotation":true},
]

```

We've got five shapes, three of which are marked with `annotation:true`, each of which have a `ref` member, which points to another shape, by its id. We want to be able to drag our main nodes around and have the `annotation` nodes follow, but we also want to be able to position the `annotation` nodes around the `main` nodes where we please. This is easily achieved:

```html
<script setup>
import { DragGroupsPlugin } from "@visuallyjs/browser-ui"

const options = {
  dragGroups: {
    assignDragGroup: (v) => {
          return v.annotation == null ? v.id : {id:v.data.ref, active:false}
        }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

* For nodes of type `main`, we just return the node's id: `v.id`
* For nodes of type `annotation`, we return the `ref` as the drag group id, and mark the vertex passive: `{id:v.data.ref, active:false}`.

Which gives us this arrangement:

**********

And there you have it! Annotated objects using just a few lines of configuration.

#### Cleaning up annotations[​](#cleaning-up-annotations "Direct link to Cleaning up annotations")

One thing to keep in mind is that the annotations and the edges that connect them to their reference nodes will not automatically be removed by VisuallyJs if the reference node is removed from the dataset. To handle this we can use another of VisuallyJs's capabilities you won't find in other libraries in this space - [Transactions](/vue/docs/diagrams/model/undo-redo#transactions) - to cleanup the annotations, but in an undo/redo friendly way.

Try clicking one of the red circle buttons below. We'll remove the node the button belongs to, and we'll also remove any annotations that are attached to it (code follows below) :

**********

To remove a node and its annotations in an undo-friendly way, we find everything we want to delete and then perform all the removals inside a transaction. An example function, into which you'd pass the model and the ID of the node to cleanup, is:

```typescript
function removeNode(model:VisuallyJsModel, nodeId:string) {
    
    // find all annotation nodes that reference this node
    const annotations = model.getNodes().filter(n => n.data.ref === nodeId)

    // in a transaction, remove all the annotation nodes and then the focus node. Edges will be cleaned up automatically, and if the user clicks undo, the entire transaction is rolled back as one.
    model.transaction(() => {
      annotations.forEach(a => model.removeNode(a))
      model.removeNode(nodeId)
    })
}

```

<br />

```javascript
<script setup>
    import { Node, VisuallyJsModel } from '@visuallyjs/browser-ui'

    const props = defineProps({
        obj:Object as PropType<Node>,
        model:Object as PropType<VisuallyJsModel>
    })

    function removeNodeAndAnnotations() {
      const annotations = props.model.getNodes().filter(n => n.data.ref === props.obj.id)
      props.model.transaction(() => {
        annotations.forEach(a => props.model.removeNode(a))
        props.model.removeNode(props.obj.id)
      })
    }
</script>
<template>
    <div>
        <div data-vjs-delete="true" @click="removeNodeAndAnnotations()"></div>        
    </div>
</template>


```

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

There are a number of CSS classes assigned to various parts of the UI during a shape drag. These can be used to easily add visual cues for your users. Note, though, that since a diagram is a pure SVG UI, you cannot use CSS to control z-index during drag. See the discussion above for how VisuallyJs handles z-index in a diagram.

| Class                              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-drag-active`                  | Assigned to any element that is a candidate drop target for an edge that is being dragged                                                                                                                                                                                                                                                                                                                                                                                 |
| `vjs-drag-hover`                   | Assigned to any element that is the current drop target for an edge that is being dragged                                                                                                                                                                                                                                                                                                                                                                                 |
| `vjs-drag-hover-cannot-drop`       | Assigned to a vertex or the canvas when an element that is being dragged on the canvas is hovering over it but drop is not allowed.                                                                                                                                                                                                                                                                                                                                       |
| `vjs-drag-original-group`          | Assigned to a group element when one of its children is being dragged. This can be useful to help manage z-index: we recommend using this class to set a z-index for the drag parent group above that of the other groups, which will ensure that the element you are dragging will appear on top of other groups.                                                                                                                                                        |
| `vjs-element-dragging`             | Assigned by the Surface to a vertex element that is being dragged                                                                                                                                                                                                                                                                                                                                                                                                         |
| `vjs-group-child-element-dragging` | Assigned by the Surface to the group parent of a vertex element that is being dragged, if applicable. You can use this class for a couple of things - to show that a child element is being dragged, of course, but also a good idea is to use this class to bump the z-index for any group that has it assigned, to put that group above other groups. This ensures that as you drag a child vertex over to some other group, it appears on top of that group in the UI. |
| `vjs-most-recently-dragged`        | Assigned by the Surface to the vertex element(s) that was/were the most recently dragged elements.                                                                                                                                                                                                                                                                                                                                                                        |
| `vjs-surface-element-dragging`     | Assigned by the Surface to its container when a node or group is being dragged                                                                                                                                                                                                                                                                                                                                                                                            |
