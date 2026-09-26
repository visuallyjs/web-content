BubbleChartComponentProps

BubbleChartComponent props

| Name              | Type                                                    | Description                                                                         |
| ----------------- | ------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| className?        | string                                                  | Optional class name to set on the chart's root element.                             |
| data?             | Array<[ObjectData]()>                                   | Data to load                                                                        |
| dataSourceFilter? | [ChartModelFilter]()                                    | Optional filter to apply to the chart's data source.                                |
| interactive?      | boolean                                                 | Whether the chart is interactive.                                                   |
| options           | Omit<[BubbleChartOptions](),"data" \| "url" \| "model"> | Options for the bubble chart.                                                       |
| reactive?         | boolean                                                 | Whether or not to respond to changes in the `url` or `data` prop. Defaults to true. |
| style?            | Record\<string,any>                                     | Optional style object                                                               |
| url?              | string                                                  | URL to load data from                                                               |
