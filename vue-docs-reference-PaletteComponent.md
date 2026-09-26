# \<PaletteComponent/>

Provides a palette from which your users can select nodes or groups to add to a canvas. Two modes are supported - the default is to allow users to drag nodes or groups from the palette element onto a canvas using touch/pointer events; it is also possible to run the palette in `tap` mode, in which a user first selects a node/group in the palette by clicking it, and then subsequently clicks on the canvas where they would like to place a new object of that type.

## Usage[​](#usage "Direct link to Usage")

```html
<script>
import { defineComponent } from "vue"
  
export default defineComponent({
  name:"my-app",
  data:() => {
    return {
      data:{
        nodes:[ ],
        edges:[ ] 
      }
    }
  }
})
    
</script>
<template>
  <SurfaceComponent :data="data"/>
  <PaletteComponent>
    <div style="display:flex;flex-direction:column">
      <h1>Item Type 1</h1>
      <div data-vjs-type="type11">Type 1</div>
      <div data-vjs-type="groupType1" data-vjs-is-group="true">Group Type 1</div>
      <h1>Item Type 2</h1>
      <div data-vjs-type="type21">Type 1</div>
    </div>
  </PaletteComponent>
</template>


```

* This component will locate the surface to attach to automatically if you have only one `SurfaceComponent` in your app.
* The `data-vjs-type` attribute on the draggable elements tells VisuallyJs what type of data object each element represents.
* The `data-vjs-is-group="true"` attribute tells VisuallyJs that the item maps a Group, not a node

## Payloads[​](#payloads "Direct link to Payloads")

When a user adds a node/group to a canvas from a Palette, VisuallyJs will prepare an initial payload for the new object in one of two ways:

### Default extractor[​](#default-extractor "Direct link to Default extractor")

By default, any `data-vjs-***` attribute on the element in the Palette will have its value read and inserted into the payload. For instance, the attribute `data-vjs-label="hello"` will result in `{label:"hello"}`.

### Custom extractor[​](#custom-extractor "Direct link to Custom extractor")

If you provide a `dataGenerator`, you can control on a fine-grained level what the payload for new objects will be. This is a [DataGeneratorFunction]() whose type definition is:

`(el:BrowserElement) => ObjectData`

### Marking groups[​](#marking-groups "Direct link to Marking groups")

To inform VisuallyJs that a certain element represents a Group and not a Node, set `data-vjs-is-group="true"` on it:

```html
<div>
  <div data-vjs-type="foo">Foo NODE</div>
  <div data-vjs-type="bar" data-vjs-is-group="true">Bar GROUP</div>
</div>

```

## Props[​](#props "Direct link to Props")

PaletteComponentProps

Props for the `PaletteComponent`

| Name               | Type                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------ | ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowClickToAdd?   | boolean                               | When in draw mode, allow addition of new vertices simply by clicking, instead of requiring a shape be drawn. (When this is true, the drawing method also still works)                                                                                                                                                                                                                                                                                                                           |
| allowDropOnCanvas? | boolean                               | Whether or not to allow drop on whitespace in the canvas. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| allowDropOnEdge?   | boolean                               | Whether or not to allow drop on edge. Defaults to false.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| allowDropOnGroup?  | boolean                               | Whether or not to allow drop on existing vertices. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| allowDropOnNode?   | boolean                               | Defaults to false. Allows items to be dropped onto nodes in the canvas. If this is true and an element is dropped onto a node, the result is the same as if the element has been dropped onto whitespace. Note that when this is false and the user has dragged something over a node, the drag item is still not considered to be over the canvas, and releasing the mouse button at that time will not cause a new node to be added. Use `ignoreDropOnNode` if that's the behaviour you want. |
| allowRotation?     | boolean                               | Whether or not to allow rotation of elements being dragged. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| autoEdgeConnect?   | boolean \| [AutoEdgeConnectOptions]() | If true, the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements.                                                                                                                                                                                                                                                                          |
| canvasDropFilter?  | [CanvasDropFilter]()                  | Optional filter to test if objects may be dropped on the canvas.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| className?         | string                                | Optional extra css classes to set on the element                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| clickToAddOnly?    | boolean                               | This flag relates to "draw" mode, and defaults to false. When true, the palette only supports click to draw new vertices, not drag. This flag is forced to true if the associated UI does not have `useModelForSizes` set, since there is no point in allowing a user to drag a vertex to some size if its not going to be honoured. When you set this flag and associated UI does have `useModelForSizes` set, the palette will use default sizes for new nodes/groups.                        |
| dataGenerator?     | [DataGeneratorFunction]()             | Function to use to get a dataset for an item that is being dragged/has been tapped. If omitted, Visually JS will use a default data generator that extracts data values from any `data-vjs-***` attribute on the element being dragged.                                                                                                                                                                                                                                                         |
| dragSize?          | [Size]()                              | Optional size to use for elements dragged from the palette; used in drag mode only.                                                                                                                                                                                                                                                                                                                                                                                                             |
| groupIdentifier?   | [GroupIdentifierFunction]()           | Function to use to determine whether an item that is being dragged/has been tapped represents a group.                                                                                                                                                                                                                                                                                                                                                                                          |
| ignoreDropOnNode?  | boolean                               | Defaults to false. When true, the palette treats nodes as if they are part of the canvas - a user can drag new items on top of existing nodes and the new item will be added to the canvas. If you want to force your users to drop on canvas whitespace, don't set this. Note that this flag will force `allowDropOnNode` to `false`.                                                                                                                                                          |
| mode?              | PaletteMode                           | Mode to operate in - 'drag', 'tap' or 'draw'. Defaults to 'drag'.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| onVertexAdded?     | [OnVertexAddedCallback]()             | Optional callback that will be invoked after a new vertex has been dropped and added to the dataset.                                                                                                                                                                                                                                                                                                                                                                                            |
| rotationSpeed?     | number                                | The number of milliseconds required to complete a full rotation of an element when the trigger key is held down. Defaults to 2000.                                                                                                                                                                                                                                                                                                                                                              |
| selectAfterAdd?    | boolean                               | Defaults to false. When true, a newly added vertex is set as the model's current selection.                                                                                                                                                                                                                                                                                                                                                                                                     |
| selector?          | string                                | CSS 3 selector identifying what child elements of `container` are draggable/can be tapped. Optional. If omitted, a default of `[data-vjs-type]` will be used.                                                                                                                                                                                                                                                                                                                                   |
| showGroups?        | boolean                               | Whether or not to show groups in the palette. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| surface?           | [Surface]()                           | The surface to attach to. Optional: this component can derive a surface from a SurfaceProvider or SurfaceComponent. You'll only need this in certain advanced scenarios.                                                                                                                                                                                                                                                                                                                        |
| typeGenerator?     | [TypeGeneratorFunction]()             | Function to use to get the type of an item that is being dragged/has been tapped.                                                                                                                                                                                                                                                                                                                                                                                                               |
