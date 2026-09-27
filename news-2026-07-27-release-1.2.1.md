# Release 1.2.1

July 27, 2026 ·

<!-- -->

7 min read

sporritt

We've pleased to announce the release of VisuallyJs 1.2.1, containing several useful new features and a couple of great starter apps.

* Popups - components that VisuallyJs automatically keeps aligned with some vertex in your canvas, adjusting for pan/zoom as necessary
* A brand AI Agent Builder starter app was added
* Component overlays for Vue and Svelte - use components as overlays, fully wired into the reactive state and the VisuallyJs data model
* Support for marking up properties inside inspectors as belonging to ports on a vertex, allowing you to edit ports in your data model alongside the nodes they belong to
* Several new signals were added to the BaseVertexComponent in Angular, providing reactive state that exposes the edges attached to the vertex.
* We added a new renderer - the Paper component. This is a "static" version of the Surface: nodes, groups and edges are all rendered in the same way, but the view does not support pan or zoom, and the canvas is scaled automatically so that the content is always visible in the viewport.
* We dusted off the FIFA World Cup visualization from 2018 and released it as a starter app for VisuallyJs.

## Popups[​](#popups "Direct link to Popups")

![AI Agent Builder](https://static.visuallyjs.com/img/blog/1.2.1/popups.png)

## AI Agent Builder[​](#ai-agent-builder "Direct link to AI Agent Builder")

![AI Agent Builder](https://static.visuallyjs.com/img/app-card/ai-agent-builder-2400.png)

Everyone's got one of these, and now we do too! But we're pleased to be able to report that this app required far fewer lines of code than similar demonstrations from other libraries (almost 1/5th of the size of the codebase from another well-known diagramming library!). Our AI Agent Builder is fully featured and ready for you to drop in to your app, or use as a base for your own. [Check it out here](https://visuallyjs.com/demonstrations/ai-agent-builder) - a link to the repository is on the demo page.

## Component overlays[​](#component-overlays "Direct link to Component overlays")

Support for using components as overlays has been in our Angular and React integrations for some time now. In 1.2.1 we've also added this feature to our Vue and Svelte integrations.

## Port Inspectors[​](#port-inspectors "Direct link to Port Inspectors")

Inspectors provide a convenient means of wiring up property editors to the vertices in your app. Prior to 1.2.1, though, if you wanted to edit the properties of ports on your vertices, you'd have to setup a separate rendering condition for them. In 1.2.1 we've added support for a new `vjs-port` attribute, which allows you to tell VisuallyJs that some input field in your inspector pertains to a port, not the vertex:

```html
<div>
  <input vjs-att="label"/>  
  <input vjs-port="yes" vjs-att="label"/>
  <input vjs-port="no" vjs-att="label"/>
</div>

```

Here, our inspector allows us to edit the 'label' property on the vertex itself, as well as each of the vertex's ports.

## Angular Signals[​](#angular-signals "Direct link to Angular Signals")

With every release we're modernising and tightening up our Angular integration, and 1.2.1 is no exception - we've added several signals to the BaseVertexComponent, allowing you to reactively access the edges attached to a given vertex. This makes it easy to do things like showing an 'add child' button if the node has no children, for example:

```javascript
@Component({
  template:`<div>
  <h1>{{$data().label}}</h1>
  @if(sourceEdges().length === 0) {
    <button (click)="addChild">Add Child</button>
  }`
})

export class MyComponent extends BaseNodeComponent {}

```

You can get the list of source/target edges connected to just the vertex itself, or all of the source/target edges connected to the vertex and any of its ports.

We've also updated the `SurfaceComponent`, `PaperComponent` and `DiagramComponent` to convert the `data` and `url` inputs into signals. You can still use them as plain old inputs, but now you can wire them up to signals and have the component reload dynamically.

## Paper Component[​](#paper-component "Direct link to Paper Component")

Sometimes you want to render a static view of your dataset, without given users the ability to pan, zoom or drag elements around - but you still want them to be able to interact with, and update, the model. The Paper component gives you that. It's a version of the Surface without pan, zoom or element dragging, and it automatically scales its canvas to fit inside the bounds of the viewport (unless you don't want it to; you can switch off scaling and have it fill its natural size, and the parent will scroll if needs be).

We're using this component in the Group Stage and Journey View components of our FIFA World Cup visualizer - we look forward to seeing what you build with it!

## FIFA World Cup[​](#fifa-world-cup "Direct link to FIFA World Cup")

We released this for JsPlumb back in 2018 but we've always had a soft spot for some of the visualizations it contains, so we've updated it for VisuallyJs and added to our list of starter apps. It's a great showcase for the range of things you can easily build with VisuallyJs, containing several different views of the data, and integrating natively with React, Angular, Vue and Svelte.

![FIFA World Cup](https://static.visuallyjs.com/img/app-card/fifaworldcup-2400.png)

The group stage view, with its high "data-ink" ratio, is one of our favourites:

![FIFA Group Stage](https://static.visuallyjs.com/img/blog/world-cup-group-stage.png)

We're also quite partial to the "journey view", which takes advantage of our new Paper component to render a static view:

![FIFA Journey Viewer](https://static.visuallyjs.com/img/blog/world-cup-journey-stage.png)

[Check out the demonstration here](https://visuallyjs.com/demonstrations/fifaworldcup). There's a link to the repo if you want to clone it.

## Changelog[​](#changelog "Direct link to Changelog")

### General[​](#general "Direct link to General")

* The `EVENT_GRAPH_CLEARED` event, fired by the model, now passes the model that fired it as a payload.
* The Surface was updated to fix an issue where it was holding on to stale viewport dimensions: calling `zoomToFit` after external change to viewport element size would use the cached dimensions.
* Added the `data-vjs-no-events` attribute which can be set on any element inside a node vertex, marking it as excluded from firing mouse events for that vertex.
* Updated `centerOn` and `centerOnAndZoom` in the Surface to support optional centering on multiple elements as opposed to just a single one.
* Added support for a `vjs-port` attribute on controls inside an inspector. This allows you to edit properties on ports inside your vertices from the vertex inspector.

### Breaking[​](#breaking "Direct link to Breaking")

* The previous `Index` class was renamed to `GraphSearchIndex`
* In `BaseAngularOverlayComponent`, the `surface` member was renamed to `ui`; its type is now derived from a type parameter on the class (which you declare when you create a subclass)

### React[​](#react "Direct link to React")

* The `useZoom` hook no longer requires that a `ui` can be passed in: it can derive one from the context.
* `overlays` is now marked optional in the `ReactEdgeMapping` interface used in view options
* Added `SurfacePopup` component, an automatic mechanism for launching a popup on a vertex component and keeping it located correctly as the user pans, zooms and drags the vertex.
* `InspectorComponent` updated to function correctly inside a `PaperProvider` or `PaperComponent`

### Vue[​](#vue "Direct link to Vue")

* Added `SurfacePopup` component, an automatic mechanism for launching a popup on a vertex component and keeping it located correctly as the user pans, zooms and drags the vertex.
* Added support for Vue component overlays

### Svelte[​](#svelte "Direct link to Svelte")

* Added `SurfacePopup` component, an automatic mechanism for launching a popup on a vertex component and keeping it located correctly as the user pans, zooms and drags the vertex.
* Added support for Svelte component overlays

### Angular[​](#angular "Direct link to Angular")

* Added `SurfacePopup` component, an automatic mechanism for launching a popup on a vertex component and keeping it located correctly as the user pans, zooms and drags the vertex.
* Added several new signals to the `BaseVertexComponent` - `sourceEdges()`, `allSourceEdges()`, `targetEdges()` and `allTargetEdges()`. With these signals you can dynamically respond to connectivity changes inside your templates.
* Added `PaperComponent` - a fixed view version of SurfaceComponent, with the same support for rendering but no pan/zoom, and which automatically adjusts its dimensions to fit into its viewport. The "data" and "url" inputs on the `SurfaceComponent`, `PaperComponent` and `DiagramComponent` of the Angular integration were updated to be reactive - you can hook them up to some state and have the component reload the dataset automatically.

<!-- -->

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets
