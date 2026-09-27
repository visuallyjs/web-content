# Release 1.2.0

July 15, 2026 ·

<!-- -->

5 min read

sporritt

This release focuses on a few main things:

## Hooks and Reactivity[​](#hooks-and-reactivity "Direct link to Hooks and Reactivity")

We've updated each of our integrations to be more reactive - the React hooks, for instance, now return reactive state instead of Promises and the Angular service exposes its various members as signals, instead of getters with callbacks. Additionally, we've added a `useVisuallyJsUpdate()` hook to each of our integrations, allowing you to easily extract a dynamically updating value from the underlying model.

## Inspectors[​](#inspectors "Direct link to Inspectors")

Our Vue and Svelte inspectors have been updated to interoperate seamlessly with a piece of reactive state, cutting down on the amount of boilerplate you're required to write

## Starter apps[​](#starter-apps "Direct link to Starter apps")

Each of our library integrations - Vue, React, Svelte and Angular - offers the same full list of starter apps, and all of our starter apps have been updated to take advantage of the many updates 1.2.0 has to offer.

## Changelog[​](#changelog "Direct link to Changelog")

### General updates[​](#general-updates "Direct link to General updates")

* Circular layout has new `centerContent` option, to avoid placing nodes in negative space (useful when used inside a Group in particular)
* New config `groupProperty` added to model options. You can set the name of the property that identifies group membership in your node/group data, if the default value of `group` clashes with your dataset.
* Added `SelectionGenerator` type, defining the `generator` function that can be used to fill a `VisuallyJsSelection`
* Updated transaction handling to ensure the `transaction(...)` method could be nested cleanly
* Added functionality to the `Palette` in "tap" mode where you can tap an item again to exit the drag (previously you'd have to press Escape)

### React[​](#react "Direct link to React")

* `data` and `url` are now reactive props in the React `SurfaceComponent`. A small but very powerful change, allowing much greater composability of the `SurfaceComponent` in your apps
* Added new React `PaperComponent`, which functions as a static version of a surface - no pan/zoom or dragging, and the content is zoomed to fit the viewport at all times.
* Added new `useVisuallyJsUpdate` hook. This hook lets you respond to updates in the underlying model, and is handy for such use cases as components which display information about the current state of the model.
* (breaking) The `useZoom()`, `useVisuallyJsModel()` and `useDiagram()` React hooks now return a reactive state object instead of a Promise.

### Angular[​](#angular "Direct link to Angular")

* Added new `useVisuallyJsUpdate` hook. This hook lets you respond to updates in the underlying model, and is handy for such use cases as components which display information about the current state of the model.
* Added new `useZoom` hook, providing access to a signal containing the current zoom for the UI in context.
* Converted the `VisuallyJsService` to expose model/surface/paper/diagram as signals, and deprecated the previous callback approach to accessing these members.
* Updated the `Gantt` starter app to have feature parity with the React Gantt

### Svelte[​](#svelte "Direct link to Svelte")

* Added new `useVisuallyJsUpdate` hook. This hook lets you respond to updates in the underlying model, and is handy for such use cases as components which display information about the current state of the model.
* Added new `NetworkInfrastructure` and `SupplyChain` starter apps. These are clones of the same apps that previously only existed for React/Angular, demonstrating how to build integrated dashboards with various VisuallyJs components sharing a single model.
* Added `BPMN` starter app
* Updated the `Gantt` starter app to have feature parity with the React Gantt
* Updated all of the chart components to source their data from a model in scope, when data/url not provided
* Replaced all usages of `<slot></slot>` elements with the modern `{@render children?.()}` syntax
* Updated `InspectorComponent` to optionally take a 2-way state object defining the current selection. This reduces the amount of boilerplate code required to use the inspector.
* Updated the `SankeyChartComponent` to set the `pivot` property to be reactive
* Added `Mindmap` starter app
* (breaking) The `useZoom()` hook no longer takes `ui` as a prop; it finds the UI from the context

### Vue[​](#vue "Direct link to Vue")

* Added new `useVisuallyJsUpdate` composable
* Updated the `Gantt` starter app to have feature parity with the React Gantt
* Updated `InspectorComponent` to support passing in a `v-model`, which is a reactive object that references the current selected object. Using this, you can do away with the need for `refresh` and `renderEmptyContainer` functions (and that approach is now deprecated)
* Added `BPMN` starter app
* Added `useSurface`, `usePaper` and `useDiagram` composables, for access to the UI in scope
* (breaking) Updated `useZoom` to not take a `ui` as argument, instead resolving the UI from the context
* Added `ERD` starter app - an entity relationship diagram
* Added `Mindmap` starter app
* Added new `NetworkInfrastructure` starter app

### Breaking[​](#breaking "Direct link to Breaking")

* The `useZoom()`, `useVisuallyJsModel()` and `useDiagram()` React hooks now return a reactive state object instead of a Promise.
* The `useZoom()` hook in the Svelte integration no longer takes `ui` as a prop; it finds the UI from the context
* The `useZoom()` composable in the Vue integration no longer takes a `ui` as argument, instead resolving the UI from the context

### Deprecated[​](#deprecated "Direct link to Deprecated")

* The `getModel`, `getSurface`, `getPaper`, `getInspector` and `getDiagrams` methods of the Angular `VisuallyJsService` are deprecated. Use the signals based approach instead.
* The `refresh` and `renderEmptyContainer` functions in the `InspectorComponent` for both the Vue and Svelte integrations are deprecated; see above for alternatives.

<!-- -->

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets
