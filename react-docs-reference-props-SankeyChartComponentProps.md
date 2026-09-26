SankeyChartComponentProps

SankeyChartComponent props

| Name              | Type                                               | Description                                                                         |
| ----------------- | -------------------------------------------------- | ----------------------------------------------------------------------------------- |
| className?        | string                                             | Optional class name to set on the chart's root element.                             |
| csvData?          | string                                             | Optional data to load into the chart (in CSV format)                                |
| dataSourceFilter? | [ChartModelFilter]()                               | Optional filter to apply to the chart's data source.                                |
| interactive?      | boolean                                            | Whether the chart is interactive.                                                   |
| jsonData?         | [VisuallyJsDefaultJSON]()                          | Optional data to load into the chart (in VisuallyJs default json format)            |
| options           | Omit<[SankeyOptions](),"data" \| "url" \| "model"> | Options for the sankey chart                                                        |
| pivot?            | string                                             | Optional property to pivot the sankey chart on.                                     |
| reactive?         | boolean                                            | Whether or not to respond to changes in the `url` or `data` prop. Defaults to true. |
| style?            | Record\<string,any>                                | Optional style object                                                               |
| url?              | string                                             | URL to load data from                                                               |
