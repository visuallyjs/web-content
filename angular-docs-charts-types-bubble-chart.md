# Bubble Chart

Bubble charts are scatter charts where each point has a size representing a third value.

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-bubble-chart [data]="data" [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = [
    {x:10,y:10,r:5},
     {x:20,y:20,r:10},
     {x:15,y:25,r:7}
]
    
  chartOptions = {
  title: {
    text: "Fat/sugar consumption vs obesity"
  },
  series: [
    {
      xAxisField: "sugar",
      yAxisField: "fat",
      valueField: "obesity",
      color: "#456"
    }
  ]
}   
}

```

## Axis origin[​](#axis-origin "Direct link to Axis origin")

By default, the scatter chart will compute min/max values for each axis based upon the dataset, and the minimum value for each axis is not always 0 - you can see this in the chart above, where the minimum on the Y axis is 0, but the minimum on the X axis is 60.

This arrangement is aimed at providing the best visual layout for the user. In some cases, though, you might want to specify the minimum value for one or both axes - either in order to ensure that the user has a clear understanding of the magnitude of the values, or because one or more of your data points is placed on an axis and you wish to improve the clarity - for example:

<br />

In this case you can specify `min` for your axes:

## Specifying Marker[​](#specifying-marker "Direct link to Specifying Marker")

By default, bubble charts use circular markers for each data point. You can customize the marker's appearance using various options in the `ChartSeriesOptions`.

### Marker Type[​](#marker-type "Direct link to Marker Type")

You can change the shape of the marker using the `markerType` option. For example, to use a square marker:

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-bubble-chart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  series: [
    {
      xAxisField: "sugar",
      yAxisField: "fat",
      valueField: "obesity",
      markerType: "square"
    }
  ]
}   
}

```

Valid options are `"circle"` (the default), `"square"` and `"cross"`.

### Marker Size[​](#marker-size "Direct link to Marker Size")

In a bubble chart, `markerSize` is ignored, as the size of each marker is determined by the `valueField` of each data point. You can, however, control the range of sizes that the bubbles can take by using the `minPointSize` and `maxPointSize` options.

The default value for `minPointSize` is 10. There is no default for `maxPointSize`.

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-bubble-chart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  series: [
    {
      xAxisField: "sugar",
      yAxisField: "fat",
      valueField: "obesity",
      minPointSize: 5,
      maxPointSize: 30
    }
  ]
}   
}

```

### Custom Marker Template[​](#custom-marker-template "Direct link to Custom Marker Template")

For full control over the marker's appearance, you can provide an SVG template string using the `marker` option:

```typescript
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"
import { Component } from '@angular/core'
    
@Component({
  selector: 'app-root',
  imports: [VisuallyJsModule],
  template: '<vjs-bubble-chart [options]="chartOptions"/>',
  styleUrl: './app.css'
})
export class App {
    
  data = ...
    
  chartOptions = {
  series: [
    {
      xAxisField: "sugar",
      yAxisField: "fat",
      valueField: "obesity",
      marker: <svg:svg width='18' height='18' viewBox='0 0 6 6'>
<svg:circle cx='3' cy='3' r='2.5' fill='yellow' stroke='black' stroke-width='0.2' />
<svg:circle cx='2' cy='2.2' r='0.3' stroke='black' fill='yellow'/>
<svg:circle cx='4' cy='2.2' r='0.3' stroke='black' fill='yellow' />
<svg:path d='M 1.8 3.8 Q 3 5 4.2 3.8' fill='none' stroke='black' stroke-width='0.3' stroke-linecap='round' />
</svg:svg>
    }
  ]
}   
}

