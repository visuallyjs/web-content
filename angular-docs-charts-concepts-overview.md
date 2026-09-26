# Charts

VisuallyJs offers a number of different charts, many of which are what we refer to as a `CategoryValueChart` - the data is presented with an X and Y axis, where one axis notates the values in the dataset and the other notates the categories. Examples of `CategoryValueChart` include [BarChart](/angular/docs/charts/types/bar-chart.md), [ColumnChart](/angular/docs/charts/types/column-chart.md), [LineChart](/angular/docs/charts/types/line-chart.md) and [AreaChart](/angular/docs/charts/types/area-chart.md).

Another common type is a `DualValueChart`, in which both the X and Y axes plot a value from the dataset. Example of these include [ScatterChart](/angular/docs/charts/types/scatter-chart.md) and [BubbleChart](/angular/docs/charts/types/bubble-chart.md).

<!-- -->

Several other chart types are supported, including [Pie charts](/angular/docs/charts/types/pie-chart.md), [Sankey charts](/angular/docs/charts/types/sankey.md), and more.

### Title / Subtitle[​](#title--subtitle "Direct link to Title / Subtitle")

User-supplied text describing the chart. By default this appears at the top center of the chart, but can be relocated to any axis and left/right aligned. Can also be omitted. For more information see [Title and subtitle](/angular/docs/charts/concepts/title.md).

### Series[​](#series "Direct link to Series")

Every chart is a representation of one or more data series'. In the above example we show two data series. In VisuallyJs you can supply data series information directly to a chart, but you can also extract the series data by defining a filter on some model that is backing an app or diagram in your UI. This is a powerful mechanism that lets you easily construct sophisticated applications in which your charts respond dynamically to actions taken elsewhere in the UI.

For more information see [Series](/angular/docs/charts/concepts/title.md).

### Axes[​](#axes "Direct link to Axes")

Many charts use two axes to display data - a vertical axis, or Y axis, and a horizontal axis, or X axis. VisuallyJs offers a number of charts that use an X and Y axis to plot data. For more information about axes see [Axes](/angular/docs/charts/concepts/axes.md).

### Legend[​](#legend "Direct link to Legend")

Provides information to your users about the data that is displayed. Legends appear, by default, at the bottom center of the chart, but can be moved to any axis or positioned absolute, or omitted.

For more information see [Legend](/angular/docs/charts/concepts/legend.md).

### Tooltips[​](#tooltips "Direct link to Tooltips")

Several chart types support tooltips on hover - configurable popups containing a summary of a data point or data series.

For more information see [Tooltips](/angular/docs/charts/concepts/tooltips.md).

### Crosshairs[​](#crosshairs "Direct link to Crosshairs")

Crosshairs provide visual cues to a user for how the location of the pointer relates to the chart data. They're switched off by default but you can see them in the chart above.

For more information see [Crosshairs](/angular/docs/charts/concepts/crosshairs.md).
