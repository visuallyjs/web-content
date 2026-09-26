# Axes

Most charts use two axes to display data - a vertical axis, or Y axis, and a horizontal axis, or X axis. Each axis can display:

* a title, positioned in the center of the axis or aligned to one end;
* labels, showing either values the axis is measuring, or the names of categories plotted on the axis;
* a marker line demarcating the axis from the plot area

All of these are optional.

In the chart above,

* "Millions of inhabitants" is the `title` for the y axis;
* The numbers 0 - 70 on the y axis are the y axis `labels`;
* 'UK' and 'Canada' are the x axis `labels`

Also, the chart has a [title and subtitle](/vue/docs/charts/concepts/title.md), and a [legend](/vue/docs/charts/concepts/legend.md). See the linked pages for a discussion of these.

## Axis Types[​](#axis-types "Direct link to Axis Types")

There are two types of axis:

* [Category Axis](#category-axis) This axis type contains the various categories in the dataset. In the chart above, we plotted the population of several countries, and the category axis contains the country names.
* [Value Axis](#value-axis) This axis type plots values from the dataset. In the chart above, the value axis contains the population figures. Note that in VisuallyJs, value axes are always **linear**, that is the values advance in a linear progression. Support for logarithmic and datetime axes is scheduled for an upcoming release.

Not every chart has both a category axis and a value axis - `Scatter` and `Bubble` charts, for instance, have two value axes, as they plot two values from the dataset. But `Column`, `Bar`, `Line` and `Area` charts have a category axis and a value axis.

## Specifying axes[​](#specifying-axes "Direct link to Specifying axes")

How you specify axes depends on the type of chart you're creating.

### CategoryValueCharts[​](#categoryvaluecharts "Direct link to CategoryValueCharts")

For this type of chart (`Column`, `Bar`, `Line` and `Area`), your chart options will contain a `categoryAxis` and a `valueAxis` definition:

```html
<script setup>
    
const data = ... 

const options = {
  categoryAxis: {
    title: {
      text: "Country"
    }
  },
  valueAxis: {
    title: {
      text: "Country"
    }
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

### DualValueCharts[​](#dualvaluecharts "Direct link to DualValueCharts")

For this type of chart (`Scatter`, `Bubble`), your chart options will contain an `xAxis` and a `yAxis` definition, each of which describes a value axis:

```html
<script setup>
    
const data = ... 

const options = {
  xAxis: {
    title: {
      text: "Age"
    },
    valueField: "age"
  },
  yAxis: {
    title: {
      text: "height"
    },
    valueField: "height"
  }
}
   
</script>
<template>
        <ScatterChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Axis Title[​](#axis-title "Direct link to Axis Title")

The title for an axis is specified by [AxisTitleSpec](). The simplest title contains just the text to display:

```javascript
title:{
    text:"Axis Title"
}

```

### Title alignment[​](#title-alignment "Direct link to Title alignment")

Axis titles are, by default, aligned to the middle of their axis. You can control this via the `align` option:

## Configuring an axis[​](#configuring-an-axis "Direct link to Configuring an axis")

### CategoryValueCharts[​](#categoryvaluecharts-1 "Direct link to CategoryValueCharts")

#### Category Axis[​](#category-axis "Direct link to Category Axis")

This is the axis containing the various categories in the dataset. In the example above of country populations, the category axis lists the countries in the dataset.

This is an optional config; VisuallyJs will use defaults if you do not provide a `categoryAxis` in your chart options.

```html
<script setup>
    
const data = ... 

const options = {
  categoryAxis: {
    title: {
      text: "Country"
    }
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

There are a number of configurable options on the category axis:

CategoryAxisDefinition

Definition of a category axis

| Name       | Type                            | Description                                                                                                                                                                                                                                                                                      |
| ---------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| crosshair? | boolean \| [CrosshairOptions]() | Whether to show a crosshair for this axis. If you supply 'true', defaults will be used. Otherwise you can supply options to customise the crosshair.                                                                                                                                             |
| font?      | [FontSpec]()                    | Spec for the font to use for all text on the axis. If you provide a `title` spec for this axis, any font settings in that spec will override these for the title.                                                                                                                                |
| id?        | string                          | Axis ID.                                                                                                                                                                                                                                                                                         |
| lineSize?  | number                          | The width of the baseline (if visible). Defaults to 2 pixels.                                                                                                                                                                                                                                    |
| position?  | AxisPosition                    | The position for the axis: for a Y axis, AXIS\_POSITION\_START means on the left (this is the default for a y axis), and AXIS\_POSITION\_END means on the right. For an X axis, AXIS\_POSITION\_START means on the top, and AXIS\_POSITION\_END means on the bottom (the default for an X axis). |
| showLine?  | boolean                         | Whether or not to show a solid line representing the axis' baseline. Defaults to false.                                                                                                                                                                                                          |
| title?     | [AxisTitleSpec]()               | Title for the axis. Defaults to empty.                                                                                                                                                                                                                                                           |

#### Value Axis[​](#value-axis "Direct link to Value Axis")

This axis contains the values from the dataset. In the example above of country populations, the value axis plots the population figures.

This is an optional config; VisuallyJs will use defaults if you do not provide a `valueAxis` in your chart options.

```html
<script setup>
    
const data = ... 

const options = {
  valueAxis: {
    title: {
      text: "Country"
    }
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

There are a number of configurable options on the value axis:

ValueAxisDefinition

A value axis displays a set of values. It may be in either the X or Y axis, depending on how the chart is setup. For example, in a bar chart, the value axis is on the X axis, and the category axis is on the Y axis, but for a column chart it's the other way around. Scatter and bubble charts have a value axis in both X and Y.

| Name            | Type                            | Description                                                                                                                                                                                                                                                                                                                     |
| --------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| crosshair?      | boolean \| [CrosshairOptions]() | Whether to show a crosshair for this axis. If you supply 'true', defaults will be used. Otherwise you can supply options to customise the crosshair.                                                                                                                                                                            |
| font?           | [FontSpec]()                    | Spec for the font to use for all text on the axis. If you provide a `title` spec for this axis, any font settings in that spec will override these for the title.                                                                                                                                                               |
| gridLineSize?   | number                          | Width of the grid lines. Defaults to 1 pixel.                                                                                                                                                                                                                                                                                   |
| id?             | string                          | Axis ID.                                                                                                                                                                                                                                                                                                                        |
| inverted?       | boolean                         | Whether or not to invert the axis. If true, the axis will run from max to min instead of min to max.                                                                                                                                                                                                                            |
| labelFormatter? | (value:number) => string        | Optional formatter for all value labels.                                                                                                                                                                                                                                                                                        |
| labelPrefix?    | string                          | Optional prefix for all value labels. Will be ignored if you provide a `labelFormatter`.                                                                                                                                                                                                                                        |
| labelSuffix?    | string                          | Optional suffix for all value labels. Will be ignored if you provide a `labelFormatter`.                                                                                                                                                                                                                                        |
| lineSize?       | number                          | The width of the baseline (if visible). Defaults to 2 pixels.                                                                                                                                                                                                                                                                   |
| max?            | number                          | Maximum value for the axis. Defaults to not set. If this is set and your dataset has values above this value their visual representation in bar/column charts will be truncated. If you have a chart with multiple value axes and one or more of them declares a `max`, the largest value for `max` will be used for all axes.  |
| min?            | number                          | Minimum value for the axis. Defaults to not set. If this is set and your dataset has values below this value their visual representation in bar/column charts will be truncated. If you have a chart with multiple value axes and one or more of them declares a `min`, the smallest value for `min` will be used for all axes. |
| position?       | AxisPosition                    | The position for the axis: for a Y axis, AXIS\_POSITION\_START means on the left (this is the default for a y axis), and AXIS\_POSITION\_END means on the right. For an X axis, AXIS\_POSITION\_START means on the top, and AXIS\_POSITION\_END means on the bottom (the default for an X axis).                                |
| showGrid?       | boolean                         | Whether or not to show grid lines for each value in the scale. Defaults to false.                                                                                                                                                                                                                                               |
| showLine?       | boolean                         | Whether or not to show a solid line representing the axis' baseline. Defaults to false.                                                                                                                                                                                                                                         |
| step?           | number                          | Optional fixed step size for the axis scale.                                                                                                                                                                                                                                                                                    |
| title?          | [AxisTitleSpec]()               | Title for the axis. Defaults to empty.                                                                                                                                                                                                                                                                                          |

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class                               | Description                                              |
| ----------------------------------- | -------------------------------------------------------- |
| `vjs-chart-crosshair`               | Added to the crosshairs element of a chart               |
| `vjs-chart-crosshair-label`         | Added to the label of a value axis crosshair element     |
| `vjs-chart-subtitle`                | Added to the subtitle element of a chart                 |
| `vjs-chart-title`                   | Added to the title element of a chart                    |
| `vjs-chart-crosshair-category-axis` | Added to the category axis crosshair elements of a chart |
| `vjs-chart-crosshair-value-axis`    | Added to the value axis crosshair elements of a chart    |
