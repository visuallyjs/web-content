# ShapePalette

This is a palette that sources its draggable items from the SVG shapes that the surface it is attached to has available.

## Usage[​](#usage "Direct link to Usage")

You'll need to create an element in your markup that will host the shape palette:

```html
<!doctype html>
<html>
    <head>
        <link rel="stylesheet" href="node_modules/@visuallyjs/browser-ui/css/visuallyjs.css">
    </head>
    <body>
      <div id="myContainer"></div>
      <div id="shapePaletteContainer"></div>
    </body>
</html>

```

And you'll need to setup your Surface to be using a shape library:

```typescript
import {createSurface, FLOWCHART_SHAPES, ShapePalette} from "@visuallyjs/browser-ui"

const renderOptions = {
    shapes: {
        sets: [FLOWCHART_SHAPES]
    }
}

const surface = createSurface(document.getElementById("myContainer"), renderOptions)
const shapePalette = new ShapePalette({
    surface,
    container:document.getElementById("shapePaletteContainer")
})


```

## Options[​](#options "Direct link to Options")

ShapePaletteOptions

Options for a shape palette.

| Name                      | Type                                                                                         | Description                                                                                                                                                                                                                                                                                                                        |
| ------------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowClickToAdd?          | boolean                                                                                      | When in tap mode, allow addition of new vertices simply by clicking, instead of requiring a shape be drawn. (When this is true,<br />the drawing method also still works)                                                                                                                                                          |
| allowDropOnEdge?          | boolean \| CanDropOnEdgeFilter                                                               | If true, shapes can be dropped on edges in the canvas. The edge on which the shape was dropped has its target set to be the new node, and a new edge is added with the new node as source and the original edge's target as target.                                                                                                |
| allowRotation?            | boolean                                                                                      | Whether or not to allow rotation of elements being dragged. Defaults to true.                                                                                                                                                                                                                                                      |
| autoEdgeConnect?          | boolean \| [AutoEdgeConnectOptions]()                                                        | Controls whether the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements. You can set this to simply 'true', and use defaults, or you can provide values for various options. |
| autoExitDrawMode?         | boolean                                                                                      | Defaults to true: when in 'tap' mode and a new group/node has been drawn on the canvas, the UI is set back to pan mode.                                                                                                                                                                                                            |
| canDrop?                  | (candidate:[Node]() \| [Group](), target:[Node]() \| [Group](), onCanvas:boolean) => boolean | Optional function that is invoked at the start of a drag, and which identifies allowed drop targets. Each target - the canvas, nodes and groups - is passed in turn to this method; returning false indicates that the given target is not valid for that drag.                                                                    |
| connectToPortsOnEdgeDrop? | boolean                                                                                      | `<br/>If `allowDropOnEdge`is also true, this flag instructs the shape palette to provide a default`edgeDropHandler\` to the underlying palette which will attempt to find a source and target port on the new vertex, and connect to those instead of to the vertex itself. Defaults to true.                                      |
| container                 | HTMLElement                                                                                  | The element to draw the palette into.                                                                                                                                                                                                                                                                                              |
| dataGenerator?            | [DataGeneratorFunction]()                                                                    | Optional data generator to allow you to specify initial data for some element to be dragged. Note that you cannot override the object's `type` with this function. The palette will set the new object's type to match the type of the element that the user is dragging from the palette.                                         |
| dragSize?                 | [Size]()                                                                                     | Optional size to use for dragged elements.                                                                                                                                                                                                                                                                                         |
| fill?                     | string                                                                                       | Optional fill color to use for elements in the palette. This should be in RGB format, *not* a color like 'white' or 'cyan' etc. Defaults to "#FFFFFF".                                                                                                                                                                             |
| iconSize?                 | [Size]()                                                                                     | Optional size to use for icons. Defaults to 150x100 pixels. If you provide this but not `dragSize` this size will also be used for an icon that is being dragged.                                                                                                                                                                  |
| initialSet?               | string                                                                                       | Optional ID of the first set to show, hiding the others.                                                                                                                                                                                                                                                                           |
| inspector?                | boolean                                                                                      | When `true`, selecting an element in the canvas will cause its related shape to be selected in the palette. Defaults to true.                                                                                                                                                                                                      |
| mode?                     | PaletteMode                                                                                  | Mode to operate in - 'drag' or 'draw'. Defaults to 'drag' (PALETTE\_MODE\_DRAG).                                                                                                                                                                                                                                                   |
| onVertexAdded?            | [OnVertexAddedCallback]()                                                                    | Optional callback to invoke when a new vertex has been added                                                                                                                                                                                                                                                                       |
| outline?                  | string                                                                                       | Optional color to use for elements in the palette. Should be in RGB format. Defaults to "#000000".                                                                                                                                                                                                                                 |
| outlineWidth?             | number                                                                                       | Optional outline width (in pixels) to use for elements in the palette. Defaults to 2.                                                                                                                                                                                                                                              |
| paletteStrokeWidth?       | number                                                                                       | Stroke width to use for shapes in palette. Defaults to 1.                                                                                                                                                                                                                                                                          |
| preparedShapes?           | Array<[PreparedShape]()>                                                                     | Optional set of prepared shapes to show in the palette. When this is provided, the palette will only render these shapes, and not the contents of the shape library.                                                                                                                                                               |
| rotationSpeed?            | number                                                                                       | The number of milliseconds required to complete a full rotation of an element when the trigger key is held down. Defaults to 2000.                                                                                                                                                                                                 |
| selectAfterDrop?          | boolean                                                                                      | When true (which is the default), a newly dropped vertex will be set as the underlying model's selection.                                                                                                                                                                                                                          |
| shapeLibrary?             | ShapeLibrary\<T>                                                                             | The shape library to render. If you do not provide this the palette gets it from the UI it is attached to.                                                                                                                                                                                                                         |
| showAllMessage?           | string                                                                                       | Message to use for the 'show all' option in the shape set drop down when there is more than one set of shapes. Defaults to `Show all`.                                                                                                                                                                                             |
| showGroups?               | boolean                                                                                      | Whether or not to show groups in the palette. Defaults to true.                                                                                                                                                                                                                                                                    |
| showLabels?               | boolean                                                                                      | Optionally show each shape icon's label underneath it                                                                                                                                                                                                                                                                              |
| updateTypeOnPaletteTap?   | boolean                                                                                      | When `true`, clicking on an entry in the palette will change the type of any selected vertices to that type. Defaults to `false`. This is a potentially destructive operation if the properties of the new shape type are not compatible with the old one.                                                                         |
