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
