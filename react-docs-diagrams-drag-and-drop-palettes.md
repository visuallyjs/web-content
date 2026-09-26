# Palettes

With some types of diagrams, you'll want to provide your users with the ability to drag new shapes onto the canvas.

## Setup[​](#setup "Direct link to Setup")

To drag and drop SVG shapes, you can use a `DiagramPaletteComponent` - a palette that sources its draggable shapes from the underlying diagram's `ShapeLibrary`.

```jsx
import { useEffect, useRef} from 'react';
import { FLOWCHART_SHAPES } from "@visuallyjs/browser-ui"
import {  DiagramPaletteComponent, DiagramComponent, DiagramProvider } from "@visuallyjs/browser-ui-react"

export default function FlowchartComponent() {

    const options = {
        shapes:FLOWCHART_SHAPES
    }
    
    return <div>
            <DiagramProvider>
                <DiagramComponent options={options}/>
                <DiagramPaletteComponent className="node-palette"/>
            </DiagramProvider>
        </div>


```

The `DiagramPaletteComponent` is context aware and can locate the canvas to use from a `DiagramProvider`.

## Options[​](#options "Direct link to Options")

The full list of available props is:

DiagramPaletteComponentProps

Options for a palette for a diagram.

| Name                    | Type                                  | Description                                                                                                                                                                                                                                                                                                                        |
| ----------------------- | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowClickToAdd?        | boolean                               | When in tap mode, allow addition of new vertices simply by clicking, instead of requiring a shape be drawn. (When this is true, the drawing method also still works)                                                                                                                                                               |
| allowDropOnEdge?        | boolean \| CanDropOnEdgeFilter        | Whether or not to allow drop on edge. Defaults to false.                                                                                                                                                                                                                                                                           |
| autoEdgeConnect?        | boolean \| [AutoEdgeConnectOptions]() | Controls whether the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements. You can set this to simply 'true', and use defaults, or you can provide values for various options. |
| autoExitDrawMode?       | boolean                               | Defaults to true: when in 'tap' mode and a new group/node has been drawn on the canvas, the UI is set back to pan mode.                                                                                                                                                                                                            |
| className?              | string                                | Optional class name to set on the diagram palette root element.                                                                                                                                                                                                                                                                    |
| diagram?                | [Diagram]()                           | Optional diagram to attach to. In most cases it is better to use a DiagramProvider to provision the diagram to this component.                                                                                                                                                                                                     |
| dragSize?               | [Size]()                              | Optional size to use for dragged elements.                                                                                                                                                                                                                                                                                         |
| fill?                   | string                                | Optional fill color to use for dragged elements. This should be in RGB format, *not* a color like 'white' or 'cyan' etc.                                                                                                                                                                                                           |
| iconSize?               | [Size]()                              | Optional size to use for icons. Defaults to 150x100 pixels. If you provide this but not `dragSize` this size will also be used for an icon that is being dragged.                                                                                                                                                                  |
| inspector?              | boolean                               | When `true`, selecting an element in the canvas will cause its related shape to be selected in the palette. Defaults to true.                                                                                                                                                                                                      |
| mode?                   | PaletteMode                           | Mode to operate in - 'drag' or 'tap'. Defaults to 'drag' (PALETTE\_MODE\_DRAG).                                                                                                                                                                                                                                                    |
| onCellAdded?            | (dc:[DiagramCell]()) => any           | Callback to invoke when a new diagram cell has been added.                                                                                                                                                                                                                                                                         |
| onVertexAdded?          | [OnVertexAddedCallback]()             | Optional callback that will be invoked after a new vertex has been dropped and added to the dataset.                                                                                                                                                                                                                               |
| outline?                | string                                | Optional color to use for outline of dragged elements. Should be in RGB format.                                                                                                                                                                                                                                                    |
| paletteStrokeWidth?     | number                                | Stroke width to use for shapes in palette. Defaults to 1.                                                                                                                                                                                                                                                                          |
| preparedShapes?         | Array<[PreparedShape]()>              | Optional set of prepared shapes to show in the palette. When this is provided, the palette will only render these shapes, and not the contents of the shape library.                                                                                                                                                               |
| selectAfterAdd?         | boolean                               | When true (which is the default), a newly dropped shape will be set as the underlying model's selection.                                                                                                                                                                                                                           |
| showAllMessage?         | string                                | Message to use for the 'show all' option in the shape set drop down when there is more than one set of shapes. Defaults to `Show all`.                                                                                                                                                                                             |
| showGroups?             | boolean                               | Whether or not to show groups in the palette. Defaults to true.                                                                                                                                                                                                                                                                    |
| showLabels?             | boolean                               | Optionally show each shape icon's label underneath it                                                                                                                                                                                                                                                                              |
| style?                  | Record\<string,string>                | Optional style object to apply to the container element.                                                                                                                                                                                                                                                                           |
| updateTypeOnPaletteTap? | boolean                               | When `true`, clicking on an entry in the palette will change the type of any selected vertices to that type. Defaults to `false`. This is a potentially destructive operation if the properties of the new shape type are not compatible with the old one.                                                                         |

