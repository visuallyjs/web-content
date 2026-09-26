# Line Chart

Line charts connect a series of data points with a line, and are often used to represent changes over time, although that is not their only use - sometimes a line chart can be used in place of a bar or column chart because the fact they use less ink makes for a more appealing visual.

## Single series[​](#single-series "Direct link to Single series")

The simplest line chart consists of a single series:

```html
<script>
import {LineChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  title: {
    text: "Maximum Temperature",
    align: "left"
  },
  valueAxis: {
    title: {
      text: "Degrees celsius"
    }
  },
  legend: false,
  series: [
    {
      id: "max",
      valueField: "max",
      label: "Temperature"
    }
  ]
}
   
</script>
<template>
        <LineChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

### Inverting axes[​](#inverting-axes "Direct link to Inverting axes")

By default, the line chart will use the X axis as the category axis, and the Y axis as the value axis. This behaviour can be changed by specifying you want the chart to be `inverted`.

```html
<script>
import {LineChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  inverted: true
}
   
</script>
<template>
        <LineChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Displaying a range[​](#displaying-a-range "Direct link to Displaying a range")

You can display a range with a line chart - a separate line will be drawn for the minimum and maximum values:

The only difference in the setup for a range vs a single series is that we specify `minValueField` and `maxValueField` instead of just `valueField`:

```html
<script>
import {LineChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  title: {
    text: "Temperature Range"
  },
  valueAxis: {
    title: {
      text: "Degrees celsius"
    }
  },
  legend: false,
  series: [
    {
      maxValueField: "max",
      minValueField: "min",
      label: "Temperature"
    }
  ]
}
   
</script>
<template>
        <LineChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

### Inverting axes[​](#inverting-axes-1 "Direct link to Inverting axes")

As with a single series line chart, set `inverted` if you wish to invert the axes:

```html
<script>
import {LineChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  inverted: true
}
   
</script>
<template>
        <LineChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Specifying Marker[​](#specifying-marker "Direct link to Specifying Marker")

By default, line charts use circular markers for each data point. You can customize the marker's appearance using various options in the `ChartSeriesOptions`.

### Marker Type[​](#marker-type "Direct link to Marker Type")

You can change the shape of the marker using the `markerType` option. For example, to use a square marker:

```html
<script>
import {LineChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  series: [
    {
      valueField: "max",
      markerType: "square"
    }
  ]
}
   
</script>
<template>
        <LineChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

Valid options are `"circle"` (the default), `"square"` and `"cross"`.

### Marker Size[​](#marker-size "Direct link to Marker Size")

The size of the marker can be adjusted using the `markerSize` option, whose default value is 10. This is useful for making markers more prominent:

```html
<script>
import {LineChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  series: [
    {
      valueField: "max",
      markerSize: 20
    }
  ]
}
   
</script>
<template>
        <LineChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

### Custom Marker Template[​](#custom-marker-template "Direct link to Custom Marker Template")

For full control over the marker's appearance, you can provide an SVG template string using the `marker` option:

```html
<script>
import {LineChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  series: [
    {
      valueField: "max",
      marker: <svg:rect viewBox='0 0 30 30' width='30' height='10'/>
    }
  ]
}
   
</script>
<template>
        <LineChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

This template must be in VisuallyJs's template syntax.

## Assigning Colors[​](#assigning-colors "Direct link to Assigning Colors")

Colors can be managed in several ways depending on whether you want a uniform look, series-specific styling, or dynamic color generation.

### Chart Level[​](#chart-level "Direct link to Chart Level")

Setting a `defaultColor` at the chart level applies a base color to all series unless overridden. This is useful for maintaining brand consistency across simple charts.

```javascript
options: {
    defaultColor: '#3498db',
  // ...
}

```

### Series Level[​](#series-level "Direct link to Series Level")

For charts with multiple data series, you can assign specific colors to individual series to help distinguish between datasets.

```javascript
series: [
  {
    valueField: "corn",
    label: "Corn",
    color: "#f1c40f"
  },
  {
    valueField: "wheat",
    label: "Wheat",
    color: "#e67e22"
  }
]

```

### Color Generator[​](#color-generator "Direct link to Color Generator")

If you have a dynamic number of series or prefer an automated approach, you can provide a color generator (or an array of colors). The chart will then cycle through these colors for each new series or data point.

```javascript
options: {
  colors: ['#1abc9c', '#2ecc71', '#3498db', '#9b59b6'],
  // ...
}

```

### Background color[​](#background-color "Direct link to Background color")

You can set the background color of the chart using the `backgroundColor` property. It defaults to `#FFFFFF`. Alternatively, you can use the `.vjs-chart-background` CSS class to style the background.

```html
<script>
import {LineChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = [
    {x:1,id:"Value 1"},
     {x:2,id:"Value 2"},
     {x:3,id:"Value 3"}
]

const options = {
  backgroundColor: "#f0f0f0",
  title: "Background Color Example",
  series: [
    {
      valueField: "x"
    }
  ]
}
   
</script>
<template>
        <LineChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class            | Description                                   |
| ---------------- | --------------------------------------------- |
| `vjs-line-chart` | Set on the container element for a line chart |
