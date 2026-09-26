# Colors

There are several parts of a chart that you can configure colors for:

* [Chart background](#chart-background)
* [Plot background](#plot-background)
* [Grid lines](#grid-lines)
* Chart data points/lines/areas
* Chart axes/labels

## Chart background[​](#chart-background "Direct link to Chart background")

You can set the background color of the chart using the `backgroundColor` property of a chart's `style`. It defaults to `#FFFFFF`. Alternatively, you can use the `.vjs-chart-background` CSS class to style the background.

```javascript
import { LineChart } from "@visuallyjs/browser-ui"

const data = [
    {x:1,id:"Value 1"},
     {x:2,id:"Value 2"},
     {x:3,id:"Value 3"}
]

const options = {
  style: {
    backgroundColor: "#f0f0f0"
  },
  series: [
    {
      valueField: "x"
    }
  ],
  data: data
}

new LineChart(document.querySelector("#app"), options)

```

## Plot background[​](#plot-background "Direct link to Plot background")

Most charts support the concept of the 'plot' area - the part of the chart where the data points are drawn. By default, the plot background will be the same color as the chart background, but you can set it independently in one of two ways: you can set the `plotBackgroundColor` property on a chart's `style`, or you can use the `.vjs-chart-plot-background` CSS class to style the background (but note using CSS means the color will not be set in an SVG export of the chart).

```javascript
import { LineChart } from "@visuallyjs/browser-ui"

const data = [
    {x:1,id:"Value 1"},
     {x:2,id:"Value 2"},
     {x:3,id:"Value 3"}
]

const options = {
  style: {
    plotBackgroundColor: "#f0f0f0"
  },
  series: [
    {
      valueField: "x"
    }
  ],
  data: data
}

new LineChart(document.querySelector("#app"), options)

```

## Grid lines[​](#grid-lines "Direct link to Grid lines")

Grid lines, in charts that use them, have a default color of `#AAAAAA`. This can be overridden by supplying a `gridLineColor` in the `style` option for a chart:

```javascript
import { LineChart } from "@visuallyjs/browser-ui"

const data = [
    {x:1,id:"Value 1"},
     {x:2,id:"Value 2"},
     {x:3,id:"Value 3"}
]

const options = {
  style: {
    gridLineColor: "#FF0000"
  },
  series: [
    {
      valueField: "x"
    }
  ],
  data: data
}

new LineChart(document.querySelector("#app"), options)

```

## Labels[​](#labels "Direct link to Labels")

The labels on each axis default to the system color for their text. You can change this by providing a `labelColor` config on the style config:

```javascript
import { LineChart } from "@visuallyjs/browser-ui"

const data = [
    {x:1,id:"Value 1"},
     {x:2,id:"Value 2"},
     {x:3,id:"Value 3"}
]

const options = {
  style: {
    labelColor: "#2233ee"
  },
  series: [
    {
      valueField: "x"
    }
  ],
  data: data
}

new LineChart(document.querySelector("#app"), options)

```

### Per-label color[​](#per-label-color "Direct link to Per-label color")

You can also provide a `labelColorGenerator` function, if you want to be able to specify custom colors per label. In this example we mark whole number values as red (and returning null for other values means the default is used, which you may have set via a `labelColor` config):

```javascript
import { LineChart } from "@visuallyjs/browser-ui"

const data = [
    {x:1,id:"Value 1"},
     {x:2,id:"Value 2"},
     {x:3,id:"Value 3"}
]

const options = {
  style: {},
  series: [
    {
      valueField: "x"
    }
  ],
  data: data
}

new LineChart(document.querySelector("#app"), options)

```

## Data points[​](#data-points "Direct link to Data points")

Different charts represent their data points in various ways.

### Default Data Color[​](#default-data-color "Direct link to Default Data Color")

The `defaultColor` property in `BaseChartOptions` allows you to set a single color that will be used for all data series in the chart. This property, if set, overrides any `colorGenerator` that might be present. Each of the 2D charts will honor this setting. Here's a bar chart with a default color, for example:

```javascript
import { BarChart } from "@visuallyjs/browser-ui"

const data = [
    {id:"A",value:10},
     {id:"B",value:20},
     {id:"C",value:15}
]

const options = {
  defaultColor: "royalblue",
  series: [
    {
      valueField: "value"
    }
  ],
  data: data
}

new BarChart(document.querySelector("#app"), options)

```

...and here's an area chart showing the default color:

```javascript
import { AreaChart } from "@visuallyjs/browser-ui"

const data = [
    {id:"A",value:10},
     {id:"B",value:20},
     {id:"C",value:15}
]

const options = {
  defaultColor: "royalblue",
  series: [
    {
      valueField: "value"
    }
  ],
  data: data
}

new AreaChart(document.querySelector("#app"), options)

```

## Color Generators[​](#color-generators "Direct link to Color Generators")

For charts with multiple series, or where you want more variety in colors, you can use a `ColorGenerator`. The `ColorGenerator` interface defines an object that can generate colors for a specific context.

```typescript
interface ColorGenerator {
    generate(ctx: any): string;
}

```

There are several concrete implementations of `ColorGenerator` available:

### StaticColorGenerator[​](#staticcolorgenerator "Direct link to StaticColorGenerator")

A `StaticColorGenerator` perpetually cycles through a given list of colors. This is useful when you have a specific palette you want to use.

```javascript
import { PieChart } from "@visuallyjs/browser-ui"

const data = [
    {label:"Red",value:300},
     {label:"Blue",value:50},
     {label:"Purple",value:100},
     {label:"Yellow",value:40}
]

const options = {
  colorGenerator: new StaticColorGenerator(['#ff6384', '#36a2eb', '#cc65fe', '#ffce56']),
  data: data
}

new PieChart(document.querySelector("#app"), options)

```

### RandomColorGenerator[​](#randomcolorgenerator "Direct link to RandomColorGenerator")

A `RandomColorGenerator` generates random colors within certain bounds. It attempts to ensure that it doesn't return colors that are too similar and keeps colors within the range (20, 245).

```javascript
import { BarChart } from "@visuallyjs/browser-ui"

const data = [
    {category:"A",value:10},
     {category:"B",value:20},
     {category:"C",value:15}
]

const options = {
  colorGenerator: new RandomColorGenerator(),
  data: data
}

new BarChart(document.querySelector("#app"), options)

```

tip

The same color is applied to each datapoint in a bar chart - if you want to confirm that the selected color was random, you'll have to reload this page!

### SingleColorGenerator[​](#singlecolorgenerator "Direct link to SingleColorGenerator")

A `SingleColorGenerator` always returns the same color. It's essentially a generator wrapper around a single color value.

```javascript
import { AreaChart } from "@visuallyjs/browser-ui"

const data = [
    {x:1,y:5},
     {x:2,y:10},
     {x:3,y:7}
]

const options = {
  colorGenerator: new SingleColorGenerator('seagreen'),
  series: [
    {
      valueField: "x"
    }
  ],
  categoryAxis: {
    labelField: "y"
  },
  data: data
}

new AreaChart(document.querySelector("#app"), options)

```
