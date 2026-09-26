# ShapePalette

HTML Tag

**vjs-shape-palette**

This is a palette that sources its draggable items from the SVG shapes that the surface it is attached to has available.

## Usage[​](#usage "Direct link to Usage")

```typescript
import { Component } from "@angular/core"
import {FLOWCHART_SHAPES, BASIC_SHAPES} from "@visuallyjs/browser-ui";

@Component({
   template:`<div>
   
  <vjs-surface [renderOptions]="renderOptions"/>
  <vjs-shape-palette/>
  
</div>` 
})
export class MyApp {
    renderOptions = {
        shapes:{
            sets:[ FLOWCHART_SHAPES, BASIC_SHAPES]
        }
    }
}  

```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name                    | Type                                  | Description                                                                                                                                                                                                                                                                                                                        |
| ----------------------- | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowDropOnEdge?        | boolean \| CanDropOnEdgeFilter        | Whether or not to allow drop on edge. Defaults to false.                                                                                                                                                                                                                                                                           |
| allowRotation?          | boolean                               | Whether or not to allow rotation of elements being dragged. Defaults to true.                                                                                                                                                                                                                                                      |
| autoEdgeConnect?        | boolean \| [AutoEdgeConnectOptions]() | Controls whether the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements. You can set this to simply 'true', and use defaults, or you can provide values for various options. |
| dataGenerator?          | [DataGeneratorFunction]()             | Optional function you can use to set some initial data for an element being dragged. Note that you cannot override the object's `type` with this function.                                                                                                                                                                         |
| dragSize                | [Size]()                              | Optional size to use for dragged elements.                                                                                                                                                                                                                                                                                         |
| fill?                   | string                                | Optional fill color to use for dragged elements. This should be in RGB or hex format, *not* a color like 'white' or 'cyan' etc.                                                                                                                                                                                                    |
| iconSize                | [Size]()                              | Optional size to use for icons.                                                                                                                                                                                                                                                                                                    |
| initialSet?             | string                                | When the shape library contains multiple sets, use this to instruct the palette that you want it to initially load just displaying this set. Optional.                                                                                                                                                                             |
| inspector?              | boolean                               | When `true`, selecting an element in the canvas will cause its related shape to be selected in the palette. Defaults to true.                                                                                                                                                                                                      |
| onVertexAdded?          | [OnVertexAddedCallback]()             | Callback to invoke when a vertex has been dropped on the canvas                                                                                                                                                                                                                                                                    |
| outline?                | string                                | Optional color to use for outline of dragged elements. Should be in RGB or hex format.                                                                                                                                                                                                                                             |
| paletteStrokeWidth?     | number                                | Stroke width to use in shapes in the palette. Defaults to 1.                                                                                                                                                                                                                                                                       |
| preparedShapes?         | Array<[PreparedShape]()>              | Optional set of prepared shapes to show in the palette. When this is provided, the palette will only render these shapes, and not the contents of the shape library.                                                                                                                                                               |
| rotationSpeed?          | number                                | The number of milliseconds required to complete a full rotation of an element when the trigger key is held down. Defaults to 2000.                                                                                                                                                                                                 |
| selectAfterDrop?        | boolean                               | When true (which is the default), a newly dropped vertex will be set as the underlying model's selection.                                                                                                                                                                                                                          |
| showAllMessage?         | string                                | Message to use for the 'show all' option in the shape set drop down when there is more than one set of shapes. Defaults to `Show all`.                                                                                                                                                                                             |
| showGroups?             | boolean                               | Whether or not to show groups in the palette. Defaults to true.                                                                                                                                                                                                                                                                    |
| updateTypeOnPaletteTap? | boolean                               | When `true`, clicking on an entry in the palette will change the type of any selected vertices to that type. Defaults to `false`. This is a potentially destructive operation if the properties of the new shape type are not compatible with the old one.                                                                         |
