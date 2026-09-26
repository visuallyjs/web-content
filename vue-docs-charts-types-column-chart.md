# Column Chart

In a column chart, values are presented on the Y axis, and categories are presented on the X axis.

## Single series[​](#single-series "Direct link to Single series")

The simplest column chart consists of a single data series:

```html
<script setup>
    
const data = ... 

const options = {
  title: {
    text: "Fuel Types"
  },
  categoryAxis: {
    showLine: true,
    title: {
      text: "Fuel Type"
    }
  },
  valueAxis: {
    showLine: true,
    title: {
      text: "Number of vehicles"
    }
  },
  series: [
    {
      valueField: "value",
      label: "Type"
    }
  ],
  tooltip: {
    format: "{{category}}:{{point.value}}"
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Multiple series[​](#multiple-series "Direct link to Multiple series")

Multiple data series' are supported:

```html
<script setup>
    
const data = ... 

const options = {
  title: {
    text: "Corn vs wheat estimated production for 2023"
  },
  subtitle: {
    text: "Source: https://www.indexmundi.com/agriculture/?commodity=corn"
  },
  categoryAxis: {
    accessibility: {
      description: "Countries"
    },
    title: {
      text: "Country"
    }
  },
  valueAxis: {
    title: {
      text: "1000 metric tons (MT)"
    }
  },
  tooltip: {
    format: "<b>{{category}}</b><br/>{{series.label}}:{{point.value}}",
    valueSuffix: " (1000 MT)"
  },
  series: [
    {
      valueField: "corn",
      label: "Corn"
    },
    {
      valueField: "wheat",
      label: "Wheat"
    }
  ]
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Ranged data[​](#ranged-data "Direct link to Ranged data")

You can display data that contains a minimum and maximum value:

```html
<script setup>
    
const data = ... 

const options = {
  title: {
    text: "Temperature range",
    align: "right"
  },
  valueAxis: {
    title: {
      text: "Degrees Celsius"
    }
  },
  series: [
    {
      id: "max",
      maxValueField: "max",
      minValueField: "min",
      label: "Temperature"
    }
  ],
  legend: false,
  tooltip: {
    format: "<b>{{category}}</b><br/>{{point.minValue}} - {{point.maxValue}}",
    valueSuffix: " C"
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

Note how the chart options contain a `minValueField` and `maxValueField` specifier in the data series definition. The dataset used here looks like this:

```javascript
const data = [
    {id:"Jan", "min":-9.5, "max":8.0},
    {id:"Feb", "min":-7.8, "max":8.3}
]

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
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Stacking[​](#stacking "Direct link to Stacking")

The `stacked` option determines how different series within the same category are displayed relative to each other. It can take one of the following values:

* `false` (default): Series are displayed side-by-side within each category.
* `true` or `"default"`:
  <!-- -->
  Series are stacked on top of each other
  <!-- -->
  . The total
  <!-- -->
  height
  <!-- -->
  of the stack represents the sum of the values in that category.
* `"percent"`: Series are stacked such that they always fill 100% of the available space on the value axis. Each segment's size represents its proportional contribution to the total for that category.

As an example, this is the corn/wheat production chart from above, with the two crops stacked for each country:

```html
<script setup>
    
const data = ... 

const options = {
  title: {
    text: "Corn vs wheat estimated production for 2023"
  },
  subtitle: {
    text: "Source: https://www.indexmundi.com/agriculture/?commodity=corn"
  },
  stacked: true,
  series: [
    {
      valueField: "corn",
      label: "Corn"
    },
    {
      valueField: "wheat",
      label: "Wheat"
    }
  ]
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

### Percent stacking and the value axis[​](#percent-stacking-and-the-value-axis "Direct link to Percent stacking and the value axis")

When `stacked` is set to `"percent"`, the chart automatically adjusts the value axis to reflect percentage values:

* The value axis scale is set to range from 0 to 100.
* Internally, the chart sets the `labelSuffix` of the value axis to `%`. This ensures that labels on the axis (e.g., 0, 25, 50, 75, 100) are displayed with a percentage sign (0%, 25%, etc.).
* Note that if you have manually provided a `labelSuffix` or a `labelFormatter` in the axis definition, the automatic `%` suffix will not be applied.

## Grouping[​](#grouping "Direct link to Grouping")

The `grouped` option, combined with `groupField`, allows you to create more complex layouts where multiple stacks or bars are grouped side-by-side within a single category.

* `grouped: true`: Enables grouping.
* `groupField: string`: Specifies the field in your data objects that identifies which group/stack a record belongs to. Defaults to `"group"`.

This is particularly useful when you want to compare different sets of stacked data. Here we show the crop data chart again, with the figures grouped by the continent each country belongs to:

```html
<script setup>
    
const data = ... 

const options = {
  title: {
    text: "Corn vs wheat estimated production for 2023"
  },
  subtitle: {
    text: "Source: https://www.indexmundi.com/agriculture/?commodity=corn"
  },
  stacked: true,
  grouped: true,
  groupField: "continent",
  series: [
    {
      valueField: "corn",
      label: "Corn"
    },
    {
      valueField: "wheat",
      label: "Wheat"
    }
  ]
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Pivoting[​](#pivoting "Direct link to Pivoting")

The `pivot` flag is an option for `BarChart`, `ColumnChart`, and other category-value charts in Visually.js. It allows you to quickly change the perspective of your data visualization without needing to restructure your underlying data source.

When you enable `pivot: true`, the chart swaps the roles of **series** and **categories**:

* **Categories become Series**: Each data record (which originally represented a single category) is transformed into a new series.
* **Series become Categories**: The original series definitions (e.g., the different `valueField` entries) are transformed into the new categories on the category axis.

Consider the following dataset of fruit consumption by different people:

```javascript
const fruitData = [
    { id: "Apples", john: 10, jane: 15, joe: 7 },
    { id: "Oranges", john: 5, jane: 8, joe: 12 },
    { id: "Bananas", john: 12, jane: 6, joe: 9 }
];

```

#### Without Pivoting (Default):[​](#without-pivoting-default "Direct link to Without Pivoting (Default):")

```html
<script setup>
    
const data = [
    {id:"Apples",john:10,jane:15,joe:7},
     {id:"Oranges",john:5,jane:8,joe:12},
     {id:"Bananas",john:12,jane:6,joe:9}
] 

const options = {
  title: {
    text: "Fruit consumption"
  },
  series: [
    {
      valueField: "john",
      label: "John"
    },
    {
      valueField: "jane",
      label: "Jane"
    },
    {
      valueField: "joe",
      label: "Joe"
    }
  ]
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

When you don't specify a value for `pivot` the chart is organised in this way:

* **Categories**: Apples, Oranges, Bananas (each record is a category).
* **Series**: John, Jane, Joe (each `valueField` is a series).
* **Comparison**: You see how much fruit each person ate for a specific fruit (e.g., three columns for Apples).

#### With Pivoting:[​](#with-pivoting "Direct link to With Pivoting:")

```html
<script setup>
    
const data = [
    {id:"Apples",john:10,jane:15,joe:7},
     {id:"Oranges",john:5,jane:8,joe:12},
     {id:"Bananas",john:12,jane:6,joe:9}
] 

const options = {
  title: {
    text: "Fruit consumption"
  },
  pivot: true,
  series: [
    {
      valueField: "john",
      label: "John"
    },
    {
      valueField: "jane",
      label: "Jane"
    },
    {
      valueField: "joe",
      label: "Joe"
    }
  ]
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

With `pivot:true` set, the series and categories are swapped:

* **Categories**: John, Jane, Joe (the original series names become the categories).
* **Series**: Apples, Oranges, Bananas (each original record becomes a series).
* **Comparison**: You see the breakdown of fruit types for each person (e.g., three columns for John).

#### Notes[​](#notes "Direct link to Notes")

* The chart automatically generates new series and labels based on the pivoted structure.
* Pivoting is handled internally during the data loading phase, so it works seamlessly with both static data and data loaded via a URL.
* Legend labels will also reflect the pivoted structure, showing the original record identifiers as the new series.

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class                     | Description                                      |
| ------------------------- | ------------------------------------------------ |
| `vjs-column-chart`        | Added to the container element of a column chart |
| `vjs-column-chart-column` | Added to each column element in a column chart   |
