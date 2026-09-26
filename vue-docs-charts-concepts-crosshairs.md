# Crosshairs

Crosshairs are lines that follow the mouse as it moves across an XY Chart. They can be attached to any value or category axis.

## Behavior by Axis Type[​](#behavior-by-axis-type "Direct link to Behavior by Axis Type")

The appearance of a crosshair depends on the type of axis it is attached to:

* **Category Axis**: On a category axis, the crosshair is represented by a rectangle that is as wide (on X) or as high (on Y) as the entire category. This helps highlight the specific category being hovered.
* **Value Axis**: On a value axis, the crosshair is a thin line (by default 1 pixel wide). It allows for precise tracking of values across the chart.

## Configuration Options[​](#configuration-options "Direct link to Configuration Options")

Crosshairs are configured using the `crosshair` property on an axis definition. You can set it to `true` to use default settings, or provide a `CrosshairOptions` object:

CrosshairOptions

Options for the crosshair display on an axis.

| Name              | Type                       | Description                                                                                                                                                                     |
| ----------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| color?            | string                     | Color of the crosshair line.                                                                                                                                                    |
| cssClass?         | string                     | Optional CSS class to write to the crosshair element.                                                                                                                           |
| labelColor?       | string                     | Color for the label text. Defaults to the same color as the line.                                                                                                               |
| labelFont?        | [FontSpec]()               | Font for the label.                                                                                                                                                             |
| labelFormat?      | string                     | Formatter for the label.                                                                                                                                                        |
| labelPosition?    | "end" \| "start"           | Position of the label on the crosshair. For a horizontal line, 'start' means 'left' and 'end' means 'right'. For a vertical line, 'start' means 'bottom' and 'end' means 'top'. |
| labelValueFormat? | number \| "float" \| "int" | Standard number format for the value (e.g. 'int', 'float', or a number for decimal places).                                                                                     |
| showLabel?        | boolean                    | Whether or not to show the current value on the crosshair. Defaults to true.                                                                                                    |
| width?            | number                     | Width of the crosshair line. Defaults to 1.                                                                                                                                     |

## Labelling on Value Axes[​](#labelling-on-value-axes "Direct link to Labelling on Value Axes")

When attached to a value axis, a crosshair can display the current value corresponding to the mouse position.

* **Automatic Positioning**: Labels are automatically positioned to remain within the chart area. If a label on a vertical crosshair would go outside the chart to the right, it is shifted to the left. For horizontal crosshairs, if it would go above the chart, it is shifted below.
* **Custom Formatting**: You can use the `labelFormat` option to customize how the value is displayed. This supports the same template engine as tooltips, allowing for rich text (e.g., `<b>{{value}}</b>`) and access to the `value` and `rawValue` variables.
* **Font Specification**: The `labelFont` property accepts a `FontSpec` object to control the size and style of the label text.
* **Start/End Positioning**: Use `labelPosition` to decide which end of the crosshair the label should appear on by default ('start' for bottom/left, 'end' for top/right).

#### Example[​](#example "Direct link to Example")

```html
<script setup>
    
const data = ... 

const options = {
  categoryAxis: {
    crosshair: true
  },
  valueAxis: {
    crosshair: {
      color: "red",
      width: 2,
      showLabel: true,
      labelPosition: "end",
      labelFormat: "Value: <b>{{value}}</b>"
    }
  }
}
   
</script>
<template>
        <LineChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```
