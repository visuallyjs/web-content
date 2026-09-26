# Quick Start

## Installation[​](#installation "Direct link to Installation")

First create a new app (if you need to, otherwise skip this and move to the install command below). There are various tools for this, but we'd recommend [Vite](https://vitejs.dev/).

* npm
* pnpm
* yarn
* bun

```bash
npm init vite visuallyjs-app

```

```bash
pnpm create vite visuallyjs-app

```

```bash
yarn create vite visuallyjs-app

```

```bash
bunx create-vite visuallyjs-app

```

Then `cd` into your project directory and install VisuallyJs:

* npm
* pnpm
* yarn
* bun

```bash
npm install @visuallyjs/browser-ui

```

```bash
pnpm add @visuallyjs/browser-ui

```

```bash
yarn add @visuallyjs/browser-ui

```

```bash
bun add @visuallyjs/browser-ui

```

## MCP[​](#mcp "Direct link to MCP")

To speed up your development you can optionally setup our MCP server with your agent - we provide tools for searching the docs and the apidocs for each library integration. A full discussion of our MCP servers are available on [this page](/vanilla/docs/mcp.md), but if you've done this before, this is the command you need:

```bash
npx @visuallyjs/browser-ui-vanilla-mcp

```

## Usage[​](#usage "Direct link to Usage")

What do you want to build? VisuallyJs can be used to build a variety of different solutions. We split them up into four main categories:

#### [Apps](#apps)[​](#apps "Direct link to apps")

Apps use <!-- -->Javascript<!-- --> components to render each node/group in the display. Functionality can be encapsulated in these components. Node/group sizes in an App are typically dependent on CSS and are managed automatically by VisuallyJs. Apps are great when you need rich content in your nodes/groups and you don't want to be limited to using SVG.

#### [Diagrams](#diagrams)[​](#diagrams "Direct link to diagrams")

Diagrams are pure SVG applications, that draw SVG shapes into an SVG canvas, and provide an API to manipulate each cell/link individually. VisuallyJs offers a <!-- -->Javascript<!-- --> component that you can use to seamlessly embed a Diagram into your application, as well as several other components such as a miniview, a palette (from which shapes can be dragged onto the canvas), and basic controls such as pan/zoom/undo/redo etc.

#### [Charts](#charts)[​](#charts "Direct link to charts")

VisuallyJs includes a wide range of chart types—from standard Line and Bar charts to more specialized Pie, Donut, and Scatter charts, which can be rendered standalone, or integrated with the data model that is powering an App or Diagram on the same page.

#### [Dashboards](#dashboards)[​](#dashboards "Direct link to dashboards")

A powerful feature of VisuallyJs is the ability to mix and match different types of components on a single page. You can create a dashboard that combines a rich node-based canvas or a diagram with real-time charts, all powered by the same underlying data model.

For example, you might have an app representing a manufacturing process where clicking on a machine (a node in the app) updates a set of charts showing that machine's performance metrics. Or a supply chain visualizer with an attached sankey diagram giving you insights into the flow of materials - there are endless possibilities.

<!-- -->

### Apps[​](#apps "Direct link to Apps")

We'll use the `Surface` component from `@visuallyjs/browser-ui` to render a zoomable and pannable canvas.

1. Remove all the code from `src/main.js` and replace with this:

```javascript
import '@visuallyjs/browser-ui/css/visuallyjs.css'
import './style.css'

import { ready, createSurface } from '@visuallyjs/browser-ui'

const data = {
        nodes:[
            { id:"1", label:"Hello", left:50, top:50 },
            { id:"2", label:"World", left:50, top:250 }
        ],
        edges:[
            { source:"1", target:"2" }
        ]
    }

ready(() => {
  const surface = createSurface(document.querySelector('#app'))
  surface.model.load({data})
})

```

2. Remove all the code from `src/style.css` and replace with this:

```css
#app {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
}


```

<br />

And that's it! It's very easy to quickly build apps with VisuallyJs. That example uses some default HTML to render the nodes, which is great to get you up and running, but you'll typically want to provide your own. In this next snippet we supply the HTML to render each node and we add a miniview and some controls.

* main.js
* CSS
* html

Replace the contents of `src/main.js` with this:

