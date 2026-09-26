ChartTitleSpec

Definition of a title used in a chart.

| Name       | Type                    | Description                                                                                                                                                                                               |
| ---------- | ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| align?     | [ChartTitleAlignment]() | How to align the text - left, middle or right                                                                                                                                                             |
| fillRatio? | number                  | If the title is too wide for the chart, this defines the amount of the width of the chart that it should fill, before being wrapped. Ignored if you set titleWrap<!-- -->:false<!-- -->. Defaults to 0.9. |
| font?      | [FontSpec]()            | Specs for the font to use for the title. In the title, the default font size is 20px, and style is 'bold'                                                                                                 |
| padding?   | number                  | How much blank space to leave after the title.                                                                                                                                                            |
| placement? | [ChartTitlePlacement]() | Where to place the title - top or bottom. Defaults to top.                                                                                                                                                |
| text?      | string                  | The text to display.                                                                                                                                                                                      |
| wrap?      | boolean                 | If the title is too wide for the chart, this flag controls whether or not the title is wrapped. It defaults to true.                                                                                      |
