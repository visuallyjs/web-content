ChartStyleOptions

Basic style options for a chart.

| Name                   | Type                             | Description                                                                                                                                                                                |
| ---------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| backgroundColor?       | string                           | Background color for chart. Defaults to #FFFFFF. You can also use the `.vjs-chart-background` css class to set this.                                                                       |
| crosshairColor?        | string                           | What color to draw crosshairs                                                                                                                                                              |
| gridLineColor?         | string                           | What color to draw gridlines. Defaults to #AAAAAA.                                                                                                                                         |
| labelColor?            | string                           | Color for labels, defaults to #000000. Can be overridden in axis definitions via the `labelColor` property.                                                                                |
| labelColorGenerator?   | (v:number, idx:number) => string | Optional function invoked to compute a custom color for a given label                                                                                                                      |
| legendBackgroundColor? | string                           | Background color for the legend.                                                                                                                                                           |
| legendOutlineColor?    | string                           | What color to draw as outline for the legend                                                                                                                                               |
| legendOutlineWidth?    | number                           | Width of the legend outline                                                                                                                                                                |
| plotBackgroundColor?   | string                           | Background color for chart's plot area. Defaults to being the same as the value calculated for `backgroundColor`. You can also use the `.vjs-chart-plot-background` css class to set this. |
