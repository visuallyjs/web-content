SankeyChartComponentProps

| Name         | Type                                               | Description                                                                                                                              |
| ------------ | -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| className?   | string                                             | Optional class name to set on the chart component's container                                                                            |
| csvData?     | string                                             | Optional data to load into the chart (in CSV format)                                                                                     |
| interactive? | boolean                                            | Whether the chart is interactive.                                                                                                        |
| jsonData?    | [VisuallyJsDefaultJSON]()                          | Optional data to load into the chart (in VisuallyJs default json format)                                                                 |
| options      | Omit<[SankeyOptions](),"data" \| "url" \| "model"> | Options for the chart                                                                                                                    |
| pivot?       | string                                             | Optional property to pivot the sankey chart on.                                                                                          |
| url?         | string                                             | Optional url from which to load data after the component has been mounted. If you provide this and also data, this will take precedence. |
