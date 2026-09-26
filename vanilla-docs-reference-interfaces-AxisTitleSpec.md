AxisTitleSpec

Definition of the title for an axis

| Name       | Type                   | Description                                                                                                                                                                                               |
| ---------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| align?     | [AxisTitleAlignment]() | How to align the text - start, middle or end                                                                                                                                                              |
| fillRatio? | number                 | If the title is too wide for the chart, this defines the amount of the width of the chart that it should fill, before being wrapped. Ignored if you set titleWrap<!-- -->:false<!-- -->. Defaults to 0.9. |
| font?      | [FontSpec]()           | Spec for the font to use for the axis. Default size is 14px and style is 'normal'.                                                                                                                        |
| padding?   | number                 | How much blank space to leave after the title.                                                                                                                                                            |
| text?      | string                 | The text to display.                                                                                                                                                                                      |
| wrap?      | boolean                | If the title is too wide for the chart, this flag controls whether or not the title is wrapped. It defaults to true.                                                                                      |