```javascript
import '../node_modules/@visuallyjs/browser-ui/css/visuallyjs.css'
import './style.css'

import { ready, 
  createSurface, 
  EVENT_TAP,
  ControlsComponent
} from '@visuallyjs/browser-ui'

const data = {
        nodes:[
            { id:"1", label:"Hello", left:50, top:50, bg:"cadetblue" },
            { id:"2", label:"World", left:50, top:200, bg:"forestgreen" }
        ],
        edges:[
            { source:"1", target:"2" }
        ]
    }

const view = {
  nodes:{
    default:{
      template:`<div style="background-color:{{bg}}" class="my-node">{{label}}</div>`,
      events:{
        [EVENT_TAP]:(p) => alert(`You clicked on vertex ${p.obj.id}`)
      }
    }
  }
}    

ready(() => {
  
  const surface = createSurface(document.querySelector('#app'), {
    view
  })
  
  new ControlsComponent(document.getElementById("controls"), surface)
  
  surface.attachMiniview({
    container:document.getElementById("miniview")
  })

  surface.model.load({data})
})

```

Remove all the code from `src/style.css` and replace with this:

```css
#app {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
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

In `index.html`, add two divs as children of the div with id `app`:

```html
<div id="app">
    <div id="controls"></div>
    <div id="miniview"></div>
</div>

```

**********

Try clicking on the label for each node - we've mapped the "tap" event on the default node to a function that shows a popup with the vertex ID. This is a simple example but hopefully gives you an idea of what is possible.

To find out more about building Javascript/Typescript apps with VisuallyJs, we'd suggest [starting here](/vanilla/docs/apps.md).

### Diagrams[​](#diagrams "Direct link to Diagrams")

***

Diagrams use SVG shapes to render their nodes and groups. It's straightforward to create one - first replace the contents of `src/main.js` with this code:

```javascript
import { FLOWCHART_SHAPES, ArrowOverlay, createDiagram } from "@visuallyjs/browser-ui"

const data = {
    nodes:[
        { id:"1", label:"Begin", x:50, y:50, width:100, height:40, type:"terminus" },
        { id:"2", label:"Test", x:70, y:200, width:60, height:60, type:"decision" }
    ],
    edges:[
        { source:"1", target:"2" }
    ]
}
    
const options = {
    shapes:FLOWCHART_SHAPES,
    edges:{
        overlays:[
           { type:ArrowOverlay.type, options:{location:1}}
        ]
    },
    zoomToFit:true
}

const diagram = createDiagram(document.querySelector("#app"), options)

diagram.load({data})


```

Then, remove all the code from `src/style.css` and replace with this:

```css
@import "../node_modules/@visuallyjs/browser-ui/css/visuallyjs.css";

#app {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
}


```

**********

### Charts[​](#charts "Direct link to Charts")

***

VisuallyJs has support for many different types of charts. Here's a simple column chart:

* main.js
* css

Replace the contents of `src/main.js` with this code:

```javascript
import { ColumnChart } from "@visuallyjs/browser-ui"

const data = [ 
    { id:"USA", corn:387749, wheat:45321 },
    { id:"China", corn:280000, wheat:140000 },
    { id:"Brazil", corn:129000, wheat:10000 },
    { id:"EU", corn:64300, wheat:140500 },
    { id:"Argentina", corn:54000, wheat:19500 },
    { id:"India", corn:34300, wheat:113500 }
]

const options = {
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
    ],
    data
}
    
new ColumnChart(document.querySelector("#app"), options)


```

Replace the contents of `src/style.css` with this:

```css
@import "../node_modules/@visuallyjs/browser-ui/css/visuallyjs.css";

#app {
    width:600px;
    height:500px;
    position:relative;
    outline:1px solid;
}


```

Here we pass the data in to the chart when the chart is created, but there are a number of ways to supply data to chart, including the ability for a chart to source its data from the model backing an App or Diagram.

See the [charts docs](/vanilla/docs/charts/concepts/overview.md) for a full discussion of how to use VisuallyJs to render charts.

## Next Steps[​](#next-steps "Direct link to Next Steps")

***

Where to from here?

[Apps](/vanilla/docs/apps.md)

[Read about building professional visual apps with Javascript/Typescript](/vanilla/docs/apps.md)

[Diagrams](/vanilla/docs/diagrams.md)

[Read about how to build SVG diagrams with VisuallyJs](/vanilla/docs/diagrams.md)

[Charts](/vanilla/docs/charts)

[Read about Visually's powerful chart engine](/vanilla/docs/charts)

[Dashboards](/vanilla/docs/dashboards.md)

[Read more about how to build dashboards with VisuallyJs](/vanilla/docs/dashboards.md)

[Templates](/vanilla/templates)

[Clone an app, diagram or chart template project](/vanilla/templates)

[API Reference](/api-reference)

[Browse the VisuallyJs API docs](/api-reference)