## Configuring appearance[​](#configuring-appearance "Direct link to Configuring appearance")

Shapes in a diagram use a set of common properties to determine their appearance - `fill`, `outline`, `color`, etc. Diagrams maintain an internal context which tracks the last set value for properties, so when you drag a shape out of a palette and onto the canvas, the diagram will populate the shape's data with the latest values, or with default values if nothing has yet been set.

Supported properties depend on the shape set in question, but all shape sets that VisuallyJs ships support these optional properties:

* `fill` - Color to fill the shape with. Defaults to `#FFFFFF`.
* `outline` - Color to outline the shape with. Defaults to `#000000`.
* `outlineWidth` - Width of the shape's outline. Defaults to 2px.
* `color` - Color to use for the shape's label (if shown). Defaults to `#000000`.

## Drawing vertices[​](#drawing-vertices "Direct link to Drawing vertices")

The diagram palette can be run in "draw" mode, which then gives your users the ability to draw new vertices with the mouse. Click on a shape in the palette below, and then you can draw it onto the canvas:

```jsx
<DiagramProvider>
  <DiagramPaletteComponent mode="draw"/>
  <DiagramComponent options={{ shapes:[FLOWCHART_SHAPES] }} data={{ ... }}/>
</DiagramProvider>

```

## Dropping on Edges[​](#dropping-on-edges "Direct link to Dropping on Edges")

You can instruct the palette to support dropping shapes onto edges, which will split the edge at the point the new shape was dropped - try it below. As you start dragging a shape, the edge will turn green (via some css - see below for details). When the shape intersects the edge path, the edge will turn red, indicating you can drop the shape at that point and the edge will split:

In the canvas above we implemented the drag/hover effect on the edge via these two CSS rules:

```css
.vjs-connector.vjs-palette-drag-active .vjs-connector-path {
  stroke:forestgreen;
}

.vjs-connector.vjs-palette-drag-hover .vjs-connector-path {
  stroke:red;
}

```

Whenever a shape is being dragged from a palette, the `vjs-palette-drag-active` CSS class is added to any possible drop targets. On hover, the CSS class `vjs-palette-drag-hover` is also added. The two selectors above target the active/hover states for an edge.

## Rotating shapes[​](#rotating-shapes "Direct link to Rotating shapes")

The `DiagramPalette` component automatically supports node rotation during drag - this is the same canvas as at the top of the page; try holding down the Meta (CMD on mac) key as you are dragging a shape from the palette and you will see it rotate:

### Rotation Stops[​](#rotation-stops "Direct link to Rotation Stops")

The palette will honor the rotation configuration for cells in your diagram, so if you configure your cells with a `rotateStops` value:

```typescript
const diagramOptions = {
    cells:{
        rotateStops:4
    }
}

```

Then the palette will also use that value when rotating - in this canvas, tap the Meta (CMD on mac) key to step through the rotation stops available:

## Auto edge connect[​](#auto-edge-connect "Direct link to Auto edge connect")

Since:

<!-- -->

1.2.5

Auto edge connect lets your users drag shapes from the palette and connect them to existing shapes as they are dragging, allowing for super fast authoring.

info

In this initial release, auto edge connect only works with shapes that declare their own `data-vjs-source` and/or `data-vjs-target` attributes. We invite feedback for how we can build on this functionality to support more use cases. For live examples of this functionality, take a look at the [Logic Gates](/demonstrations/logic-gates.md) or [Circuit Diagram](/demonstrations/circuit-diagram.md) demonstrations.

```jsx
import { useEffect, useRef} from 'react';
import { MY_SHAPES } from "somewhere"
import {  DiagramPaletteComponent, DiagramComponent, DiagramProvider } from "@visuallyjs/browser-ui-react"

export default function FlowchartComponent() {

    const options = {
        shapes: MY_SHAPES,
        autoEdgeConnect: {
            enabled:true,
            connectMode:"eager"
        }
    }

    return <div>
        <DiagramProvider>
            <DiagramComponent options={options}/>
            <DiagramPaletteComponent className="node-palette"/>
        </DiagramProvider>
    </div>
}

```

In this first example, we have specified that we want "eager" `connectMode`, which means that as soon as the user starts to drag, candidate source and target elements are highlighted, and the auto edge connect manager is active:

### Connect mode[​](#connect-mode "Direct link to Connect mode")

In a busy canvas your users might find that shapes are being connected to existing shapes when they did not want them to be. There are two solutions to this:

* Hold down Shift as you are dragging in `eager` mode. This temporarily disables the auto edge connect functionality (try it above!)
* Use the `onDemand` connect mode, in which the user must press Shift in order to activate the auto edge connect functionality. This is actually the default, and you can see it in the canvas below.

