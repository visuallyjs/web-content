# Connecting charts

One of the key requirements of a dashboard is the ability to connect charts to your model. VisuallyJs makes this a snap. On this page we'll run through various basic scenarios, to give you a feel for what's possible.

## Series based charts[​](#series-based-charts "Direct link to Series based charts")

We'll start with a simple example - in this canvas we have a set of nodes that display a value they are tracking.

* Click the +/- buttons to increment/decrement the value.
* Click in whitespace to add a new node at the location you clicked, with a random new value between 0 and 15.

**********

### Column chart[​](#column-chart "Direct link to Column chart")

<!-- -->

## Dual value axis charts[​](#dual-value-axis-charts "Direct link to Dual value axis charts")

Charts with two value axes - such as bubble and scatter charts - are easily integrated too.

### Scatter Chart[​](#scatter-chart "Direct link to Scatter Chart")

Here's a [scatter chart](/svelte/docs/charts/types/scatter-chart.md) which tracks the location of the nodes on the canvas (perhaps not the most useful application, but fun!):

**********

This is the code:

```jsx
<SurfaceProvider>
  <DashboardExampleSurface1/>
  <ScatterChartComponent options={{
    title:{ text:"Node location" },
    series:[{
      xAxisField:"left",
      yAxisField:"top",
      color:"#569934"
    }],
    yAxis:{
      inverted:true
    },
    tooltip:{
      format:"<b>Node: </b>{{point.id}}<b>Value: </b>{{point.value}}<b>Left: </b>{{point.left}}<b>Top: </b>{{point.top}}"
    }}}/>
</SurfaceProvider>

```

Points to note are:

* We map `xAxisField` to `left` and `yAxisField` to `top` - these are the properties used to position nodes on the canvas.
* We mark `yAxis` as `inverted:true`. By default, the Y axis in a dual value chart has its minimum value in the lower left corner, but that is the opposite way to the way that browsers measure Y. So marking the y axis `inverted` means that the scatter points correctly map the Y axis of the nodes in the canvas.

### Bubble Chart[​](#bubble-chart "Direct link to Bubble Chart")

This [bubble chart](/svelte/docs/charts/types/bubble-chart.md) extends the view provided by the scatter chart above to map the `value` field from each node to the bubble size:

**********

* As with the scatter chart, we map `xAxisField` to `left` and `yAxisField` to `top`
* We mark `yAxis` as `inverted:true` - see discussion for scatter chart above
* We map `valueField` to `value`, meaning that the size of each bubble is proportional to the `value` in the node it represents.

note

Bubble charts have a default maximum bubble size of 50 pixels and a default minimum size of 8 pixels. This is to prevent large discrepancies in data values from resulting in bubbles of widely different sizes in the chart. This maximum and minimum can be changed in the chart options.

## Pie Charts[​](#pie-charts "Direct link to Pie Charts")
