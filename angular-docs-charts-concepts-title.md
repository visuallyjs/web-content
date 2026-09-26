# Title and subtitle

Charts in VisuallyJs support both a `title` and `subtitle`, both of which are optional.

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-column-chart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  title: {
    text: "Population by year"
  },
  subtitle: {
    text: "Source: https://macrotrends.net"
  }
}   
}

```

## Alignment[​](#alignment "Direct link to Alignment")

By default, a chart title will be center aligned, as in the example above. You can control this via the `align` configuration:

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-column-chart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  title: {
    text: "Population by year",
    align: CHART_TITLE_ALIGN_LEFT
  },
  subtitle: {
    text: "Source: https://macrotrends.net",
    align: CHART_TITLE_ALIGN_LEFT
  }
}   
}

```

## Placement[​](#placement "Direct link to Placement")

By default, a chart title will appear at the top of the chart. You can control this via the `placement` configuration:

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-column-chart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  title: {
    text: "Population by year",
    placement: CHART_TITLE_PLACEMENT_BOTTOM
  },
  subtitle: {
    text: "Source: https://macrotrends.net",
    placement: CHART_TITLE_PLACEMENT_BOTTOM
  }
}   
}

```

## Wrapping[​](#wrapping "Direct link to Wrapping")

By default, a chart title will wrap if it is wider than the container the chart is displayed in.

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-column-chart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  title: {
    text: "This chart shows you the figures corresponding to the population of two countries, from the year 2010 through to the year 2012"
  },
  subtitle: {
    text: "Source: https://macrotrends.net"
  }
}   
}

```

### Fill ratio[​](#fill-ratio "Direct link to Fill ratio")

When wrapping is enabled, the maximum length of any line of text is computed according to the current `fillRatio`, which defaults to 0.9, meaning that by default a wrapped line will fill up to 90% of the available width. You can change this value:

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-column-chart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  title: {
    text: "This chart shows you the figures corresponding to the population of two countries, from the year 2010 through to the year 2012",
    fillRatio: 0.75
  },
  subtitle: {
    text: "Source: https://macrotrends.net"
  }
}   
}

```

### No wrapping[​](#no-wrapping "Direct link to No wrapping")

Wrapping can be switched off:

```javascript
title:{
    text:"This chart shows you the figures corresponding to the population of two countries, from the year 2010 through to the year 2012",
    wrap:false
}

```
