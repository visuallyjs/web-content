# Quick Start

## Installation[​](#installation "Direct link to Installation")

First create a new app (if you need to, otherwise skip this and move to the install command below). There are various tools for this, but we'd recommend [Vite](https://vitejs.dev/).

* npm
* pnpm
* yarn
* bun

#### Javascript

```bash
npm init vite visuallyjs-app -- --template svelte

```

#### Typescript

```bash
npm init vite visuallyjs-app -- --template svelte-ts

```

#### Javascript

```bash
pnpm create vite visuallyjs-app -- --template svelte

```

#### Typescript

```bash
pnpm create vite visuallyjs-app -- --template svelte-ts

```

#### Javascript

```bash
yarn create vite visuallyjs-app -- --template svelte

```

#### Typescript

```bash
yarn create vite visuallyjs-app -- --template svelte-ts

```

#### Javascript

```bash
bunx create-vite visuallyjs-app -- --template svelte

```

#### Typescript

```bash
bunx create-vite visuallyjs-app -- --template svelte-ts

```

Then `cd` into your project directory and install VisuallyJs:

* npm
* pnpm
* yarn
* bun

```bash
npm install @visuallyjs/browser-ui-svelte

```

```bash
pnpm add @visuallyjs/browser-ui-svelte

```

```bash
yarn add @visuallyjs/browser-ui-svelte

```

```bash
bun add @visuallyjs/browser-ui-svelte

```

## MCP[​](#mcp "Direct link to MCP")

To speed up your development you can optionally setup our MCP server with your agent - we provide tools for searching the docs and the apidocs for each library integration. A full discussion of our MCP servers are available on [this page](/svelte/docs/mcp.md), but if you've done this before, this is the command you need:

```bash
npx @visuallyjs/browser-ui-svelte-mcp

```

## Start Building[​](#start-building "Direct link to Start Building")

What do you want to build? VisuallyJs can be used to build a variety of different solutions. We split them up into four main categories:

#### [Apps](#apps)[​](#apps "Direct link to apps")

Apps use <!-- -->Svelte<!-- --> components to render each node/group in the display. Functionality can be encapsulated in these components. Node/group sizes in an App are typically dependent on CSS and are managed automatically by VisuallyJs. Apps are great when you need rich content in your nodes/groups and you don't want to be limited to using SVG.

#### [Diagrams](#diagrams)[​](#diagrams "Direct link to diagrams")

Diagrams are pure SVG applications, that draw SVG shapes into an SVG canvas, and provide an API to manipulate each cell/link individually. VisuallyJs offers a <!-- -->Svelte<!-- --> component that you can use to seamlessly embed a Diagram into your application, as well as several other components such as a miniview, a palette (from which shapes can be dragged onto the canvas), and basic controls such as pan/zoom/undo/redo etc.

#### [Charts](#charts)[​](#charts "Direct link to charts")

VisuallyJs includes a wide range of chart types—from standard Line and Bar charts to more specialized Pie, Donut, and Scatter charts, which can be rendered standalone, or integrated with the data model that is powering an App or Diagram on the same page.

#### [Dashboards](#dashboards)[​](#dashboards "Direct link to dashboards")

A powerful feature of VisuallyJs is the ability to mix and match different types of components on a single page. You can create a dashboard that combines a rich node-based canvas or a diagram with real-time charts, all powered by the same underlying data model.

For example, you might have an app representing a manufacturing process where clicking on a machine (a node in the app) updates a set of charts showing that machine's performance metrics. Or a supply chain visualizer with an attached sankey diagram giving you insights into the flow of materials - there are endless possibilities.

<!-- -->

### Build an App[​](#build-an-app "Direct link to Build an App")

We'll use the `SurfaceComponent` from `@visuallyjs/browser-ui-svelte` to render a zoomable and pannable canvas.

1. Remove all the code from `src/App.svelte` and replace with this:

```html
<script>
    import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
    
    const data = {
        nodes:[
            { id:"1", label:"Hello", left:50, top:50 },
            { id:"2", label:"World", left:50, top:250 }
        ],
        edges:[
            { source:"1", target:"2" }
        ]
    }

</script>

<div class="my-container">
  <SurfaceComponent data={data}/>
</div>


```

2. Remove all the code from `src/app.css` and replace with this:

```css
@import "../node_modules/@visuallyjs/browser-ui/css/visuallyjs.css";

.my-container {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
}

.vjs-surface {
    width:100%;
    height:100%;
}


```

<br />

And that's it! It's very easy to quickly build apps with VisuallyJs. That example uses a default component to render the nodes, which is great to get you up and running, but you'll typically want to provide your own. In this next snippet we supply the component to render each node and we add a miniview and some controls.

* App.svelte
* MyComponent.svelte
* css

Replace the contents of `src/App.svelte` with this:

```html
<script>

  import { 
    SurfaceProvider, 
    SurfaceComponent, 
    ControlsComponent, 
    MiniviewComponent } from "@visuallyjs/browser-ui-svelte"

  import MyComponent from "./lib/MyComponent.svelte";

  const data = {
        nodes:[
            { id:"1", label:"Hello", left:50, top:50, bg:"cadetblue" },
            { id:"2", label:"World", left:50, top:200, bg:"forestgreen" }
        ],
        edges:[
            { source:"1", target:"2" }
        ]
    }

  const viewOptions = {
      nodes:{
        default:{
          component:MyComponent
          }
       }
    }

</script>

<div class="my-container">
  <SurfaceProvider>
    <SurfaceComponent data={data} viewOptions={viewOptions}/>
    <MiniviewComponent/>
    <ControlsComponent/>
  </SurfaceProvider>
</div>


```

Create `src/lib/MyComponent.svelte` and paste this code:

```html
<script>
    export let data;
    export let vertex;
    export let surface;
    export let model;

    function info() {
        alert(`You clicked on vertex ${data.id}`)
    }

</script>

<div style="background-color:{data.bg}" class="my-node">
    <span on:click={info}>{data.label}</span>
</div>

```

Remove all the code from `src/app.css` and replace with this:

```css
@import "../node_modules/@visuallyjs/browser-ui/css/visuallyjs.css";

.my-container {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
}

.vjs-surface {
    width:100%;
    height:100%;
}

.my-node {
    color:white;
    display:flex;
    align-items: center;
    justify-content: center;
    width:100px;
    height:60px;
}


```

**********

Try clicking on the label for each node - you'll get a popup with its ID, which we sourced from the `data` prop of the component. You might have noticed that our `MyComponent` actually declares 4 props - they're not all used in this example, but VisuallyJs passes in the current `Surface`, the `Vertex` model object, the `data` backing the object, and the data model itself. With all these props available you can implement flexible and powerful components.

This is a simple example but hopefully gives you an idea of what is possible when you use Svelte components to render the nodes in your UI.

To find out more about building Svelte apps with VisuallyJs, we'd suggest [starting here](/svelte/docs/apps.md).

### Build a Diagram[​](#build-a-diagram "Direct link to Build a Diagram")

***

Diagrams use SVG shapes to render their nodes and groups. It's straightforward to create one - first replace the contents of `src/App.svelte` with this code:

```html
<script>
import { FLOWCHART_SHAPES, ArrowOverlay } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = {
  nodes:[
    {id:"1",label:"Begin",x:50,y:50,width:100,height:40,type:"terminus"},
     {id:"2",label:"Test",x:70,y:200,width:60,height:60,type:"decision"}
  ],
  edges:[
    {source:"1",target:"2"}
  ]
}
    
const options = {
  shapes: FLOWCHART_SHAPES,
  edges: {
    overlays: [
      {
        type: ArrowOverlay.type,
        options: {
          location: 1
        }
      }
    ]
  },
  zoomToFit: true
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

Then, remove all the code from `src/app.css` and replace with this:

```css
@import "@visuallyjs/browser-ui/css/visuallyjs.css";

.my-container {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
}

.vjs-surface {
    width:100%;
    height:100%;
}


