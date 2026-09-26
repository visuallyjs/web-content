LineStyle

Defines the simple properties for an edge style.

| Name           | Type                     | Description                                                                                                  |
| -------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------ |
| color?         | string                   | Color to paint the edge's path                                                                               |
| dashArray?     | string                   | Definition of dash pattern to use to draw the edge path                                                      |
| fontFamily?    | string                   | Font size to use; defaults to whatever the browser decides given the context                                 |
| fontSize?      | number                   | Font size to use; defaults to whatever the browser decides given the context                                 |
| fontStyle?     | [FontStyle]()            | Font style to use; defaults to whatever the browser decides given the context                                |
| gradient?      | Array<\[number, string]> | An array of color stops to use as a linear gradient for the edge path. When this is set, `color` is ignored. |
| label?         | string                   | Label to show on the edge                                                                                    |
| labelLocation? | number                   | Location for the label, defaults to 0.5                                                                      |
| lineWidth?     | number                   | Width of the edge path                                                                                       |
| outlineColor?  | string                   | Color to paint the edge's outline path                                                                       |
| outlineWidth?  | number                   | Width to draw the edge's outline path                                                                        |
