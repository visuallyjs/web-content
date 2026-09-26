# Area Chart

Area charts are similar to line charts, but the area below the line is filled with color.

```html
<script setup>
    
const data = ... 

const options = {
  title: {
    text: "Corn & Wheat Production"
  },
  valueAxis: {
    title: {
      text: "1000 Metric Tons (MT)"
    }
  },
  series: [
    {
      valueField: "corn",
      label: "Corn",
      color: "rgb(223, 44, 184)"
    },
    {
      valueField: "wheat",
      label: "Wheat",
      color: "rgb(20, 119, 182)"
    }
  ]
}
   
</script>
<template>
        <AreaChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

### Inverting axes[​](#inverting-axes "Direct link to Inverting axes")

By default, the area chart will use the X axis as the category axis, and the Y axis as the value axis. This behaviour can be changed by specifying you want the chart to be `inverted`.

```html
<script setup>
    
const data = ... 

const options = {
  inverted: true
}
   
</script>
<template>
        <AreaChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Displaying a range[​](#displaying-a-range "Direct link to Displaying a range")

You can display a range with an area chart - the area between the minimum and maximum values will be filled:

The only difference in the setup for a range vs a single series is that we specify `minValueField` and `maxValueField` instead of just `valueField`:

```html
<script setup>
    
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
        <AreaChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

### Inverting axes[​](#inverting-axes-1 "Direct link to Inverting axes")

As with a single series area chart, set `inverted` if you wish to invert the axes:

```html
<script setup>
    
const data = ... 

const options = {
  inverted: true
}
   
</script>
<template>
        <AreaChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

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
<script setup>
    
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
        <AreaChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class                 | Description                                        |
| --------------------- | -------------------------------------------------- |
| `vjs-area-chart`      | Set on the container element for an area chart     |
| `vjs-area-chart-area` | Added to the painted area element of an Area chart |