### Example shapes[​](#example-shapes "Direct link to Example shapes")

As mentioned above, to use this functionality your shapes must declare their own `data-vjs-source` and/or `data-vjs-target` attributes. For example, here's the template for the NOT gate from the logic gates shape set:

```html
<svg preserveAspectRatio="none" overflow="visible" viewBox="0 0 120 120" width="{{width}}" height="{{height}}">
  <path vector-effect="non-scaling-stroke" d="M 0 60 L 20 60 M 100 60 L 120 60" fill="none" stroke="#000000" stroke-width="2"/>
  <circle cx="0" cy="60" r="6" fill="transparent" stroke="none" data-vjs-anchor="0.5,0.5,-1,0" data-vjs-target="true" data-vjs-port="in1"/>
  <circle cx="120" cy="60" r="6" fill="transparent" stroke="none" data-vjs-anchor="0.5,0.5,1,0" data-vjs-source="true" data-vjs-port="out"/>
  <path vector-effect="non-scaling-stroke" d="M 20 0 L 80 60 L 20 120 Z" fill="#FFFFFF" stroke="#000000"/>
  <circle vector-effect="non-scaling-stroke" cx="90" cy="60" r="10" fill="none" stroke="#000000"/>
</svg>

```

This gate has one source port and one target port. Note also on this template the `data-vjs-anchor` attributes - these are a new feature in 1.2.5 also; they provide an efficient means for your template to define how they expect edges to travel out of each port. You can read more about anchor attributes in the [dragging edges documentation](/react/docs/diagrams/edges/dragging-edges.md).

## Prepared Shapes[​](#prepared-shapes "Direct link to Prepared Shapes")

Shape libraries give you a powerful mechanism for building diagrams, but at quite a low level - each shape needs to be individually configured with its fill, outline etc. Prepared shapes are a method you can use to define the shapes in your diagram at a slightly higher level.

The interface that defines a `PreparedShape` is as follows:

PreparedShape

Defines a wrapper around a shape with some `type` and `category` that adds properties (to be used to define the shape's appearance) and, optionally, the shape's initial size.

| Name       | Type           | Description                                                                             |
| ---------- | -------------- | --------------------------------------------------------------------------------------- |
| category   | string         | The shape set the underlying shape is sourced from                                      |
| label      | string         | Label to show for the prepared shape in a palette                                       |
| properties | [ObjectData]() | Properties with which to configure the shape when it is created.                        |
| shapeId    | string         | The ID for this prepared shape. Used internally, but ensure you provide a unique value. |
| size?      | [Size]()       | Optional initial size to use for the shape                                              |
| type       | string         | The type of the underlying shape                                                        |

#### Example[​](#example "Direct link to Example")

As a simple example, we'll define three prepared shapes:

```javascript
const preparedShapes = [{
    shapeId:"greenBox",
    type:"rectangle",
    category:"basic",
    properties:{
        fill:"#44ff44",
        outline:"#12F456"
    }
},
{
    shapeId:"redOctagon",
    type:"octagon",
    category:"basic",
    properties:{
        fill:"#FF3333",
        outline:"#F21456"
    }
},
{
    shapeId:"blueEllipse",
    type:"ellipse",
    category:"basic",
    properties:{
        fill:"#3333FF",
        outline:"#1214F6"
    }
}]

```

We tell the palette about them like this:

```jsx
<DiagramProvider>
  <DiagramPaletteComponent  preparedShapes={preparedShapes}/>
  <DiagramComponent options={{ shapes:[BASIC_SHAPES] }} data={{ ... }}/>
</DiagramProvider>

```

and this is the result - the palette shows only the prepared shapes that we gave it:

## CSS[​](#css "Direct link to CSS")

| Class                                  | Description                                                                                                                                                                                      |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `vjs-palette-auto-edge-connect-active` | Assigned to the UI's canvas when a drag has started and auto edge connect is active.                                                                                                             |
| `vjs-palette-current-shape-type`       | Assigned to a shape in a ShapePalette that matches the type of the model's currently selected shape.                                                                                             |
| `vjs-palette-drag-active`              | Assigned to possible drop targets when an element is being dragged from the Palette                                                                                                              |
| `vjs-palette-drag-hover`               | Assigned to a drop target when an element that is being dragged from the Palette is hovering over it.                                                                                            |
| `vjs-palette-drag-hover-cannot-drop`   | Assigned to a vertex or the canvas when an element that is being dragged from the palette is hovering over it but drop is not allowed.                                                           |
| `vjs-palette-current`                  | Assigned to an element when it is being dragged from a palette                                                                                                                                   |
| `vjs-palette-selected-element`         | Assigned to the currently selected element in a palette when in tap/draw mode.                                                                                                                   |
| `vjs-palette-tap-mode-active`          | Assigned to the surface canvas when a user has tapped an element in a palette in tap mode. this class can be used to show the user that a vertex can be dropped via click or drawn on the canvas |
