# Maximising the data-ink ratio in a World Cup visualization

August 3, 2026 ·

<!-- -->

3 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

Many years ago a manager of mine introduced me to a fantastic book about data visualization, entitled **The Visual Display of Quantitative Information**, by Edward Tufte:

![The Visual Display of Quantitative Information](/img/tech-talk/vdqi.png)

You should go to a bookstore and buy this book, it's great.

One of the core concepts in this book is that of the "data-ink" ratio - the amount of ink used to represent data vs the total amount of ink used to draw the entire image. There are many examples of this throughout the book, and it's a concept that has stuck with me.

### FIFA World Cup[​](#fifa-world-cup "Direct link to FIFA World Cup")

We recently dusted off our [FIFA World Cup Visualizer](/demonstrations/fifaworldcup.md) and released it as an app that people can use in their sites. In this app we're particularly pleased with the group stage visualization, because we think it has a satisfying data-ink ratio:

![World cup group stage](https://static.visuallyjs.com/img/blog/world-cup-group-stage.png)

For a given team in the group stage, this visualization lets the user track 10 discrete pieces of information:

<!-- -->

#### Stats table[​](#stats-table "Direct link to Stats table")

In the stats table the user can view:

* The number of wins
* The number of draws
* The number of losses
* The total goals scored by the team
* The total goals scored against the team
* The points scored by the team

#### Border color[​](#border-color "Direct link to Border color")

The team's ranking in the group is encoded by the border color:

* Dark green - 1st place
* Light green - 2nd place
* Orange - 3rd place
* Red - 4th place

#### Edges[​](#edges "Direct link to Edges")

The edges linked to each team represent the matches the team has played, and they contain the score for each match. The user can see all of the matches played and the individual scores.

***

### Summary[​](#summary "Direct link to Summary")

At a glance, a user can absorb every piece of information about the group stage they need to, in a single place. We're quite pleased with this visualization. Got any comments? Drop us a line via the [contact page](/contact.md) - we love to chat about this sort of stuff.

In a future post we're going to look at some other ways in which VisuallyJs can be used to create innovative views on a dataset, including a really nifty flight booking component.

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets

***

**Tags:**

* [typescript](/tech-talk/tags/typescript.md)
* [javascript](/tech-talk/tags/javascript.md)
* [class](/tech-talk/tags/class.md)
* [interface](/tech-talk/tags/interface.md)
* [inheritance](/tech-talk/tags/inheritance.md)
* [tufte](/tech-talk/tags/tufte.md)
* [data-ink](/tech-talk/tags/data-ink.md)
* [visualization](/tech-talk/tags/visualization.md)
* [fifa](/tech-talk/tags/fifa.md)
