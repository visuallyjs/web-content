ChartExporterOptions

Options for a chart export menu.

| Name      | Type   | Description                                                                                                                                                                                                               |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| filename? | string | Optional filename to use when exporting this chart. If not provided, a filename (with maximum length 30 characters) will be created from the chart's title, if it has one. Otherwise `chart-export` will be the filename. |
| right?    | string | Placement respective to right edge of the chart. Any valid CSS dimension works. Default is 1rem.                                                                                                                          |
| top?      | string | Placement respective to top edge of the chart. Any valid CSS dimension works. Default is 1rem.                                                                                                                            |
