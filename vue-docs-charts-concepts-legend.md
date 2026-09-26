# Legend

The legend provides a visual key for the series displayed in the chart. By default, the legend is visible and automatically includes all series with a `label` defined.

## Visibility[​](#visibility "Direct link to Visibility")

Legends are shown by default. However, if a chart contains only a single series, the legend is hidden by default to save space. You can control this behavior using the `hide` and `hideForSingleSeries` properties.

* `hide`: Set to `true` to always hide the legend.
* `hideForSingleSeries`: Defaults to `true`. Set to `false` if you want to show the legend even when there is only one series.

## Positioning[​](#positioning "Direct link to Positioning")

The legend can be positioned relative to the chart area or at an absolute position within the chart container.

### Relative Positioning[​](#relative-positioning "Direct link to Relative Positioning")

Use the `valign` and `align` properties to position the legend relative to the chart.

* **Above**: Set `valign` to `"top"`.
* **Below**: Set `valign` to `"bottom"` (default).
* **Left/Right**: When `valign` is set to `"middle"`, the legend is positioned to the left or right of the chart area based on the `align` property (`"left"` or `"right"`).

### Absolute (Floating) Positioning[​](#absolute-floating-positioning "Direct link to Absolute (Floating) Positioning")

For more precise control, you can "float" the legend by setting `floating: true`. This allows you to position the legend anywhere within the chart container using `x` and `y` coordinates.

```javascript
legend: {
  floating: true,
  x: 100,
  y: 50
}

```

## Layout and Orientation[​](#layout-and-orientation "Direct link to Layout and Orientation")

The legend items can be arranged in a row or a column using the `orientation` property:

* **Row**: Set `orientation` to `"horizontal"`.
* **Column**: Set `orientation` to `"vertical"` (default).

## API Reference[​](#api-reference "Direct link to API Reference")

### LegendSpec[​](#legendspec "Direct link to LegendSpec")

The `legend` object in the chart options is of type [LegendSpec]() and supports the following properties:

LegendSpec

Options for a chart legend.

| Name                 | Type                          | Description                                                                                                                                                                                                  |
| -------------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| align?               | "center" \| "left" \| "right" | How to align the content of the legend. Defaults to center align.                                                                                                                                            |
| floating?            | boolean                       | Defaults to false, meaning the legend is positioned inline with the chart. When this is set to true, the legend can be floated anywhere in the chart (for which you need to provide values for `x` and `y`). |
| font?                | [FontSpec]()                  | Optional font specification for the legend.                                                                                                                                                                  |
| hide?                | boolean                       | Defaults to false. If true, the legend will not be shown.                                                                                                                                                    |
| hideForSingleSeries? | boolean                       | Defaults to true: when there is a single series in the chart, the legend is not drawn. Set this to false to override that behaviour.                                                                         |
| hover?               | boolean                       | Defaults to true - when user hovers over a series in the legend, the series is highlighted in the chart                                                                                                      |
| orientation?         | "horizontal" \| "vertical"    | Defaults to vertical. The orientation in which to align the items.                                                                                                                                           |
| padding?             | number                        | When not floating, padding to draw around the legend.                                                                                                                                                        |
| valign?              | "top" \| "bottom" \| "middle" | Where to position the legend vertically (when floating is false). Defaults to bottom; you can choose to place the legend at the top (underneath the title), or to the left/right of the chart area.          |
| x?                   | number                        | When floating is true, the X position of the legend.                                                                                                                                                         |
| y?                   | number                        | When floating is true, the Y position of the legend.                                                                                                                                                         |
