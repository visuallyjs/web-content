# How we improved our apidocs with Typedoc groups and categories

March 19, 2025 ·

<!-- -->

10 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

info

This post is from JsPlumb, which is now in maintenance mode. To see the VisuallyJs apidocs, visit [this page](https://api.visuallyjs.com)

JsPlumb uses the excellent [Typedoc](https://typedoc.org/) documentation generator to create [our API documentation](https://apidocs.jsplumbtoolkit.com/7.0.0/), but since we adopted it last year we haven't really made the most of it. We would run Typedoc over our codebase with the default settings, and the result is a page in which everything is listed alphabetically, grouped by `Enumerations` `Classes`, `Interfaces`, etc.

It can be a useful page - if you know what you're looking for. But it doesn't lend itself very well to browsing, and browseable docs are great, because they lead to discovery.

The last 6.x release API docs page looks like this:

<!-- -->

![Apidocs index page for JsPlumb 6.81.0 - VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](/assets/images/release-6-81-0-apidocs-1fcf090d5970819a6be35959549d65c5.png)

For release 7.x we wanted to spruce up these API docs and make them more useful, so we started looking through the Typedoc documentation, and came across `groups` and `categories`.

## Groups[​](#groups "Direct link to Groups")

By default, Typedoc classifies the things it finds in a Typescript codebase according to their Typescript kind - `Class` , `Interface`, `Type Alias`, etc. With this module, for example:

```typescript
/**
    This is Foo
*/
export const Foo = "FOO"

/**
    This is Bar
*/
export const Foo = "FOO"

/**
* This is Foo or Bar
*/
export type FooOrBar = typeof FOO | typeof BAR

/**
* This is some class.
*/
export class MyClass {

    /**
    * This method handles a Foo or a Bar.
    * @param v
    */
    handleFooOrBar(v:FooOrBar):void {
        ...
    }
}

```

Typedoc would write out an index page listing the variables `Foo` and `Bar`, the class `MyClass` and the type alias `FooOrBar`, which is all true, but what it does not convey to the user is the larger context, and this is what we felt was lacking from the JsPlumb API docs. What are `Foo` and `Bar` actually *for*? What *sort* of class is `MyClass`?

As a simple example, in JsPlumb we have a constant representing a click event on a canvas:

```typescript
/**
* Event fired when a user clicks on the surface canvas.
*/
export const EVENT_CANVAS_CLICK = "canvasClick"

```

which would be listed as a variable in the default output. But in JsPlumb it's more than a variable - it's a variable representing an event, and if I'm a JsPlumb user and I'm interested in what events get fired, it would be helpful for me to find it via that context. Enter the `@group` tag:

```typescript
/**
* Event fired when a user clicks on the surface canvas.
* @group Events
*/
export const EVENT_CANVAS_CLICK = "canvasClick"

```

Now `EVENT_CANVAS_CLICK` is marked as belonging to the `Events` group, which gets an entry in the index page:

![Events group listed in index - When you've reached the limits with SvelteFlow, VisuallyJs has what you need](/assets/images/events-group-listing-c9a81297c8c8fc88957ff46f9ebcf3e8.png)

We've gone through the JsPlumb codebase and added groups to *everything*. Another great example of how classifying things with groups and categories is useful is with CSS classes. JsPlumb exposes a great number of CSS classes, making it very easy for you to skin your app and to achieve some nice UI effects, but previously we haven't had this list of classes particularly well organised - in the API docs they would just show as "constants", and in the main documentation we had a constant task of trying to ensure our class lists there were up to date (more on this [below](#Using-the-generated-JSON)).

For instance, here are a couple of classes that the surface adds to edges that it has painted:

```javascript
/**
 * Assigned to the SVG element that is the parent of the path element used to draw an edge. A common setup using this class is to assign it a z-index which is lower than the z-index set for `.jtk-node` and `.jtk-group`. You can target the path element directly using `.jtk-connector path`, for instance for setting a `stroke-width` or `stroke`
 * @group CSS Classes
 * @category Edges
 */
export const CLASS_CONNECTOR = "jtk-connector"

/**
 * Assigned to the SVG path element used to draw an edge's outline.
 * @group CSS Classes
 * @category Edges
 */
export const CLASS_CONNECTOR_OUTLINE = "jtk-connector-outline"

```

Where previously we did not have `@group` and `@category` set for these, they'd just appear in a big long list of constants. In our 7.x apidocs, though, you can find them conveniently classified like this;

![CSS classes classified by group and category - When you've reached the limits with SvelteFlow, VisuallyJs has what you need](/assets/images/css-by-group-and-category-7d2c2972a47098cfeabf85fba69ba8cd.png)

When you click through to one of these you'll get the value you can use in your CSS, and a discussion of its use:

![CSS classes classified by group and category - When you've reached the limits with SvelteFlow, VisuallyJs has what you need](/assets/images/css-definition-f33c134583abe4ce0bfb332f2ef4eef5.png)

As an aside, this ability to easily custom JsPlumb using CSS is one of JsPlumb's many strengths, and not one which is easily achieved with a library that was originally designed for diagramming and is restricted to SVG or canvas for output.

### Configuring the output for groups[​](#configuring-the-output-for-groups "Direct link to Configuring the output for groups")

One important point to note is that in order to see your groups like this, you need to instruct Typedoc to `includeGroups` in the config file:

```json
{
  "navigation": {
    "includeGroups": true
  }
}

```

For a discussion, see the [Typedoc pages](https://typedoc.org/documents/Options.Output.html).

## Categories[​](#categories "Direct link to Categories")

As we were deciding on the groups we wanted we realised that in some cases we'd like to be able to break up a group into more granular parts. For instance, `EVENT_CANVAS_CLICK` is an event which is fired by the surface component in the UI. It's an event, yes, but also it's a *UI event*. JsPlumb fires many events from its model that are UI agnostic, and we'd like to be able to separate these concepts in the docs. For that, we decided to use `@category`:

```typescript
/**
* Event fired when a user clicks on the surface canvas.
* @group Events
* @category UI Events
*/
export const EVENT_CANVAS_CLICK = "canvasClick"

```

We now have nested menus on our index page:

![Events group and categories listed in index - When you've reached the limits with SvelteFlow, VisuallyJs has what you need](/assets/images/events-group-and-category-listing-7c1f66ea09b7fb62fc9eb73d2a1825ae.png)

### Configuring the output for categories[​](#configuring-the-output-for-categories "Direct link to Configuring the output for categories")

As with groups, to get this nesting of group/category, you need to instruct Typedoc to `includeCategories` in the config file:

```json
{
  "navigation": {
    "includeGroups": true,
    "includeCategories": true
  }
}

```

## Using the generated JSON[​](#using-the-generated-json "Direct link to Using the generated JSON")

One other benefit of adding `@group` and `@category` tags to our code has been that we can now ingest Typedoc's generated JSON in our regular docs, making for one less thing we have to keep up to date. Above we showed you an example of how we've applied `@group` and `@category` to our CSS class constants, and we mentioned that previously we'd have to manually ensure that our main documentation was up to date with the current list of CSS classes. If something was added or removed, or a description was updated, that would be a manual task for us to execute in the main documentation project.

Typedoc, by default, writes out HTML. But it can also write out JSON (or both - see the [Typedoc documentation](https://typedoc.org/documents/Options.Output.html) for details), and that JSON contains all of the reflection data Typedoc has found, and that's extremely useful.

In our main documentation project (which is, like this site, a Docusaurus app, ie React) we've written a few simple components that can load definitions from the Typedoc JSON, and using these we can now be confident that our main documentation is entirely up to date with the state of the code, with no manual intervention required. This is a big win for us.

For example, we list all of the CSS classes exposed by the JsPlumb on this page - <https://docs.jsplumbtoolkit.com/toolkit/7.x/lib/css>, organised by `@group`. Here's what the `Edges` group looks like:

![Edge CSS classes - VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](/assets/images/css-class-table-cd9350ed1fe0fb20a0d7ecf826d99808.png)

Does this look familiar? That's because it's the output from Typedoc arranged into a table.

### CSS table component[​](#css-table-component "Direct link to CSS table component")

Achieving this was pretty straightforward, and given the amount of time we've spent keeping those docs up to date we're kind of kicking ourselves we didn't dedicate any time into this before. The Typedoc JSON exposes all of the groups it found in `groups` array which is a child of its root. Each entry in that array has a `title`, a list of `children`, and also - when you use categories - a list of `categories`:

```json

{
  "groups": [
    {
      "title": "CSS Classes",
      "description": [
        {
          "kind": "text",
          "text": "List of CSS classes assigned to DOM elements by various parts of JsPlumb's UI."
        }
      ],
      "children": [
        11793,
        11794,
        11806,
        ...
      ],
      "categories": [
        {
          "title": "Edges",
          "children": [
            11793,
            11794,
            11806,
            11805,
            346
          ]
        }
      ]
    }
  ]
}


```

So we can find our `CSS Classes` group inside the JSON like this:

```javascript

import BrowserUI from "../src/apidocs/browser-ui"    // this is the Typedoc JSON file

const cssClasses = BrowserUI.groups.find(c => c.title==="CSS Classes")


```

and inside of that we can get our `Edges` category like this:

```javascript
const edgeClasses = cssClasses.categories.find(c => c.title.toLowerCase() === "edges")

```

we actually have a couple of helper functions for these operations:

```javascript
/**
 * Load a group definition from the api
 * @param api API json
 * @param id ID = actually the title - of the group to retrieve.
 */
export function getGroup(api, id) {
    return api.groups.find(c => c.title===id)
}

/**
 * Load a category from the given group
 * @param group Group to load from
 * @param id ID = actually the title - of the category to retrieve.
 */
export function getCategory(group, id) {
    return group.categories.find(c => c.title.toLowerCase() === id.toLowerCase())
}

```

So we're going to use these two functions to load the `CSS Classes` group and then load the `Edges` category from it:

```javascript
import BrowserUI from "../src/apidocs/browser-ui"    // this is the Typedoc JSON file

const cssClasses = getGroup(BrowserUI, "CSS Classes")
const category = getCategory(cssClasses, id)

```

Recall from the JSON above that the category we just retrieved looks like this:

```json
{
  "title": "Edges",
  "children": [
    11793,
    11794,
    11806,
    11805,
    346
  ]
}

```

...it's got the category title and then a list of child pointers. Each of these children can be retrieved from the `children` element inside the API JSON root. Again we have a helper function - `findClasses` - to resolve these pointers:

```javascript
function findClasses(api, category) {
    return category.children.map(c => findClass(api, c))
}

```

The `findClass` function is key here - it looks inside the API JSON's `children` element for matches, but the important thing to note is the `kind` match: Typedoc assigns a `kind` to everything internally, and 32 is the kind for a constant.

```javascript
function findClass(api, id) {
    return api.children.find(c => c.id === id && c.kind === 32)
}

```

So - we've now got a few helper functions to pull out arbitrary information from the API JSON. Our final React component looks like this:

```jsx
import React from "react"

import BrowserUI from "../src/apidocs/browser-ui"    // this is the Typedoc JSON file

export function ClassTable({id}) {

  const cssClasses = getGroup(BrowserUI, "CSS Classes")
  const category = getCategory(cssClasses, id)
  const defs = findClasses(BrowserUI, category)

   return <table className="jtk-docs-props">
            <thead>
              <tr>
                <th>Class</th>
                <th>Description</th>
              </tr>
            </thead>
            <tbody>
              { defs.map(def => renderClass(def))}
            </tbody>
          </table>
}


```

## Summary[​](#summary "Direct link to Summary")

Taking the time to go through what Typedoc offers has been a big win for us - we've managed to streamline our documentation process, and to reduce the amount of manual churn or risk of stale information. We see this update as the first step in an ongoing process of trying to automate as much as possible of our documentation generation. As we make further changes we'll keep you updated via this blog.

We actually have a bunch of other tags based around the Typedoc JSON that we use in our documentation - for instance, we can inject the spec for an interface or type, and we can do that in a type-safe way, as it will break during the build if we try to reference something that does not exist. If you're interested in hearing more about these tags, drop us a line at <hello@visuallyjs.com>, we'd be happy to discuss.

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets

**Tags:**

* [typescript](/tech-talk/tags/typescript.md)
* [javascript](/tech-talk/tags/javascript.md)
* [class](/tech-talk/tags/class.md)
* [interface](/tech-talk/tags/interface.md)
* [inheritance](/tech-talk/tags/inheritance.md)
* [typedoc](/tech-talk/tags/typedoc.md)
* [apidocs](/tech-talk/tags/apidocs.md)
* [docusaurus](/tech-talk/tags/docusaurus.md)
