# Tooltips

Tooltips provide extra information about data points when a user hovers over them. They are supported in most chart types, including all `BaseXYChart` subclasses (Column, Bar, Line, Area etc.), `DualValueChart` subclasses (Scatter, Bubble), and Pie/Donut charts.

## Configuration[​](#configuration "Direct link to Configuration")

Tooltips are configured via the `tooltip` object in the chart options.

### Basic example[​](#basic-example "Direct link to Basic example")

The simplest tooltip configuration uses a format string:

```javascript
import { ColumnChart } from "@visuallyjs/browser-ui"

const data = ...

const options = {
  data: data,
  series: [
    {
      valueField: "value",
      label: "Quantity"
    }
  ],
  tooltip: {
    format: "{{category}}: {{point.value}}"
  }
}

new ColumnChart(document.querySelector("#app"), options)

```

## Format Template[​](#format-template "Direct link to Format Template")

The `format` string uses a simple templating syntax where variables are enclosed in double curly braces: `{{variable}}`.

### Context Variables[​](#context-variables "Direct link to Context Variables")

The following variables are available for use in the tooltip template:

* ##### category[​](#category "Direct link to category")

The category name of the data point (for XY charts).

* ##### series[​](#series "Direct link to series")

TooltipDataSeries

Definition of the `series` object passed to a Tooltip

{

<br />

  color:string,

<br />

  id:string,

<br />

  label:string,

<br />

  max:number,

<br />

  min:number,

<br />

  total:number

<br />

}

* ##### point[​](#point "Direct link to point")

TooltipDataPoint

Definition of the `point` object passed to a Tooltip. Not every chart type provides every field - see the individual chart docs for discussions.

{

<br />

  maxValue:string,

<br />

  minValue:string,

<br />

  rawMaxValue:number,

<br />

  rawMinValue:number,

<br />

  rawValue:number,

<br />

  stackTotal:number,

<br />

  value:string

<br />

}

### HTML support[​](#html-support "Direct link to HTML support")

Several HTML tags are supported in your format string to style the tooltip:

```javascript
tooltip: {
    format: "<b>{{category}}</b><br/>{{series.label}}: {{point.value}}"
}

```

* **b** Indicates the text inside of the element should be in bold face
* **strong** An alias for **b**
* **i** Indicates the text inside of the element should be italics
* **em** An alias for **i**
* **br** Inserts a line break. Ensure that you close this element - `<br/>`, not `<br>`.

## Customizing appearance[​](#customizing-appearance "Direct link to Customizing appearance")

### Font and Text Color[​](#font-and-text-color "Direct link to Font and Text Color")

You can customize the appearance of the tooltip's text using the `font` and `textColor` options.

* ##### font[​](#font "Direct link to font")

An optional object of type `FontSpec` that allows you to set the following properties:

FontSpec

Specs for a font. The default values depend on the context.

| Name    | Type           | Description                                                                                                    |
| ------- | -------------- | -------------------------------------------------------------------------------------------------------------- |
| family? | string         | Font family to use.                                                                                            |
| size?   | number         | Size of the font. Default value depends on the context this spec occurs in.                                    |
| style?  | [FontStyle]()  | Font style to use. Default value depends on the context this spec occurs in.                                   |
| weight? | [FontWeight]() | Font weight to use (e.g., "normal", "bold", "100", "300"). Defaults to null, which browsers treat as "normal". |

* ##### textColor[​](#textcolor "Direct link to textColor")

A string representing the color of the tooltip text (e.g., `"#FF0000"`, `"rgb(45,67,89)"`). Defaults to the system default. We recommend against the usage of named CSS colors - they can't be parsed and so effects like background highlights will fail.

### Background and Border[​](#background-and-border "Direct link to Background and Border")

The tooltip's background rectangle can be styled using the following properties:

* `fill`: The background color of the tooltip. Defaults to `"#FFFFFF"` (white).
* `outline`: The color of the tooltip's border. Defaults to `"#999999"`.
* `outlineWidth`: The width of the tooltip's border in pixels. Defaults to `1`.
* `cornerRadius`: The radius of the tooltip's corners. Defaults to `3` pixels.

## Additional options[​](#additional-options "Direct link to Additional options")

### valueSuffix[​](#valuesuffix "Direct link to valueSuffix")

A string to append to the end of any value displayed in the tooltip.

```javascript
tooltip: {
    format: "{{category}}: {{point.value}}",
    valueSuffix: " kg"
}

```

### shared[​](#shared "Direct link to shared")

When set to `true`, the tooltip will display information for all series at the same category index in a single tooltip (supported in some XY charts).

```javascript
tooltip: {
    shared: true
}

```
