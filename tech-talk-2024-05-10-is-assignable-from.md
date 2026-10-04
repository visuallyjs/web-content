# Testing class compatibility with isAssignableFrom

May 10, 2024 ·

<!-- -->

4 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

info

This post is from JsPlumb, which is now in maintenance mode. We still use this code in VisuallyJs though.

Classes are a controversial topic in the Javascript/Typescript world. Are they a terrible idea? Are they really useful, when used sensibly? This post will make no attempt at answering either of these questions. This post is about a niche method that I first encountered many years ago in the world of Java - `isAssignableFrom` - and how you can go about writing it for use in Typescript/Javascript.

### What does it do?[​](#what-does-it-do "Direct link to What does it do?")

This is what the Javadocs have to say about it:

So, given some class, you can use `isAssignableFrom` to figure out whether that class is a subclass of some other class.

### Why would I need this?[​](#why-would-i-need-this "Direct link to Why would I need this?")

If you're thinking it's a bit niche, yes, I agree. `isAssignableFrom` is one of those methods you don't use much. But when you need it, you need it.

<!-- -->

JsPlumb offers the concept of [Decorators](https://docs.jsplumbtoolkit.com/toolkit/6.x/lib/decorators) - a class that can add arbitrary extra content to the UI after a layout has been run. These can be used for a great variety of things, and if you're a JsPlumb user but haven't yet come across them, we'd encourage you to check them out.

You can register a decorator on JsPlumb using one of two different syntaxes - you can create an extension of `Decorator` and register it:

```javascript
import { Decorator, Decorators, DecorateParams, DecorateResetParams } from "@jsplumbtoolkit/browser-ui"

class MyDecorator extends Decorator {

    decorate(params: DecorateParams): void {
        ...
    }
    
    reset(params: DecorateResetParams): void {
    
    }
}

Decorators.register("MY_DECORATOR", MyDecorator)


```

...or you can just register an function whose shape fits the bill (specifically, it matches the `IDecorator` interface):

```javascript
import { Decorators, DecorateParams, DecorateResetParams } from "@jsplumbtoolkit/browser-ui"


Decorators.register("MY_DECORATOR", function() {
    
    this.decorate = (params: DecorateParams): void  => {
        ...
    }
        
    this.reset = (params: DecorateResetParams): void => {
        
    } 
})


```

The `register` method has this signature:

```javascript
register:(name:string, dec:Constructable<Decorator>)

```

info

`Constructable<Decorator>` means "a function which, when invoked with `new...`, will return an instance of Decorator.". We use this interface in a few places in the JsPlumb code.

```javascript
export type Constructable<T> = { new(...args: any[]): T }

```

So the question is, how does `register` know what was passed in? Was it given a `Decorator`, or was it given some other function? `isAssignableFrom` to the rescue!

```javascript

const decoratorMap:Record<string, Constructable<Decorator>> = {}

register:(name:string, dec:Constructable<Decorator>) => {

    if (isAssignableFrom(dec, Decorator)) {
        decoratorMap[name] = dec
    } else {
        decoratorMap[name] = functionalDecorator(dec)
    }
}

```

The `register` method determines whether or not it's been given a Decorator and just stashes it if so. Otherwise it uses the helper method `functionalDecorator` to wrap what it was given (the details of that method are orthogonal to this discussion).

How does it work then?

### Show Me The Code[​](#show-me-the-code "Direct link to Show Me The Code")

It's a simple method:

```typescript
export function isAssignableFrom(object:any, cls:any) {
    let proto = object.prototype
    while (proto != null) {
        if (proto instanceof cls) {
            return true
        }
        proto = proto.prototype
    }
    return false
}

```

It basically walks the prototype chain and tests each prototype via an `instanceof` test.

### Isn't this just instanceof?[​](#isnt-this-just-instanceof "Direct link to Isn't this just instanceof?")

No! It may seem like it is, but the key here is that comparison is being made on a **class**, not on an object. We want to know when someone has passed a reference to a class into `register`.

Consider this console session:

```javascript

class Foo {}
class Bar extends Foo {}

const bar = new Bar()

bar instanceof Bar
//  --> true

bar instanceof Foo
// --> true


```

So far, so good: our instance of `Bar`, which is a subclass of `Foo`, is recognised as being both an instance of `Foo` and of `Bar`. But how about this:

```javascript
Bar instanceof Foo
// --> false

```

which makes sense really, because `Bar` is not an instance of *anything* - it's a class.

If we want to check whether we can consider `Bar` as `Foo` we're going to need our `isAssignableFrom` function:

```javascript
isAssignableFrom(Bar, Foo)
// --> true

```

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets

**Tags:**

* [typescript](/tech-talk/tags/typescript.md)
* [java](/tech-talk/tags/java.md)
* [class](/tech-talk/tags/class.md)
* [interface](/tech-talk/tags/interface.md)
* [inheritance](/tech-talk/tags/inheritance.md)
