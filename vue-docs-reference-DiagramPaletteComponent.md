# \<DiagramPaletteComponent/>

A shape palette for linking with a [DiagramComponent](/vue/docs/reference/DiagramComponent.md). This component will automatically display the shapes available to the Diagram it is attached to, allowing your users to drag them onto your Diagram, or to click to add.

## Usage[​](#usage "Direct link to Usage")

You need to declare a `DiagramProvider` as the parent of your `DiagramComponent` and `DiagramPalette`:

```html
<script>
  export default {
    data:() => {
        data:{ ... },
        options:{ ... }
    }
  } 
</script>
<template>
  <DiagramProvider>
    <DiagramComponent :options="options" :data="data"/>
    <DiagramPalette/>
  </DiagramProvider>
</template>


```

## Props[​](#props "Direct link to Props")

DiagramPaletteProps

| Name                    | Type                                  | Description                                                                                                                                                                                                                                                     |
| ----------------------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowClickToAdd?        | boolean                               | When in tap mode, allow addition of new vertices simply by clicking, instead of requiring a shape be drawn. (When this is true, the drawing method also still works)                                                                                            |
| allowDropOnEdge?        | boolean                               | Whether or not to allow drop on edge. Defaults to false.                                                                                                                                                                                                        |
| allowRotation?          | boolean                               | Whether or not to allow rotation of elements being dragged. Defaults to true.                                                                                                                                                                                   |
| autoEdgeConnect?        | boolean \| [AutoEdgeConnectOptions]() | If true, the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements.                                          |
| autoExitDrawMode?       | boolean                               | Defaults to true: when in 'tap' mode and a new group/node has been drawn on the canvas, the UI is set back to pan mode.                                                                                                                                         |
| className?              | string                                | Optional class name to set on the diagram palette root element.                                                                                                                                                                                                 |
| diagram?                | [Diagram]()                           | Optional diagram to attach to. In most cases it is better to use a DiagramProvider to provision the diagram to this component.                                                                                                                                  |
| dragSize?               | [Size]()                              | Optional size to use for dragged elements.                                                                                                                                                                                                                      |
| fill?                   | string                                | Optional fill color to use for new elements. This should be in RGB format, *not* a color like 'white' or 'cyan' etc.                                                                                                                                            |
| iconSize?               | [Size]()                              | Optional size to use for icons. Defaults to 150x100 pixels. If you provide this but not `dragSize` this size will also be used for an icon that is being dragged.                                                                                               |
| inspector?              | boolean                               | When `true`, selecting an element in the canvas will cause its related shape to be selected in the palette. Defaults to true.                                                                                                                                   |
| mode?                   | PaletteMode                           | Mode to operate in - 'drag' or 'tap'. Defaults to 'drag' (PALETTE\_MODE\_DRAG).                                                                                                                                                                                 |
| onCellAdded?            | (dc:[DiagramCell]()) => any           | Callback to invoke when a new diagram cell has been added.                                                                                                                                                                                                      |
| outline?                | string                                | Optional color to use for outline of dragged elements. Should be in RGB format.                                                                                                                                                                                 |
| paletteStrokeWidth?     | number                                | Stroke width to use for shapes in palette. Defaults to 1.                                                                                                                                                                                                       |
| preparedShapes?         | Array<[PreparedShape]()>              | Optional set of prepared shapes to show in the palette. When this is provided, the palette will only render these shapes, and not the contents of the shape library.                                                                                            |
| rotationSpeed?          | number                                | The number of milliseconds required to complete a full rotation of an element when the trigger key is held down. Defaults to 2000.                                                                                                                              |
| selectAfterAdd?         | boolean                               | When true (which is the default), a newly dropped shape will be set as the underlying model's selection.                                                                                                                                                        |
| showAllMessage?         | string                                | Message to use for the 'show all' option in the shape set drop down when there is more than one set of shapes. Defaults to `Show all`.                                                                                                                          |
| showGroups?             | boolean                               | Whether or not to show groups in the palette. Defaults to true.                                                                                                                                                                                                 |
| showLabels?             | boolean                               | Optionally show each shape icon's label underneath it                                                                                                                                                                                                           |
| updateTypeOnPaletteTap? | boolean                               | When `true`, clicking on an entry in the palette will change the type of any selected vertices to that type. Defaults to `false`.<br />This is a potentially destructive operation if the properties of the new shape type are not compatible with the old one. |
