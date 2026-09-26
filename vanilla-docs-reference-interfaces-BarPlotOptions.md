BarPlotOptions

Options for a bar/column chart plot

| Name        | Type                              | Description                                                                                                                                                                                               |
| ----------- | --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| barGap?     | number                            | The amount of space to leave between bars of the same category when there are multiple series.                                                                                                            |
| barSize?    | number                            | The width/height to use for bars representing values. If you provide this the chart will not check whether it results in any overlap. Defaults to null.                                                   |
| dataLabels? | [DataLabelsOptions]()             | Options for data labels. If true, the value for the bar is shown. If a string, it is used as a format string.                                                                                             |
| fillRatio?  | number                            | How much of the space available to each category to use for the bars in the chart. Defaults to 0.8. You should not set this to a value greater than 1.                                                    |
| maxBarSize? | number                            | The maximum size of a bar representing a value. Defaults to 50 pixels. This value applies to the category axis, NOT the value axis! In the value axis the size of the bar maps the value being displayed. |
| stacked?    | boolean \| "percent" \| "default" | Whether to stack series values on top of each other.                                                                                                                                                      |
| valueAxis?  | string                            | ID of the value axis to attach to. Defaults to `DEFAULT`.                                                                                                                                                 |
