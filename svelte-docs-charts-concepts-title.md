# Title and subtitle

Charts in VisuallyJs support both a `title` and `subtitle`, both of which are optional.

```html
<script>
import {ColumnChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  title: {
    text: "Population by year"
  },
  subtitle: {
    text: "Source: https://macrotrends.net"
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Alignment[​](#alignment "Direct link to Alignment")

By default, a chart title will be center aligned, as in the example above. You can control this via the `align` configuration:

```html
<script>
import {ColumnChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  title: {
    text: "Population by year",
    align: CHART_TITLE_ALIGN_LEFT
  },
  subtitle: {
    text: "Source: https://macrotrends.net",
    align: CHART_TITLE_ALIGN_LEFT
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Placement[​](#placement "Direct link to Placement")

By default, a chart title will appear at the top of the chart. You can control this via the `placement` configuration:

```html
<script>
import {ColumnChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  title: {
    text: "Population by year",
    placement: CHART_TITLE_PLACEMENT_BOTTOM
  },
  subtitle: {
    text: "Source: https://macrotrends.net",
    placement: CHART_TITLE_PLACEMENT_BOTTOM
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

## Wrapping[​](#wrapping "Direct link to Wrapping")

By default, a chart title will wrap if it is wider than the container the chart is displayed in.

```html
<script>
import {ColumnChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  title: {
    text: "This chart shows you the figures corresponding to the population of two countries, from the year 2010 through to the year 2012"
  },
  subtitle: {
    text: "Source: https://macrotrends.net"
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

### Fill ratio[​](#fill-ratio "Direct link to Fill ratio")

When wrapping is enabled, the maximum length of any line of text is computed according to the current `fillRatio`, which defaults to 0.9, meaning that by default a wrapped line will fill up to 90% of the available width. You can change this value:

```html
<script>
import {ColumnChartComponent} from "@visuallyjs/browser-ui-svelte"

const data = ...

const options = {
  title: {
    text: "This chart shows you the figures corresponding to the population of two countries, from the year 2010 through to the year 2012",
    fillRatio: 0.75
  },
  subtitle: {
    text: "Source: https://macrotrends.net"
  }
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

### No wrapping[​](#no-wrapping "Direct link to No wrapping")

Wrapping can be switched off:

```javascript
title:{
    text:"This chart shows you the figures corresponding to the population of two countries, from the year 2010 through to the year 2012",
    wrap:false
}

```
