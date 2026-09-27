# Annotating objects with drag groups

May 18, 2026 ·

<!-- -->

8 min read

One of the key differentiators between VisuallyJs and other libraries in this space is VisuallyJs's level of configurability - more often than not you'll find that once you hit a blocker in some other library, VisuallyJs will offer you the ability to do what you need.

A great example of this is VisuallyJs's concept of a `DragGroup`. Simply put, this is a group of vertices that should be dragged together - but as we'll see, it's not quite as simple as that, and it can be used to great effect with minimal work required on your part.

### Active vs passive members[​](#active-vs-passive-members "Direct link to Active vs passive members")

In this canvas, try dragging the large green box around. You'll see the two red boxes drag along with it. Now try dragging one of the red boxes - nothing else moves. This is because all of the nodes are inside a drag group, but the large green node is marked `active` and the red nodes are marked `passive`:

**********

<!-- -->

* React
* Vue
* Angular
* Svelte
* Javascript

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { DragGroupsPlugin } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return { id:'dragGroup', active:v.type === 'main' }
        }
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

```html
<script setup>

import { DragGroupsPlugin } from "@visuallyjs/browser-ui"

const renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return { id:'dragGroup', active:v.type === 'main' }
        }
      }
    }
  ]
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { DragGroupsPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return { id:'dragGroup', active:v.type === 'main' }
        }
      }
    }
  ]
};
}

```

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { DragGroupsPlugin } from "@visuallyjs/browser-ui"
  const renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return { id:'dragGroup', active:v.type === 'main' }
        }
      }
    }
  ]
}
</script>

<SurfaceComponent {renderOptions}/>

```

```javascript
import { newInstance, DragGroupsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return { id:'dragGroup', active:v.type === 'main' }
        }
      }
    }
  ]
})

```

Our dataset looks like this:

```javascript
{
  nodes:[
    {id:"1", left:50, top:50, type:"main" },
    {id:"2", left:250, top:160 },
    {id:"3", left:350, top:100 }
  ]
}

```

The key is the `assignDragGroup` function that we provide. In the implementation above we do two things:

* all vertices are assigned to a drag group called `"dragGroup"`
* The vertex whose `type` is `"main"` is marked `active:true`; the others are marked `active:false`

### Multiple drag groups[​](#multiple-drag-groups "Direct link to Multiple drag groups")

Our example above used a single drag group, but just in case you're wondering, you can have as many of these as you want. For instance, here's a canvas in which all the red elements are dragged in a single group, and all the green elements are dragged in a different group:

**********

This was an even simpler setup - we just use each node's `type` to specify its drag group:

* React
* Vue
* Angular
* Svelte
* Javascript

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { DragGroupsPlugin } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type
        }
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

```html
<script setup>

import { DragGroupsPlugin } from "@visuallyjs/browser-ui"

const renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type
        }
      }
    }
  ]
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { DragGroupsPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type
        }
      }
    }
  ]
};
}

```

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { DragGroupsPlugin } from "@visuallyjs/browser-ui"
  const renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type
        }
      }
    }
  ]
}
</script>

<SurfaceComponent {renderOptions}/>

```

```javascript
import { newInstance, DragGroupsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type
        }
      }
    }
  ]
})

```

Every element in this example is marked `active` because that's the default if you do not specify it. All we had to do in this example is return the name of a drag group and VisuallyJs adds the vertex as an active participant to that group.

Our dataset in this example is:

```javascript
{
  nodes:[
    {id:"1", left:50, top:50, type:"green" },
    {id:"2", left:150, top:160, type:"red" },
    {id:"3", left:200, top:30, type:"red" },
    {id:"4", left:250, top:100, type:"green" }
  ]
}

```

### Annotating Objects[​](#annotating-objects "Direct link to Annotating Objects")

To get back to the point of this post: how can we use this functionality to annotate objects? A key requirement when implementing the ability to annotate objects in a diagram is that the user wants to be able to place the annotation wherever they like around the object that is being annotated, depending on what else is in the diagram. So the annotation needs to be draggable, but if the user moves the annotated object, the annotation should stay close - and that's why we think the drag groups plugin is perfect for the job.

Consider this dataset:

