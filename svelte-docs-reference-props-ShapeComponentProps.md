ShapeComponentProps

| Name             | Type           | Description                                                                                                                                                                           |
| ---------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data             | [ObjectData]() | Backing data for the vertex. Required. This is passed in as a prop to a component used to render a node/group, so you can pass it straight through from the parent to this component. |
| font?            | [FontSpec]()   | Optional font size/style.                                                                                                                                                             |
| labelPosition?   | LabelPosition  | Defaults to "center". Use "top" or "bottom" to set the label above or below the shape.                                                                                                |
| labelProperty?   | string         | The name of the property containing each vertex's label. Defaults to `label`.                                                                                                         |
| labelStrokeWidth | string         | Stroke width to use on the text element rendering a label. Defaults to "0.25px".                                                                                                      |
| showLabels?      | boolean        | Whether or not to show labels on each shape. Defaults to false.                                                                                                                       |
