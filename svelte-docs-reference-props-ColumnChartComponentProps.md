ColumnChartComponentProps

Props for the ColumnChartComponent

| Name              | Type                                | Description                                                                                                                              |
| ----------------- | ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| className?        | string                              | Optional class name to set on the chart component's container                                                                            |
| data?             | Array<[ObjectData]()>               | Optional data to load after the chart has been mounted.                                                                                  |
| dataSourceFilter? | [ChartModelFilter]()                | Optional filter to apply to the data source.                                                                                             |
| options           | Omit\<O,"data" \| "url" \| "model"> | Options for the chart                                                                                                                    |
| url?              | string                              | Optional url from which to load data after the component has been mounted. If you provide this and also data, this will take precedence. |
