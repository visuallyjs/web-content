# Release 1.1.0

June 3, 2026 ·

<!-- -->

4 min read

sporritt

Release 1.1.0 of VisuallyJs adds a couple of very useful capabilities - a component to manage scrollable lists (such as for data mappers), and the ability to declaratively hide/show content based on zoom level.

## Scrolling list manager[​](#scrolling-list-manager "Direct link to Scrolling list manager")

Configure a scrollable list with a single DOM attribute.

![](https://static.visuallyjs.com/img/app-card/list-manager-2400.png)

```javascript
export function MyList() {
    return <div data-vjs-list={true}>
        <div data-vjs-port="1">Item One</div>
        <div data-vjs-port="2">Item Two</div>
        <div data-vjs-port="3">Item Three</div>
        ...
    </div>
}

```

VisuallyJs will attach a listener to this component and then whenever it is scrolled, edges attached to any of the child elements that are scrolled out of view will be moved so that they are attached to the component's container.

## Displaying content based on zoom[​](#displaying-content-based-on-zoom "Direct link to Displaying content based on zoom")

In some applications, you might want to display more content on your nodes and groups when the canvas is zoomed in, and less when it is zoomed out, to reduce clutter. In 1.1.0 we've added support for this across our various library integrations.

* React
* Angular
* Vue
* Svelte

Use the new `useZoom` hook to get access to the current zoom as state:

```tsx
import { useZoom } from '@visuallyjs/browser-ui-react';

export default function ZoomDisplay({ ui, obj, model }) {
  const zoom = useZoom(ui);

  return (
    <div style={{ position: 'absolute', top: 10, left: 10, background: 'white', padding: '5px' }}>
      Current Zoom: {(zoom * 100).toFixed(0)}%
      {zoom > 1.5 && <p>High magnification active</p>}
      {zoom < 0.5 && <p>Low magnification active</p>}
    </div>
  );
}

```

`BaseNodeComponent` and `BaseGroupComponent` now have a `zoom()` signal available for subclasses to use. As shown in this code snippet, you can use the signal both inside your templates, and also to compute dynamic properties:

```typescript
import { Component, computed } from '@angular/core';
import { BaseNodeComponent } from '@visuallyjs/browser-ui-angular';

@Component({ 
  template:`<div>
    {{data.title}}
    @if (zoom() > 1.5) {
      <div class="details">
        <!-- Detailed information shown only when zoomed in -->
        <p>{{ data.description }}</p>
      </div>
    }
  </div>`
})
export class MyCustomNode extends BaseNodeComponent {
    isZoomedIn = computed(() => this.zoom() > 2);
}

```

VisuallyJs provides a `useZoom` composable you can use to show/hide content based on zoom:

```html
<script setup lang="ts">
import { useZoom } from '@visuallyjs/browser-ui-vue';
import { BrowserUI, Node } from '@visuallyjs/browser-ui';

const props = defineProps({
  vertex: Node,
  ui: BrowserUI
})

// 'zoom' is a reactive Ref<number>
const zoom = useZoom(props.ui)
</script>

<template>
  <div class="my-node">
    <!-- Show detailed view when zoomed in (zoom > 1) -->
    <section v-if="zoom > 1" class="detailed-view">
      <p>Detailed Information</p>
    </section>
    
    <!-- Show compact view when zoomed out -->
    <section v-else class="compact-view">
      <span>Compact View</span>
    </section>
  </div>
</template>

```

VisuallyJs provides a `useZoom` reactive state object you can use to selectively show/hide content based on zoom:

```html
<script lang="ts">
    import type { SvelteWrapperProps } from "@visuallyjs/browser-ui-svelte";
    import { useZoom } from "@visuallyjs/browser-ui-svelte";

    // Receive props from VisuallyJS
    let p = $props() as SvelteWrapperProps;
    let { ui } = p;

    // Create the reactive zoom state
    const zoom = useZoom(ui);
</script>

<div style="background-color:blue; width:100%; height:100%;">
    {#if zoom.current > 1}
        <p>This is the detailed description visible at high zoom levels.</p>
    {:else}
        <p>Small description</p>
    {/if}
</div>

```

## Other updates[​](#other-updates "Direct link to Other updates")

In addition to these two new capabilities, we've also made a number of small updates:

* Updated the `ForceDirected` layout to ensure that attraction/repulsion is clamped to a specific range, to avoid blowouts in positioning.
* Palette uses `.vjs-palette-drag-active` and `.vjs-palette-drag-hover` classes now, instead of using the same ones that are used in the edge drag lifecycle.
* Improved API docs
* Fixed issue in Snaplines plugin that would cause it to not reset if drag was aborted.
* Added the ability to provide sort function to the `GridLayout` (and `ColumnLayout`/`RowLayout`)
* Fixed positioning issue when labels on a chart were rotated 45 degrees to maximise space
* Added support for pluggable router

<!-- -->

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets
