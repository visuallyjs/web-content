# CSS

VisuallyJs assigns a number of CSS classes to charts, to enable you to easily establish your own themes.

### Common chart classes[​](#common-chart-classes "Direct link to Common chart classes")

| Class                               | Description                                                                                                                        |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-area-chart`                    | Set on the container element for an area chart                                                                                     |
| `vjs-area-chart-area`               | Added to the painted area element of an Area chart                                                                                 |
| `vjs-bar-chart`                     | Added to the container element in a bar chart                                                                                      |
| `vjs-bar-chart-bar`                 | Added to each bar element in a bar chart                                                                                           |
| `vjs-bubble-chart`                  | Added to a bubble chart                                                                                                            |
| `vjs-bubble-chart-point`            | Added to each point in a bubble chart                                                                                              |
| `vjs-chart-axis`                    | Added to both the X and Y axes in an XY chart                                                                                      |
| `vjs-chart-axis-labels`             | Added to the parent container for the label elements in both the X and Y axes of an XY chart                                       |
| `vjs-chart-axis-line`               | Added to the baseline marking the X or Y axis in an XY chart                                                                       |
| `vjs-chart-axis-title`              | Added to the title element in both the X and Y axes of an XY chart                                                                 |
| `vjs-chart-background`              | Added to the background element of a chart.                                                                                        |
| `vjs-chart-body`                    | Added to the element that contains series data and crosshairs.                                                                     |
| `vjs-chart-crosshair`               | Added to the crosshairs element of a chart                                                                                         |
| `vjs-chart-crosshair-label`         | Added to the label of a value axis crosshair element                                                                               |
| `vjs-chart-empty`                   | Added to the "No data" message that is shown when a chart is empty.                                                                |
| `vjs-chart-gridline`                | Added to each gridline element in an XY chart                                                                                      |
| `vjs-chart-gridlines`               | Added to the parent SVG group of the gridlines in an XY chart                                                                      |
| `vjs-chart-legend`                  | Added to a chart's legend element                                                                                                  |
| `vjs-chart-legend-dot`              | Added to the dots for each item in a legend                                                                                        |
| `vjs-chart-legend-item`             | Added to an item in a chart's legend                                                                                               |
| `vjs-chart-legend-label`            | Added to the label in a chart's legend                                                                                             |
| `vjs-chart-plot-background`         | Added to element that is the parent of the chart's plot(s).                                                                        |
| `vjs-chart-point`                   | Added to each point in a scatter/bubble chart                                                                                      |
| `vjs-chart-point-hit-area`          | Added to the hit area elements that represent each data point. These are to assist users in selecting data points which are small. |
| `vjs-chart-axis-scale-label`        | Added to the labels of a value axis in an XY chart                                                                                 |
| `vjs-chart-series`                  | Added to an SVG group element that represents a data series in an XY chart.                                                        |
| `vjs-chart-subtitle`                | Added to the subtitle element of a chart                                                                                           |
| `vjs-chart-title`                   | Added to the title element of a chart                                                                                              |
| `vjs-chart-x-axis`                  | Added to the X axis element in an XY chart                                                                                         |
| `vjs-chart-x-axis-title`            | Added to the X axis title element in an XY chart                                                                                   |
| `vjs-chart-y-axis`                  | Added to the Y axis element in an XY chart                                                                                         |
| `vjs-chart-y-axis-title`            | Added to the Y axis title element in an XY chart                                                                                   |
| `vjs-column-chart`                  | Added to the container element of a column chart                                                                                   |
| `vjs-column-chart-column`           | Added to each column element in a column chart                                                                                     |
| `vjs-chart-crosshair-category-axis` | Added to the category axis crosshair elements of a chart                                                                           |
| `vjs-chart-crosshair-value-axis`    | Added to the value axis crosshair elements of a chart                                                                              |
| `vjs-line-chart`                    | Set on the container element for a line chart                                                                                      |
| `vjs-pie-chart`                     | CSS class set on a pie chart.                                                                                                      |
| `vjs-pie-slice`                     | CSS class set on a slice in a pie chart.                                                                                           |
| `vjs-pie-slice-selected`            | CSS class set on a selected slice in a pie chart.                                                                                  |
| `vjs-scatter-chart`                 | Added to a scatter chart                                                                                                           |
| `vjs-scatter-chart-point`           | Added to each point in a scatter chart                                                                                             |
| `vjs-tooltip`                       | Added to a chart tooltip's main element                                                                                            |

### Area Charts[​](#area-charts "Direct link to Area Charts")

| Class                 | Description                                        |
| --------------------- | -------------------------------------------------- |
| `vjs-area-chart`      | Set on the container element for an area chart     |
| `vjs-area-chart-area` | Added to the painted area element of an Area chart |

### Bar Charts[​](#bar-charts "Direct link to Bar Charts")

| Class               | Description                                   |
| ------------------- | --------------------------------------------- |
| `vjs-bar-chart`     | Added to the container element in a bar chart |
| `vjs-bar-chart-bar` | Added to each bar element in a bar chart      |

### Bubble Charts[​](#bubble-charts "Direct link to Bubble Charts")

| Class                      | Description                                                                                                                        |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-bubble-chart-point`   | Added to each point in a bubble chart                                                                                              |
| `vjs-chart-point`          | Added to each point in a scatter/bubble chart                                                                                      |
| `vjs-chart-point-hit-area` | Added to the hit area elements that represent each data point. These are to assist users in selecting data points which are small. |

### Column Charts[​](#column-charts "Direct link to Column Charts")

| Class                     | Description                                      |
| ------------------------- | ------------------------------------------------ |
| `vjs-column-chart`        | Added to the container element of a column chart |
| `vjs-column-chart-column` | Added to each column element in a column chart   |

### Gauge Charts[​](#gauge-charts "Direct link to Gauge Charts")

| Class                    | Description                                           |
| ------------------------ | ----------------------------------------------------- |
| `vjs-gauge-chart`        | Assigned to the container for a gauge chart           |
| `vjs-gauge-label`        | Assigned to each label element in a GaugeChart.       |
| `vjs-gauge-needle`       | Assigned to the needle element in a GaugeChart.       |
| `vjs-gauge-needle-pivot` | Assigned to the needle pivot element in a GaugeChart. |
| `vjs-gauge-tick`         | Assigned to each tick element in a GaugeChart.        |
| `vjs-gauge-track`        | Assigned to the track element in a GaugeChart.        |
| `vjs-gauge-zone`         | Assigned to each zone element in a GaugeChart.        |

### Line Charts[​](#line-charts "Direct link to Line Charts")

| Class            | Description                                   |
| ---------------- | --------------------------------------------- |
| `vjs-line-chart` | Set on the container element for a line chart |

### Pie Charts[​](#pie-charts "Direct link to Pie Charts")

| Class                    | Description                                       |
| ------------------------ | ------------------------------------------------- |
| `vjs-pie-chart`          | CSS class set on a pie chart.                     |
| `vjs-pie-slice`          | CSS class set on a slice in a pie chart.          |
| `vjs-pie-slice-selected` | CSS class set on a selected slice in a pie chart. |

### Sankey Charts[​](#sankey-charts "Direct link to Sankey Charts")

| Class                   | Description                                                                                                       |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `vjs-sankey`            | Assigned to the sankey chart container                                                                            |
| `vjs-sankey-edge`       | Assigned to edges in Sankey chart                                                                                 |
| `vjs-sankey-label`      | Assigned to labels in a sankey chart                                                                              |
| `vjs-sankey-node`       | Assigned to nodes in a sankey chart                                                                               |
| `vjs-sankey-selected`   | Assigned to edges/nodes in Sankey chart when the edge/node forms part of the selected path.                       |
| `vjs-sankey-unselected` | Assigned to edges/nodes in Sankey chart when something is selected but this edge/node is not in the selected path |

### Scatter Charts[​](#scatter-charts "Direct link to Scatter Charts")

| Class                      | Description                                                                                                                        |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-bubble-chart`         | Added to a bubble chart                                                                                                            |
| `vjs-chart-point`          | Added to each point in a scatter/bubble chart                                                                                      |
| `vjs-chart-point-hit-area` | Added to the hit area elements that represent each data point. These are to assist users in selecting data points which are small. |
| `vjs-scatter-chart`        | Added to a scatter chart                                                                                                           |
| `vjs-scatter-chart-point`  | Added to each point in a scatter chart                                                                                             |