```javascript
{
  nodes:[
      { id:"1", type:"main", left:50, top:50 },
      { id:"2", type:"main", left:300, top:50 },
      { id:"3", type:"annotation", text:"I belong to node 1", ref:"1", left:70, top:-40 },
      { id:"4", type:"annotation", text:"I belong to node 1", ref:"1", left:-90, top:120 },
      { id:"5", type:"annotation", text:"I belong to node 2", ref:"2", left:380, top:160 }
  ]
}

```

We've got two nodes of type `main`, and three nodes of type `annotation`, each of which have a `ref` member, which points to a `main` node. We want to be able to drag our `main` nodes around and have the `annotation` nodes follow, but we also want to be able to position the `annotation` nodes around the `main` nodes where we please. This is easily achieved:

* React
* Vue
* Angular
* Svelte
* Javascript

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { DragGroupsPlugin } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type === 'main' ? v.id : {id:v.data.ref, active:false}
        }
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

```html
<script setup>

import { DragGroupsPlugin } from "@visuallyjs/browser-ui"

const renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type === 'main' ? v.id : {id:v.data.ref, active:false}
        }
      }
    }
  ]
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { DragGroupsPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type === 'main' ? v.id : {id:v.data.ref, active:false}
        }
      }
    }
  ]
};
}

```

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { DragGroupsPlugin } from "@visuallyjs/browser-ui"
  const renderOptions = {
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type === 'main' ? v.id : {id:v.data.ref, active:false}
        }
      }
    }
  ]
}
</script>

<SurfaceComponent {renderOptions}/>

```

```javascript
import { newInstance, DragGroupsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: DragGroupsPlugin.type,
      options: {
        assignDragGroup: (v) => {
          return v.type === 'main' ? v.id : {id:v.data.ref, active:false}
        }
      }
    }
  ]
})

```

* For nodes of type `main`, we just return the node's id: `v.id`
* For nodes of type `annotation`, we return the `ref` as the drag group id, and mark the vertex passive: `{id:v.data.ref, active:false}`.

Which gives us this arrangement. Dragging a green node will drag its related annotations along with it, but annotations can be dragged separately, to position them in relation to their reference element:

**********

And there you have it! Annotated objects using just a few lines of configuration.

### Housekeeping[​](#housekeeping "Direct link to Housekeeping")

One thing to keep in mind is that the annotations and the edges that connect them to their reference nodes will not automatically be removed by VisuallyJs if the reference node is removed from the dataset. Don't worry, though - we've got you. We'll use another of VisuallyJs's capabilities you won't find in other libraries in this space - [](/undefined/docsundefined)- to cleanup the annotations, but in an undo/redo friendly way.

Try clicking one of the ✖ buttons below. We'll remove the node the button belongs to, and we'll also remove any annotations that are attached to it (code follows below) :

**********

To remove a node and its annotations in an undo-friendly way, we find everything we want to delete and then perform all the removals inside a transaction. An example function, into which you'd pass the VisuallyJs instance and the ID of the node to cleanup, is:

```javascript
function removeNode(model, nodeId) {
    const annotations = model.getNodes().filter(n => n.data.ref === nodeId)

    model.transaction(() => {
      annotations.forEach(a => model.removeNode(a))
      model.removeNode(nodeId)
    })
}

```

***

## Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

Interested in trying VisuallyJs? Information on how to do so can be found on our site here: <https://visuallyjs.com/trial>

***

## Get in touch\![​](#get-in-touch "Direct link to Get in touch!")

If you'd like to discuss any of the ideas/concepts in this article we'd love to hear from you - drop us a line at <hello@visuallyjs.com>.

***

***

### Try VisuallyJs[​](#try-visuallyjs-1 "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets

**Tags:**

* [svg](/news/tags/svg.md)
* [flowchart](/news/tags/flowchart.md)
* [inspector](/news/tags/inspector.md)
* [erd](/news/tags/erd.md)
* [svg export](/news/tags/svg-export.md)
* [png](/news/tags/png.md)
* [jpeg](/news/tags/jpeg.md)
* [jpg](/news/tags/jpg.md)
* [apidocs](/news/tags/apidocs.md)
* [gantt](/news/tags/gantt.md)
* [gantt chart](/news/tags/gantt-chart.md)
* [network topology](/news/tags/network-topology.md)
* [jointjs](/news/tags/jointjs.md)
* [reactflow](/news/tags/reactflow.md)
* [gojs](/news/tags/gojs.md)
