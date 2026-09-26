# Quick Start

## Installation[​](#installation "Direct link to Installation")

First create a new Vue application (if you need to, otherwise skip this and move to the install command below). There are various tools for this, but we'd recommend [Vite](https://vitejs.dev/).

* npm
* pnpm
* yarn
* bun

#### Javascript

```bash
npm init vite visuallyjs-app -- --template vue

```

#### Typescript

```bash
npm init vite visuallyjs-app -- --template vue-ys

```

#### Javascript

```bash
pnpm create vite visuallyjs-app -- --template vue

```

#### Typescript

```bash
pnpm create vite visuallyjs-app -- --template vue-ys

```

#### Javascript

```bash
yarn create vite visuallyjs-app -- --template vue

```

#### Typescript

```bash
yarn create vite visuallyjs-app -- --template vue-ys

```

#### Javascript

```bash
bunx create-vite visuallyjs-app -- --template vue

```

#### Typescript

```bash
bunx create-vite visuallyjs-app -- --template vue-ys

```

Then `cd` into your project directory and install VisuallyJs:

* npm
* pnpm
* yarn
* bun

```bash
npm install @visuallyjs/browser-ui-vue

```

```bash
pnpm add @visuallyjs/browser-ui-vue

```

```bash
yarn add @visuallyjs/browser-ui-vue

```

```bash
bun add @visuallyjs/browser-ui-vue

```

## MCP[​](#mcp "Direct link to MCP")

To speed up your development you can optionally setup our MCP server with your agent - we provide tools for searching the docs and the apidocs for each library integration. A full discussion of our MCP servers are available on [this page](/vue/docs/mcp.md), but if you've done this before, this is the command you need:

```bash
npx @visuallyjs/browser-ui-vue-mcp

```

## Setup[​](#setup "Direct link to Setup")

The first thing to do is to import the VisuallyJs Vue plugin, and ensure the VisuallyJs default CSS is available. Update `src/main.js` so that it looks like this:

```javascript
import { createApp } from 'vue'
import './style.css'
import App from './App.vue'

import { VisuallyJsPlugin } from "@visuallyjs/browser-ui-vue";

const app = createApp(App);
app.use(VisuallyJsPlugin);
app.mount('#app')

```

Now you're ready to build something!

## Start Building[​](#start-building "Direct link to Start Building")

What do you want to build? VisuallyJs can be used to build a variety of different solutions. We split them up into four main categories:

#### [Apps](#apps)[​](#apps "Direct link to apps")

Apps use <!-- -->Vue<!-- --> components to render each node/group in the display. Functionality can be encapsulated in these components. Node/group sizes in an App are typically dependent on CSS and are managed automatically by VisuallyJs. Apps are great when you need rich content in your nodes/groups and you don't want to be limited to using SVG.

#### [Diagrams](#diagrams)[​](#diagrams "Direct link to diagrams")

Diagrams are pure SVG applications, that draw SVG shapes into an SVG canvas, and provide an API to manipulate each cell/link individually. VisuallyJs offers a <!-- -->Vue<!-- --> component that you can use to seamlessly embed a Diagram into your application, as well as several other components such as a miniview, a palette (from which shapes can be dragged onto the canvas), and basic controls such as pan/zoom/undo/redo etc.

#### [Charts](#charts)[​](#charts "Direct link to charts")

VisuallyJs includes a wide range of chart types—from standard Line and Bar charts to more specialized Pie, Donut, and Scatter charts, which can be rendered standalone, or integrated with the data model that is powering an App or Diagram on the same page.

#### [Dashboards](#dashboards)[​](#dashboards "Direct link to dashboards")

A powerful feature of VisuallyJs is the ability to mix and match different types of components on a single page. You can create a dashboard that combines a rich node-based canvas or a diagram with real-time charts, all powered by the same underlying data model.

For example, you might have an app representing a manufacturing process where clicking on a machine (a node in the app) updates a set of charts showing that machine's performance metrics. Or a supply chain visualizer with an attached sankey diagram giving you insights into the flow of materials - there are endless possibilities.

<!-- -->

### Build an App[​](#build-an-app "Direct link to Build an App")

1. Remove all the code from `src/App.vue` and replace with this:

```html
<script setup>
data = {
  nodes:[
    { id:"1", label:"Hello", left:50, top:50 }, 
    { id:"2", label:"World", left:50, top:250 }
  ],
  edges:[
    { source:"1", target:"2" }
  ]
}
</script>

<template>
  <div class="my-container">
    <SurfaceComponent :data="data"/>
  </div>
</template>

```

2. Add this to `src/style.css`:

```css

@import "@visuallyjs/browser-ui/css/visuallyjs.css";

.my-container {
    width:100%;
    height:500px;
    position:relative;
}



```

<br />

And that's it! It's very easy to quickly build apps with VisuallyJs. That example uses a default Vue component to render the nodes, which is great to get you up and running, but you'll typically want to provide your own. In this next snippet we supply the component to render each node and we add a miniview and some controls:

* App.vue
* MyComponent.vue
* style.css

Remove all the code from `App.vue` and replace with this:

```html
<script setup>
import MyComponent from "./components/MyComponent.vue"

const viewOptions = {
  nodes:{
    default:{
      component:MyComponent
    }
  }
}

const data = {
  nodes:[
    { id:"1", label:"Hello", left:50, top:50, bg:"cadetblue" },
    { id:"2", label:"World", left:50, top:200, bg:"forestgreen" }
  ],
  edges:[
    { source:"1", target:"2" }
  ]
}
    
</script>
    
<template>
  <div class="my-container">
    <SurfaceComponent :data="data" :viewOptions="viewOptions"/>
    <MiniviewComponent/>        
    <ControlsComponent/>
  </div>
</template>

```

