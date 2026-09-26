# Connecting charts

One of the key requirements of a dashboard is the ability to connect charts to your model. VisuallyJs makes this a snap. On this page we'll run through various basic scenarios, to give you a feel for what's possible.

## Series based charts[​](#series-based-charts "Direct link to Series based charts")

We'll start with a simple example - in this canvas we have a set of nodes that display a value they are tracking.

* Click the +/- buttons to increment/decrement the value.
* Click in whitespace to add a new node at the location you clicked, with a random new value between 0 and 15.

**********

### Column chart[​](#column-chart "Direct link to Column chart")

There are 3 parts to this currently - the component we use to render each node, the component for the app, and then the wrapper for the app.

* Component
* Node
* App

The component uses a `DashboardExampleNode` to render each node, and sets `zoomToFit:true`, to fit all the nodes in the canvas on load. Then it registers a `canvasClick` event handler, which adds a new node with a random value at the location the user clicked.

```jsx
export default function DashboardExampleSurface1() {
    
    <SurfaceComponent viewOptions={{
        nodes: {
            default: {
                jsx: DashboardExampleNode
            }
        }
    }} data={data1} renderOptions={{
        zoomToFit: true,
        events: {
            "canvasClick": (s, e) => {
                const pos = s.mapEventLocation(e)
                s.model.addNode({
                    left: pos.x,
                    top: pos.y,
                    id: (uuid()).substring(0, 6),
                    value: Math.floor(Math.random() * 15)
                })
            }
        }
    }}>
        <ControlsComponent style={{zIndex: "50"}}/>
        <GridBackgroundComponent/>
    </SurfaceComponent>
}

```

The node component shows the node id and value, plus the +/- buttons to adjust the value. These buttons call `updateNode` to adjust the current value.

```jsx
export default function DashboardExampleNode({data, obj, model}) {
    return <div className="vjs-dashboard-node">
        <span className="vjs-dashboard-id">{data.id}</span>
        <div className="df aic w-100" style={{justifyContent: "center"}}>
            <button onClick={() => model.updateNode(obj, {value:Math.max(0, data.value - 1)})}>-</button>
            <span className="vjs-dashboard-value">{data.value}</span>
            <button onClick={() => model.updateNode(obj, {value:data.value + 1})}>+</button>
        </div>
    </div>
}

```

The code for the component itself is in the 'Component' tab. We've written

```jsx
<div className="vjs-dashboard-example-1">
  <DashboardExampleSurface1/>
</div>

```

##### Node data[​](#node-data "Direct link to Node data")

The data for each node in this app looks like this:

```javascript
{ 
    id:"1", 
    left:50, 
    top:190, 
    label:"One", 
    value:5  
}

```

##### Adding the chart[​](#adding-the-chart "Direct link to Adding the chart")

To help users make sense of what they're seeing, we're going to add a [column chart](/react/docs/charts/types/column-chart.md) to this UI, plotting the `value` field of each node.

**********

To do this, we introduced a `SurfaceProvider` to our wrapper:

```jsx
<div className="vjs-dashboard-example-1">
  <SurfaceProvider>
    <DashboardExampleSurface1/>
    <DashboardExampleChart1/>
  </SurfaceProvider>
</div>

```

and the code for `DashboardExampleChart1` looks like this:

```jsx
export default function DashboardExampleChart1() {
    return <ColumnChartComponent options={{
        title: { text: "Node Values" },
        categoryAxis: {
            title: { text: "Node Id" }
        },
        valueAxis: {
            title: { text: "Value" }
        },
        series: [{ valueField: "value", color:"midnightblue" }],
        tooltip: { format: "{{category}}:{{point.value}}" }
    }}/>
}

```

The key points to note are:

* The column chart component is context aware, and finds the surface (and its model) to attach to automatically
* The `valueField:"value"` chart option is what tells the chart where to find the values to display.

Now whenever there are changes to the model, the chart is repainted. Try clicking the +/- buttons and seeing how the chart redraws, or clicking into whitespace to add a new node. The chart is also fully integrated with the undo/redo buttons.

#### Pie Chart[​](#pie-chart "Direct link to Pie Chart")

The above example uses a column chart, but there are a number of series based charts in VisuallyJs, each of which can be dropped in for the column chart above. For example, we'll use this code for the chart instead, to show a pie chart comparing the `value` field in each node:

```jsx
<div className="vjs-dashboard-example-1">
    <SurfaceProvider>
        <DashboardExampleSurface1/>
        <PieChartComponent options={{
                colors:["#456789"],
                title: { text: "Node Values" },
                series: [{ valueField: "value" }],
                tooltip: { format: "{{category}}:{{point.value}}" }
            }}/>
    </SurfaceProvider>
</div>

```

**********

## Dual value axis charts[​](#dual-value-axis-charts "Direct link to Dual value axis charts")

Charts with two value axes - such as bubble and scatter charts - are easily integrated too.

### Scatter Chart[​](#scatter-chart "Direct link to Scatter Chart")

Here's a [scatter chart](/react/docs/charts/types/scatter-chart.md) which tracks the location of the nodes on the canvas (perhaps not the most useful application, but fun!):

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

This [bubble chart](/react/docs/charts/types/bubble-chart.md) extends the view provided by the scatter chart above to map the `value` field from each node to the bubble size:

**********

* As with the scatter chart, we map `xAxisField` to `left` and `yAxisField` to `top`
* We mark `yAxis` as `inverted:true` - see discussion for scatter chart above
* We map `valueField` to `value`, meaning that the size of each bubble is proportional to the `value` in the node it represents.

note

Bubble charts have a default maximum bubble size of 50 pixels and a default minimum size of 8 pixels. This is to prevent large discrepancies in data values from resulting in bubbles of widely different sizes in the chart. This maximum and minimum can be changed in the chart options.

## Pie Charts[​](#pie-charts "Direct link to Pie Charts")