```

This template must be in [VisuallyJs's template syntax](/vanilla/docs/reference/templating.md).

## Options[​](#options "Direct link to Options")

BubbleChartOptions

Options for a bubble chart.

| Name               | Type                                                                                        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| axisFont?          | [FontSpec]()                                                                                | Spec for the font to use for all text on the axes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| axisLineSize?      | number                                                                                      | The width to use if showing a line marking value/category axes. By default, axis lines are not painted.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| colorGenerator?    | [ColorGenerator]()                                                                          | Optional function to call in order to establish the color to be used for each series                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| cornerRadius?      | number                                                                                      | When rounding bar/column corners, use this radius. Defaults to 5 pixels.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| data?              | Array<[ObjectData]()>                                                                       | Optional data to load into the chart.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| dataSource?        | [DataSource]()                                                                              | Optional data source (of type `DataSource`, meaning both `VisuallyJsModel` and `Selection` are supported) from which to retrieve data to load into the chart.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| dataSourceFilter?  | [ChartModelFilter]()                                                                        | When you provide `dataSource`, you can also provide a filter which accepts or rejects specific nodes/groups in the data source.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| defaultColor?      | string                                                                                      | Optional color to use for every series. Overrides any colorGenerator.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| emptyMessage?      | string                                                                                      | Message to display when the chart has no data. Defaults to "No data".                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| grouped?           | boolean                                                                                     | If true, the data will be grouped, if the chart type supports it (eg Bar/Column).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| groupField?        | string                                                                                      | The name of the field that identifies which group a data point belongs to. Defaults to `group`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| height?            | number                                                                                      | Height for the chart. If omitted, height is computed from the width of the chart's container                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| legend?            | boolean \| [LegendSpec]()                                                                   | Either a boolean true/false, indicating the legend should be shown/hidden, or a spec for a legend.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| legendPadding?     | number                                                                                      | When the legend is not floating, this number defines how much whitespace to leave around it.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| maximumMarkerSize? | number                                                                                      | Maximum allowed size for a marker. Defaults to 50 pixels. Set to Infinity to have no maximum (this can have unpleasant UI side effects with some datasets)                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| maxLabelSize?      | number                                                                                      | The maximum size a category label can be as a ratio of the chart's overall size. Category labels are rotated to 45 degrees automatically when they start to overlap each other, but if the labels are long strings then there is a chance they'll use up too much of the available chart space. This value (whose default is 0.2), specifies a hard limit for label size, to avoid that situation. In a chart whose category axis is the X axis, this is applied relative to the height of the chart, and in a chart whose category axis is the Y axis, it's applied relative to the width. |
| maxPointSize?      | number                                                                                      | The maximum size (in pixels) for a bubble. No default.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| minimumMarkerSize? | number                                                                                      | Minimum allowed size for a marker. Defaults to 8 pixels. Set to -Infinity to have no minimum (this can have unpleasant UI side effects with some datasets)                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| minPointSize?      | number                                                                                      | The minimum size (in pixels) for a bubble. Defaults to 10.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| resizeObserver?    | boolean                                                                                     | Defaults to true, meaning the chart will redraw when its container element resizes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| roundCorners?      | boolean                                                                                     | Whether or not to round the corners of bars/columns. Defaults to true                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| series             | Array<[BubbleChartSeriesOptions]()>                                                         | An array of bubble chart series options.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| style?             | [ChartStyleOptions]()                                                                       | Styles for legend and grid.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| subtitle?          | [SubtitleSpec]()                                                                            | Subtitle for the chart.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| title?             | [ChartTitleSpec]()                                                                          | Title for the chart.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| titlePadding?      | number                                                                                      | Padding to leave underneath the title                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| tooltip?           | [TooltipOptions]()                                                                          | Options for the info tooltip.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| url?               | string                                                                                      | Optional URL from which to retrieve data to load into the chart                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| width?             | number                                                                                      | Width for the chart. If omitted, width is computed from the width of the chart's container                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| xAxis?             | [ValueAxisDefinition]()                                                                     | Configuration for the X axis.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| yAxis?             | [ValueAxisDefinition]()                                                                     | Configuration for the Y axis.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| yAxisPadding?      | number                                                                                      | How much padding to leave between the y axes decoration and the chart content area.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| zoom?              | {<br />  enabled:boolean,<br />  initialValue:number,<br />  range:\[number, number]<br />} | Optional zoom configuration.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class                      | Description                                                                                                                        |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-bubble-chart-point`   | Added to each point in a bubble chart                                                                                              |
| `vjs-chart-point`          | Added to each point in a scatter/bubble chart                                                                                      |
| `vjs-chart-point-hit-area` | Added to the hit area elements that represent each data point. These are to assist users in selecting data points which are small. |
