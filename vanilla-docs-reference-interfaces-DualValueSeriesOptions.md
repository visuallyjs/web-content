DualValueSeriesOptions

Options for a dual value axis chart

| Name           | Type                            | Description                                                                                                                                              |
| -------------- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| color?         | string                          | Color to use for the series. This is optional and if not provided the chart will use a color from its installed ColorGenerator.                          |
| id?            | string                          | The id of the series.                                                                                                                                    |
| label?         | string                          | Label for the series. Optional.                                                                                                                          |
| marker?        | string                          | Optional template to use for markers. This should be a string in VisuallyJs's internal template format, with namespaced SVG elements.                    |
| markerSize?    | number                          | Size (in pixels) to use for data points. Defaults to 10 pixels. For circular markers this equates to the diameter; for square/cross this is width/height |
| markerType?    | "square" \| "circle" \| "cross" | Type of marker to draw. Defaults to "circle".                                                                                                            |
| outline?       | boolean                         | Whether or not to show an outline around the markers. Defaults to false.                                                                                 |
| outlineColor?  | string                          | Color for outline. If not provided, a contrasting color will be computed.                                                                                |
| outlineWidth?  | number                          | The width of the outline in pixels. Defaults to 1.                                                                                                       |
| resolveMarker? | [MarkerResolutionFunction]()    | Optional function to resolve a marker SVG string for each data point.                                                                                    |
| type?          | string                          | Defines the series type.                                                                                                                                 |
| xAxisField     | string                          | Name of the field from which to extract X axis data points                                                                                               |
| yAxisField     | string                          | Name of the field from which to extract Y axis data points                                                                                               |