```

**********

### Build a Chart[​](#build-a-chart "Direct link to Build a Chart")

***

VisuallyJs has support for many different types of charts. Here's a simple column chart:

which we generated with this code:

* App.svelte
* CSS

```html
<script>
import { ColumnChartComponent } from "@visuallyjs/browser-ui-svelte"

const chartData = [ 
      { id:"USA", corn:387749, wheat:45321 },
      { id:"China", corn:280000, wheat:140000 },
      { id:"Brazil", corn:129000, wheat:10000 },
      { id:"EU", corn:64300, wheat:140500 },
      { id:"Argentina", corn:54000, wheat:19500 },
      { id:"India", corn:34300, wheat:113500 }
  ]

  const chartOptions = {
        title: {
            text: 'Corn vs wheat estimated production for 2023'
        },
        valueAxis: [
            {
                title: {
                    text: '1000 metric tons (MT)'
                }
            }
        ],
        series:[
            {
                valueField:"corn",
                label:"Corn"
            },
            {
                valueField:"wheat",
                label:"Wheat"
            }
        ]
    }
</script>

<ColumnChartComponent data={chartData} 
        options={chartOptions} 
        className="my-container"/>
    

```

Remove all the code from `src/app.css` and replace with this:

```css
@import "@visuallyjs/browser-ui/css/visuallyjs.css";

.my-container {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
}

```

Here we pass the data in to the chart when the chart is created, but there are a number of ways to supply data to chart, including the ability for a chart to source its data from the model backing an App or Diagram.

See the [charts docs](/svelte/docs/charts/concepts/overview.md) for a full discussion of how to use VisuallyJs to render charts.

### Build a Dashboard[​](#build-a-dashboard "Direct link to Build a Dashboard")

***

It's easy to build dashboards with VisuallyJs where multiple components all reference the same data model. Here we'll show you a quick example which is from our [dashboards documentation](/svelte/docs/dashboards.md) - a scatter chart that reflects the positions of the nodes in the canvas.

* App.svelte
* CSS

Replace the contents of `src/App.svelte` with this:

```html
<script>
  import { SurfaceProvider, SurfaceComponent, ScatterChartComponent } from "@visuallyjs/browser-ui-svelte"

  const data = {
      nodes:[
          { id:"1", label:"Hello", left:50, top:50 },
          { id:"2", label:"World", left:50, top:250 }
      ],
      edges:[
          { source:"1", target:"2" }
      ]
  }

  const chartOptions={
      series:[
          {
              xAxisField:"left",
              yAxisField:"top",
              color:"#569934"
          }
      ],
      yAxis:{
          inverted:true
      }
  }

</script>

<div class="my-container">
    <SurfaceProvider>
        <SurfaceComponent {data}/>
        <ScatterChartComponent options={chartOptions}/>
    </SurfaceProvider>
</div>

```

Remove all the code from `src/app.css` and replace with this:

```css
@import "@visuallyjs/browser-ui/css/visuallyjs.css";

.my-container {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
    display:flex;
}

.vjs-surface {
    flex:0 0 50%;
    height:100%;
}

.vjs-scatter-chart {
    flex:0 0 50%;
    height:100%;
}

```

**********

## Next Steps[​](#next-steps "Direct link to Next Steps")

***

Where to from here?

[Apps](/svelte/docs/apps.md)

[Read about building professional visual apps with Svelte components](/svelte/docs/apps.md)

[Diagrams](/svelte/docs/diagrams.md)

[Read about how to build SVG diagrams with VisuallyJs](/svelte/docs/diagrams.md)

[Charts](/svelte/docs/charts)

[Read about Visually's powerful chart engine](/svelte/docs/charts)

[Dashboards](/svelte/docs/dashboards.md)

[Read more about how to build dashboards with VisuallyJs](/svelte/docs/dashboards.md)

[Templates](/svelte/templates)

[Clone an app, diagram or chart template project](/svelte/templates)

[API Reference](/api-reference)

[Browse the VisuallyJs API docs](/api-reference)