Create `src/components/MyComponent.vue` and make this the content:

```html
<script setup>

const {model, obj} = defineProps()

function info() {
	alert(`You clicked on vertex ${obj.id}`)
}

</script>
<template>
    <div class="my-node" :style="{backgroundColor:obj.bg}" >
        <span @click="info()">{{obj.label}}</span>
    </div>
</template>


```

Add this to `src/style.css`:

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

Try clicking on the label for each node - you'll get a popup with its ID, which is sourced from the vertex passed in via the props as `obj`. This is a simple example but hopefully gives you an idea of what is possible when you use Vue components to render the nodes in your UI.

To find out more about building Vue apps with VisuallyJs, we'd suggest [starting here](/vue/docs/apps.md).

### Build a Diagram[​](#build-a-diagram "Direct link to Build a Diagram")

***

Diagrams use SVG shapes to render their nodes and groups. It's straightforward to create one:

* App.vue
* css

Remove all the code from `src/App.vue` and replace with this:

```html
<script setup>
import { FLOWCHART_SHAPES, ArrowOverlay } from "@visuallyjs/browser-ui"

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
const data = {
  nodes:[
    {id:"1",label:"Begin",x:50,y:50,width:100,height:40,type:"terminus"},
     {id:"2",label:"Test",x:70,y:200,width:60,height:60,type:"decision"}
  ],
  edges:[
    {source:"1",target:"2"}
  ]
}
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

Add this to `src/style.css`:

```css

@import "@visuallyjs/browser-ui/css/visuallyjs.css";

.my-container {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
}


```

**********

### Build a Chart[​](#build-a-chart "Direct link to Build a Chart")

***

VisuallyJs has support for many different types of charts. Here's a simple column chart:

* App.vue
* css

Remove all the code from `src/App.vue` and replace with this:

```html
<script setup>
    
const data = ... 

const options = {
  title: {
    text: "Corn vs wheat estimated production for 2023"
  },
  valueAxis: [
    {
      title: {
        text: "1000 metric tons (MT)"
      }
    }
  ],
  series: [
    {
      valueField: "corn",
      label: "Corn"
    },
    {
      valueField: "wheat",
      label: "Wheat"
    }
  ],
  data: [
    {
      id: "USA",
      corn: 387749,
      wheat: 45321
    },
    {
      id: "China",
      corn: 280000,
      wheat: 140000
    },
    {
      id: "Brazil",
      corn: 129000,
      wheat: 10000
    },
    {
      id: "EU",
      corn: 64300,
      wheat: 140500
    },
    {
      id: "Argentina",
      corn: 54000,
      wheat: 19500
    },
    {
      id: "India",
      corn: 34300,
      wheat: 113500
    }
  ]
}
   
</script>
<template>
        <ColumnChartComponent className="my-container" :data="data" :options="options"/>        
</template>

```

Add this to `src/style.css`:

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

See the [charts docs](/vue/docs/charts/concepts/overview.md) for a full discussion of how to use VisuallyJs to render charts.

### Build a Dashboard[​](#build-a-dashboard "Direct link to Build a Dashboard")

***

It's easy to build dashboards with VisuallyJs where multiple components all reference the same data model. Here we'll show you a quick example which is from our [dashboards documentation](/vue/docs/dashboards.md) - a scatter chart that reflects the positions of the nodes in the canvas.

* App.vue
* MyComponent.vue
* style.css

Remove all the code from `App.vue` and replace with this:

```html
<script setup>
import MyComponent from "./components/MyComponent.vue"

const viewOptions = {
  nodes:{
    default:{
      component:MyComponent
    }
  }
}

const data = {
  nodes:[
	  { id:"1", label:"Hello", left:50, top:50 },
	  { id:"2", label:"World", left:50, top:250 },
	  { id:"3", label:"Hola", left:250, top:150 }
  ],
  edges:[
    { source:"1", target:"2" }
  ]
}

const chartOptions = {
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
    
<template>
  <div class="my-container">
      <SurfaceProvider>
        <SurfaceComponent :data="data" :viewOptions="viewOptions"/>
        <ControlsComponent/>
		<ScatterChartComponent :options="chartOptions"/>
	  </SurfaceProvider>
  </div>
</template>

```

Create `src/components/MyComponent.vue` and make this the content:

```html
<script setup>

const {model, obj} = defineProps()

function info() {
	alert(`You clicked on vertex ${obj.id}`)
}

</script>
<template>
    <div class="my-node" :style="{backgroundColor:obj.bg}" >
        <span @click="info()">{{obj.label}}</span>
    </div>
</template>


```

Add this to `src/style.css`:

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

.my-node {
    color:white;
    display:flex;
    align-items: center;
    justify-content: center;
    width:100px;
    height:60px;
}


```

```css

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

[Apps](/vue/docs/apps.md)

[Read about building professional visual apps with Vue components](/vue/docs/apps.md)

[Diagrams](/vue/docs/diagrams.md)

[Read about how to build SVG diagrams with VisuallyJs Vue](/vue/docs/diagrams.md)

[Charts](/vue/docs/charts)

[Read about Visually's powerful Vue chart engine](/vue/docs/charts)

[Dashboards](/vue/docs/dashboards.md)

[Read more about how to build dashboards with VisuallyJs](/vue/docs/dashboards.md)

[Templates](/vue/templates)

[Clone an app, diagram or chart template project](/vue/templates)

[API Reference](/api-reference)

[Browse the VisuallyJs API docs](/api-reference)
