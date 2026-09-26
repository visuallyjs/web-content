ShapeComponentProps

Props for the `ShapeComponent`.

| Name              | Type           | Description                                                                |
| ----------------- | -------------- | -------------------------------------------------------------------------- |
| labelColor?       | string         | Color for the label. Defaults to #000000.                                  |
| labelFillRatio?   | number         | When using a multiline label, defines the maximum width of any given line. |
| labelProperty?    | string         | Name of the property containing the object's label. Defaults to "label".   |
| labelStrokeWidth? | number         | Stroke width for the label text.                                           |
| multilineLabels?  | boolean        | Defaults to true - the label will be drawn across multiple lines.          |
| obj               | [ObjectData]() | Backing data for the vertex                                                |
| showLabels?       | boolean        | Whether or not to show labels Defaults to false.                           |
