# Release 1.1.1

June 9, 2026 ·

<!-- -->

2 min read

sporritt

Release 1.1.1 adds support for rotating label and custom overlays to match their connectors. Here's our flowchart starter app with this functionality enabled:

![Rotating labels](https://static.visuallyjs.com/img/blog/rotated-label-1.1.1.png)

This feature is supported both in the `edges` config for a diagram:

* React
* Vue
* Angular
* Svelte

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  edges: {
    showLabels: true,
    labelsRotatable: true,
    targetMarker: "PlainArrow"
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

```html
<script setup>


const options = {
  edges: {
    showLabels: true,
    labelsRotatable: true,
    targetMarker: "PlainArrow"
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  edges: {
    showLabels: true,
    labelsRotatable: true,
    targetMarker: "PlainArrow"
  }
}
}

```

```html
<script>

import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  edges: {
    showLabels: true,
    labelsRotatable: true,
    targetMarker: "PlainArrow"
  }
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

**********

and inside the edges defined in a view for an App:

<!-- -->

* React
* Vue
* Angular
* Svelte
* Javascript

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const viewOptions = {
  edges: {
    default: {
      label: "{{label}}",
      labelsRotatable: true,
      targetMarker: "PlainArrow"
    }
  }
}
  return <SurfaceComponent viewOptions={viewOptions}/>
}

```

```html
<script setup>

function viewOptions() {
  return {
  edges: {
    default: {
      label: "{{label}}",
      labelsRotatable: true,
      targetMarker: "PlainArrow"
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

```

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [viewOptions]="viewOptions"></vjs-surface> `
})
export class AppComponent {
  viewOptions = {
  edges: {
    default: {
      label: "{{label}}",
      labelsRotatable: true,
      targetMarker: "PlainArrow"
    }
  }
};
}

```

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const viewOptions = {
  edges: {
    default: {
      label: "{{label}}",
      labelsRotatable: true,
      targetMarker: "PlainArrow"
    }
  }
}
</script>

<SurfaceComponent {viewOptions}/>

```

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  view: {
    edges: {
      default: {
        label: "{{label}}",
        labelsRotatable: true,
        targetMarker: "PlainArrow"
      }
    }
  }
})

```

**********

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets
