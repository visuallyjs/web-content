# Docusaurus JSON environment loader

July 22, 2022 ·

<!-- -->

2 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

info

This post is from JsPlumb, which is now in maintenance mode. We still use this plugin in the VisuallyJs site though.

JsPlumb uses [Docusaurus](https://docusaurus.io/), a super handy static site generator, for various parts of our ecosystem, including our [Documentation](https://docs.jsplumbtoolkit.com) and also our recently released [stand alone components](https://components.jsplumbtoolkit.com) product.

While developing the site for JsPlumb Components, we wanted to include a couple of pieces of information that would vary depending on whether we were running in development mode locally (ie `docusaurus start`) or building for production. We looked into the various options available, all based on the `dotenv` plugin for Webpack, but couldn't find what we were looking for: a solution that worked, with minimal manual intervention, in both development mode and when building for production.

So we ended up building our own plugin. This plugin reads values from a JSON file and makes them available to your site via the `customFields` map in the Docusaurus `siteConfig`.

note

When I say "Docusaurus" in this post I am talking about v2/v3. I've not used v1.

<!-- -->

### Installation[​](#installation "Direct link to Installation")

```bash
npm i @jsplumb/docusaurus-plugin-env-loader-json

```

### Configuration[​](#configuration "Direct link to Configuration")

You just have to add the plugin to the list of plugins in `docusaurus.config.js`:

```javascript
plugins:[
      "@jsplumb/docusaurus-plugin-env-loader-json"
  ],

```

and then create an `env.json` file in the Docusaurus project directory.

### env.json[​](#envjson "Direct link to env.json")

Your environment variables should be keyed under a section that identifies the environment you are targetting - "development" when using `docusaurus start` and "production" when running a build. The plugin reads the environment name from the environment variable `NODE_ENV`.

```json
{
    "production":{
        "SERVER_URL":"https://some.server.com/anEndpoint"
    },
    "development":{
        "SERVER_URL":"http://localhost:4200/anEndpoint"
    }
}

```

### Accessing values[​](#accessing-values "Direct link to Accessing values")

You can access these values via the `customFields` section of the Docusaurus site config:

```javscript
import useDocusaurusContext from '@docusaurus/useDocusaurusContext';

export function MyApp {

    const {siteConfig} = useDocusaurusContext();
    const serverUrl = siteConfig.customFields.SERVER_URL

    ...

}

```

### Changing the configuration file name[​](#changing-the-configuration-file-name "Direct link to Changing the configuration file name")

If you want to specify some file other than `env.json` in your project's root, you can do so by setting the `sourceFile` option of the plugin:

```javascript
plugins:[
      [
          "@jsplumb/docusaurus-plugin-env-loader-json",
          {
              "sourceFile":"path/to/aFile.json"
          }
      ]
  ],

```

This path should be specified relative to the project root. No leading slash is required.

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets

**Tags:**

* [community](/tech-talk/tags/community.md)
* [toolkit](/tech-talk/tags/toolkit.md)
* [plugin](/tech-talk/tags/plugin.md)
* [docusaurus](/tech-talk/tags/docusaurus.md)
