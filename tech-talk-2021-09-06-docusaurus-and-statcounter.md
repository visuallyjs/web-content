# Statcounter plugin for Docusaurus

September 6, 2021 ·

<!-- -->

5 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

info

This post is from JsPlumb, which is now in maintenance mode. We still use StatCounter in VisuallyJs, though.

JsPlumb uses [Statcounter](https://statcounter.com) to keep track of what pages in the documentation people are looking at. Recently, at the tail end of the work to migrate to Typescript and release version 5.x of the Community and Toolkit editions, we started using [Docusaurus](https://docusaurus.io/), a super handy static site generator that not only runs on React but has React baked right into it, allowing us to easily [embed working demonstrations](https://docs.jsplumbtoolkit.com/community/lib/anchors#anchor-offsets) throughout our docs, or to embed snippets from the api documentation directly into the main documentation via React components. It's a really handy tool, and if you're looking for a static site generator I recommend giving it a look.

note

When I say "Docusaurus" in this post I am talking about v2. I've not used v1.

<!-- -->

This is not a post about how great Docusaurus is, though. This is a quick post about a Statcounter plugin we wrote while working on the jsPlumb API documentation. Docusaurus ships with a plugin for Google Analytics, allowing you to quickly add support for GA to all the pages on your site, but jsPlumb doesn't use Google Analytics. Statcounter's interface has a pleasing directness to it and gives us all the information we need. A quick look around the internets came up blank on existing Docusaurus/Statcounter integrations, so we wrote a plugin.

### Installation[​](#installation "Direct link to Installation")

```bash
npm i @jsplumb/docusaurus-plugin-statcounter

```

### Configuration[​](#configuration "Direct link to Configuration")

First you have to add the plugin to the list of plugins in `docusaurus.config.js`:

```javascript
plugins:[
      "@jsplumb/docusaurus-plugin-statcounter"
  ],

```

Then you need to configure the plugin via a `statCounter` block in the `themeConfig` of your `docusaurus.config.js`. It takes two arguments, both required:

```javascript
themeConfig: {
    statCounter:{
      projectId: "2222222",
      securityCode: "2222222"
    },
    ...
}

```

`projectId` and `securityCode` are available in the Statcounter console for the project you wish to target.

### Internals[​](#internals "Direct link to Internals")

This is the first plugin I've written for Docusaurus and it doesn't have the most complex requirements, but I was quite impressed with the plugin mechanism. Let's start with the `package.json`:

```json
{
  "main": "src/index.js",
  "name": "@jsplumb/docusaurus-plugin-statcounter",
  "version": "1.0.0"
}

```

We deliver a basic package with a single entry point.

#### Bootstrap[​](#bootstrap "Direct link to Bootstrap")

Let's take a look at the first few lines of `index.js`:

```javascript

const path = require('path');

module.exports = function (context) {
  
  const {siteConfig} = context;
  const {themeConfig} = siteConfig;
  const {statCounter} = themeConfig || {};
  
  
};

```

Our module exports a single function that takes a `context` object, inside of which we can extract the `siteConfig`, and, from that, the `themeConfig`, which contains our `statCounter` settings.

Once we have our `statCounter` object, we extract the things we need from it, and complain about stuff that is missing:

```javascript
const {projectId, securityCode} = statCounter;

if (!projectId) {
    throw new Error(`The statcounter plugin requires a "projectId" to be set`)
}

if (!securityCode) {
    throw new Error(`The statcounter plugin requires a "securityCode" to be set`)
}

```

#### Linking with Statcounter[​](#linking-with-statcounter "Direct link to Linking with Statcounter")

Statcounter works by importing a JS file in your document's head, after setting a couple of global variables. Docusaurus makes this very easy for us - all we have to do is declare an `injectHtmlTags()` method in our plugin:

```javascript
return {
    name: 'docusaurus-plugin-statcounter',

    getClientModules() {
      return [path.resolve(__dirname, './statcounter')]
    },

    injectHtmlTags() {

      return {
        headTags:[
          {
              tagName:'script',
              innerHTML: `
                var sc_project="${projectId}"; 
                var sc_invisible=1; 
                var sc_security="${securityCode}";
              `
          },
          {
            tagName:'script',
            attributes:{
              src:"https://www.statcounter.com/counter/counter.js"
            }
          }
        ]
      }
    }
  };

```

We inject two tags into the head: first we inject a `script` element and provide its `innerHTML` - this sets up the global variables. Next, we inject another `script`, but this time we set its `src` attribute, so it loads the JS from Statcounter's site. Documentation for `injectHtmlTags(..)` can be found [here](https://docusaurus.io/docs/lifecycle-apis#injecthtmltags).

#### Tracking page changes[​](#tracking-page-changes "Direct link to Tracking page changes")

Given that Docusaurus is an SPA, pages get swapped in and out without new page loads, and Statcounter would be oblivious, were we not to advise it. Fortunately this was also straightforward. Note this block in our plugin's code:

```javascript
getClientModules() {
  return [path.resolve(__dirname, './statcounter')]
}

```

This [instructs Docusaurus](https://docusaurus.io/docs/lifecycle-apis#getclientmodules) to load the module found in `./statcounter.js`. The source code for that file looks like this:

```javascript
import ExecutionEnvironment from '@docusaurus/ExecutionEnvironment';

export default (function () {
  if (!ExecutionEnvironment.canUseDOM) {
    return null;
  }

  return {
    onRouteUpdate({location}) {
      _statcounter.record_pageview()
    },
  };
})();

```

This module hooks into `onRouteUpdate`, which I think is [perhaps undocumented](https://github.com/facebook/docusaurus/issues/3399) (for inspiration on this bit I used the Google Analytics plugin).

When a route update event occurs, we call `_statcounter.record_pageview()`. `_statcounter` is an object in the global space that was added by Statcounter's JS.

### Conclusion[​](#conclusion "Direct link to Conclusion")

That's the whole plugin - perhaps 80 lines of code. Very straightforward - it took me about half an hour to write and deploy. Injecting HTML tags is not the only thing you can do with a Docusaurus plugin, though. Take a look through [the lifecycle APIs](https://docusaurus.io/docs/lifecycle-apis) to get a feel for what's possible.

If you want to follow up on this, the source is [on Github at https://github.com/jsplumb/docusaurus-plugin-statcounter](https://github.com/jsplumb/docusaurus-plugin-statcounter).

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

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
