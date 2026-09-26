# \<ShapePalette/>

This is a palette that sources its draggable items from the SVG shapes that the surface it is attached to has available.

## Usage[​](#usage "Direct link to Usage")

This component will find the [SurfaceComponent](/vue/docs/reference/SurfaceComponent.md) to attach to if you have only one surface in your app. For complex applications with more than one surface, you can wrap everything inside a [SurfaceProvider](/vue/docs/reference/SurfaceProvider.md).

```html
<script>
import { defineComponent } from "vue"
import {FLOWCHART_SHAPES, BASIC_SHAPES} from "@visuallyjs/browser-ui";
  
export default defineComponent({
  name:"my-app",
  data:() => {
    return {
      renderOptions:{
        shapes:{
          sets:[FLOWCHART_SHAPES, BASIC_SHAPES]
        }
      }
    }
  }
})
    
</script>
<template>
    <SurfaceComponent :renderOptions="renderOptions"/>
    <ShapePalette/>
</template>


```

## Props[​](#props "Direct link to Props")

ShapePaletteComponentProps

Props for the ShapePaletteComponent

| Name                    | Type                                  | Description                                                                                                                                                                                                                                                     |
| ----------------------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowClickToAdd?        | boolean                               | When in tap mode, allow addition of new vertices simply by clicking, instead of requiring a shape be drawn. (When this is true, the drawing method also still works)                                                                                            |
| allowDropOnEdge?        | boolean                               | Whether or not to allow drop on edge. Defaults to false.                                                                                                                                                                                                        |
| allowRotation?          | boolean                               | Whether or not to allow rotation of elements being dragged. Defaults to true.                                                                                                                                                                                   |
| autoEdgeConnect?        | boolean \| [AutoEdgeConnectOptions]() | If true, the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements.                                          |
| dataGenerator?          | [DataGeneratorFunction]()             | Optional function you can use to set some initial data for an element being dragged. Note that you cannot override the object's `type` with this function.                                                                                                      |
| dragSize?               | [Size]()                              | Optional size to use for dragged elements.                                                                                                                                                                                                                      |
| fill?                   | string                                | Optional fill color to use for dragged elements. This should be in RGB format, *not* a color like 'white' or 'cyan' etc                                                                                                                                         |
| iconSize?               | [Size]()                              | Optional size to use for icons                                                                                                                                                                                                                                  |
| inspector?              | boolean                               | When `true`, selecting an element in the canvas will cause its related shape to be selected in the palette. Defaults to true.                                                                                                                                   |
| mode?                   | "tap" \| "drag"                       | Mode of operation, supported values are "tap" and "drag" - default is "drag".                                                                                                                                                                                   |
| onVertexAdded?          | [OnVertexAddedCallback]()             | Optional callback to invoke when a vertex has been dragged onto/dropped on the canvas                                                                                                                                                                           |
| outline?                | string                                | Optional color to use for outline of dragged elements. Should be in RGB format.                                                                                                                                                                                 |
| paletteStrokeWidth?     | number                                | Stroke width to use for shapes in palette. Defaults to 1.                                                                                                                                                                                                       |
| preparedShapes?         | Array<[PreparedShape]()>              | Optional set of prepared shapes to show in the palette. When this is provided, the palette will only render these shapes, and not the contents of the shape library.                                                                                            |
| rotationSpeed?          | number                                | The number of milliseconds required to complete a full rotation of an element when the trigger key is held down. Defaults to 2000.                                                                                                                              |
| selectAfterDrop?        | boolean                               | When true (which is the default), a newly dropped vertex will be set as the underlying model's selection.                                                                                                                                                       |
| showAllMessage?         | string                                | Message to use for the 'show all' option in the shape set drop down when there is more than one set of shapes. Defaults to `Show all`.                                                                                                                          |
| showGroups?             | boolean                               | Whether or not to show groups in the palette. Defaults to true.                                                                                                                                                                                                 |
| surfaceId?              | string                                | ID of the surface to attach to. This is optional; Visually JS will use the default surface ID if you do not provide this. For apps where there's only one surface there is no need to provide this.                                                             |
| updateTypeOnPaletteTap? | boolean                               | When `true`, clicking on an entry in the palette will change the type of any selected vertices to that type. Defaults to `false`.<br />This is a potentially destructive operation if the properties of the new shape type are not compatible with the old one. |
