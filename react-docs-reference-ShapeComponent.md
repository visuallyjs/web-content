# \<ShapeComponent/>

A component that renders an SVG shape from a `ShapeLibrary`. This component can be used inside your own React components if you've got a `ShapeLibrary` setup on your Surface - see the documentation for a discussion of this.

If you're building an SVG diagram in which the shapes are the entire node contents, you may want to look at the [DiagramComponent](/react/docs/reference/DiagramComponent.md).

## Usage[​](#usage "Direct link to Usage")

This component is used inside the JSX that represents some node (or group) in your app. For example, here we use one in the JSX in our view, which we pass in to a `SurfaceComponent`:

```jsx

export default function MyApp() {

    const view = {
        nodes: {
            default: {
                jsx: (ctx) => <div>
                    <strong>{ctx.obj.label}</strong>
                    <ShapeComponent ctx={ctx}/>
                </div>
            }
        }
    }

    return <SurfaceComponent viewOptions={view}/>
}  

```

`ctx` contains information about the vertex being rendered, and the Surface that is rendering it, etc. The vertex's `type` (and optionally `category`) values will be extracted and used to resolve an appropriate shape to draw from the ShapeLibrary the Surface is using.

## Supported Properties[​](#supported-properties "Direct link to Supported Properties")

An svg shape supports these properties:

* **type** Identifies the shape to be drawn. Required.
* **category** Identifies the shape set that the shape belongs to. Not required if you have only one shape set, but recommended.
* **fill** The color to use for the SVG's background - equivalent to the SVG attribute `fill`.
* **outline** The color to use for the outline of the shape - equivalent to the SVG attribute `stroke`.
* **outlineWidth** The `stroke-width` to use in the shape's outline.
* **label** Label to display for the shape.

An example payload might be:

```json
{
    "type": "process",
    "category": "flowchart",
    "fill":"#FFFFFF",
    "outline":"#000000",
    "outlineWidth":2,
    "label":"My Node" 
}

```

## Props[​](#props "Direct link to Props")

ShapeComponentProps

Props for a ShapeComponent

| Name              | Type                    | Description                                                                                       |
| ----------------- | ----------------------- | ------------------------------------------------------------------------------------------------- |
| ctx               | [JsxWrapperProps\<T>]() | Context for the vertex, as passed in by the SurfaceComponent.                                     |
| font?             | [FontSpec]()            | Optional font size/style to use for this shape.                                                   |
| labelColor?       | string                  | Color for the label. Defaults to #000000.                                                         |
| labelFillRatio?   | number                  | For multiline labels, the proportion of the width of the shape that the longest line can take up. |
| labelPosition?    | LabelPosition           | Defaults to "center". Use "top" or "bottom" to set the label above or below the shape.            |
| labelProperty?    | string                  | The name of the property that identifies some vertex's label. Defaults to "label".                |
| labelStrokeWidth? | string                  | Optional stroke width to use for labels. Defaults to "0.25px".                                    |
| multilineLabels?  | boolean                 | Defaults to true - word wrap shape labels so they fit into their shapes                           |
| showLabels?       | boolean                 | Defaults to false. If true, a label will be written on the shape (using an SVG text element).     |
