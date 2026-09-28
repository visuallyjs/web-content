# I want my MCP

June 7, 2026 ·

<!-- -->

3 min read

sporritt

Integrating an MCP server directly into your development workflow provides a powerful bridge between your IDE and the library documentation you rely on, eliminating the friction of context-switching between your editor and a browser and leading to more accurate, idiomatic implementations and a significantly smoother coding experience.

We are pleased to announce that VisuallyJs now offers an MCP for each of our library integrations. It's so useful that we're actually using it ourselves, both when developing new features and when working on our ever-increasing set of demonstrations and starter apps.

## Setup[​](#setup "Direct link to Setup")

We provide an MCP server for each of our library integrations, as well as a server that covers every integration.

| Package                              | Library                                    | Command                                  |
| ------------------------------------ | ------------------------------------------ | ---------------------------------------- |
| `@visuallyjs/browser-ui-angular-mcp` | Angular                                    | `npx @visuallyjs/browser-ui-angular-mcp` |
| `@visuallyjs/browser-ui-react-mcp`   | React                                      | `npx @visuallyjs/browser-ui-react-mcp`   |
| `@visuallyjs/browser-ui-svelte-mcp`  | Svelte                                     | `npx @visuallyjs/browser-ui-svelte-mcp`  |
| `@visuallyjs/browser-ui-vue-mcp`     | Vue                                        | `npx @visuallyjs/browser-ui-vue-mcp`     |
| `@visuallyjs/browser-ui-vanilla-mcp` | Vanilla JS                                 | `npx @visuallyjs/browser-ui-vanilla-mcp` |
| `@visuallyjs/browser-ui-mcp`         | All (Angular, React, Svelte, Vue, Vanilla) | `npx @visuallyjs/browser-ui-mcp`         |

These are published in the public NPM repository, and, for licensees, our private NPM repository.

If you've done this sort of thing before, the commands listed above will be enough to get you going. To read more about setting up MCP with your library, follow one of these links:

* [Angular](/angular/docs/mcp.md)
* [React](/react/docs/mcp.md)
* [Svelte](/svelte/docs/mcp.md)
* [Vanilla JS](/vanilla/docs/mcp.md)
* [Vue](/vue/docs/mcp.md)

## Available tools[​](#available-tools "Direct link to Available tools")

Each library-specific package provides tools with unique suffixes, allowing them to coexist in a flat namespace if multiple servers are connected simultaneously. Tools are named following the pattern `search_vjs_LIB>` for general documentation and `search_vjs_LIB_api` for API-specific documentation.

For instance, for React, the tools are:

* `search_vjs_react`: Search VisuallyJs React documentation.
* `search_vjs_react_api`: Search VisuallyJs React API documentation

The other library suffixes are `vue`, `svelte`, `vanilla` and, for Angular, `ng`.

## Examples[​](#examples "Direct link to Examples")

You can use the MCP to search all of the publically available docs and apidocs. At VisuallyJs we use IntelliJ's `Junie` or `AI Chat` - here's a selection of questions and responses showing the MCP in action.

### Zoom-specific content[​](#zoom-specific-content "Direct link to Zoom-specific content")

We asked our React MCP how to hide/show content based on zoom, and received this summary:

![Hide/show content MCP](https://static.visuallyjs.com/img/blog/react-use-zoom-1.png)

followed by this code snippet:

![Hide/show content MCP](https://static.visuallyjs.com/img/blog/react-use-zoom-2.png)

We can ask the same question in Angular:

![Hide/show content MCP](https://static.visuallyjs.com/img/blog/angular-zoom-signal-1.png)

![Hide/show content MCP](https://static.visuallyjs.com/img/blog/angular-zoom-signal-2.png)

### List available anchors[​](#list-available-anchors "Direct link to List available anchors")

Each of the library integrations has a dependency on `@visuallyjs/browser-ui`, which contains the core UI concepts. You can search through these - for instance, here, we're asking the React MCP about what anchor types are available:

<!-- -->

![MCP listing available anchors](https://static.visuallyjs.com/img/blog/list-anchors.png)

### Setup an Angular miniview[​](#setup-an-angular-miniview "Direct link to Setup an Angular miniview")

![Angular miniview MCP](https://static.visuallyjs.com/img/blog/angular-miniview-1.png)

![Angular miniview MCP](https://static.visuallyjs.com/img/blog/angular-miniview-2.png)

## Feedback[​](#feedback "Direct link to Feedback")

We'd be very interested to hear any feedback you may have regarding our MCP servers - head over to our [contact page](/contact.md) to find out how to get in touch.

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets
