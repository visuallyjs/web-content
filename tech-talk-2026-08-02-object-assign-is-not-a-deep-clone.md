# Object.assign is not a deep clone

August 2, 2026 ·

<!-- -->

3 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

The [VisuallyJs API](https://https://api.visuallyjs.com/), as with most Javascript APIs, makes extensive use of Javascript objects for configuration. A good practice to follow with inputs from the user is to make an internal copy, so as to be sure that your library is not introducing any unexpected side effects. Keep in mind that Javascript objects are passed by reference, ie:

```javascript
function doSomething(obj) {
    obj.title = "A new value."
}

const myObject = {
    title:"Initial title"
}

doSomething(myObject)

console.log(myObject.title)

=> "A new value."


```

...this is why we want to make a copy of any object we are given, because we don't know where else the user is using this JS object it passed in.

```javascript
function doSomething(obj) {
    obj = Object.assign({}, obj)
    obj.title = "A new value."
}

const myObject = {
    title:"Initial title"
}

doSomething(myObject)

console.log(myObject.title)

=> "Initial title"


```

Obviously this example is a little contrived, but hopefully you get the point. By using `Object.assign({}, obj)` to create a copy of the object we were given, we've now insulated ourselves from userland...or have we? What about if I pass in a more complex object:

<!-- -->

```javascript
function doSomething(obj) {
    obj = Object.assign({}, obj)
    obj.child.title = "A new value."
}

const myObject = {
    title:"Initial title",
    child:{
        title:"Initial child title"
    }
}

doSomething(myObject)

console.log(myObject.child.title)

=> "A new value."


```

Oh no! What's happened here? The problem is that **Object.assign is not a deep clone**.

### Cloning an object[​](#cloning-an-object "Direct link to Cloning an object")

What you should do instead of using `Object.assign` is to *clone* the object. Most browsers have offered a `structuredClone` method on the window since about 2022, so an approach like this is widely supported:

```javascript
function doSomething(obj) {
    obj = structuredClone(obj)
    obj.child.title = "A new value."
}

const myObject = {
    title:"Initial title",
    child:{
        title:"Initial child title"
    }
}

doSomething(myObject)

console.log(myObject.child.title)

=> "Initial child title"


```

### core-js Polyfill[​](#core-js-polyfill "Direct link to core-js Polyfill")

If the fact that it's not guaranteed that your users have a browser supporting `structuredClone` is a concern, you could use a [polyfill from core-js](https://github.com/zloirock/core-js#structuredclone).

### Clone example code[​](#clone-example-code "Direct link to Clone example code")

If you don't want to use a polyfill from core-js, feel free to grab this code instead:

```javascript

function clone(a) {
    if (a == null) {
        return null
    } else if (typeof a === "string") {
        // string
        return "" + a
    } else if (typeof a === "boolean") {
        // boolean
        return !!a
    } else if (Object.prototype.toString.call(a) === "[object Date]") {
        // Date
        return new Date(a.getTime())
    } else if (Object.prototype.toString.call(a) === "[object Function]") {
        // Function (not cloned; returned as-is)
        return a
    } else if (Array.isArray(a)) {
        // Array - create new array and clone entries from existing array        
        return a.map(e => clone(e))        
    } else if (Object.prototype.toString.call(a).match(/\[object .*Element]/) != null) {
        // DOM Element (not cloned; returned as-is)
        return a
    } else if (Object.prototype.toString.call(a) === "[object Text]") {
        // DOM Text Node (not cloned; returned as-is)
        return a 
    } else if (Object.prototype.toString.call(a) === "[object Object]") {
        // JS Object
        const c = {}
        for (let j in a) {
            c[j] = clone(a[j])
        }
        return c
    }
    else {
        return a
    }
}

```

### Read more[​](#read-more "Direct link to Read more")

* Read about `structuredClone` [on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/structuredClone)

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets
