# Problems with the change event on a color input in React

July 11, 2025 ·

<!-- -->

3 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

Way back in the day, HTML offered a very limited set of components for capturing input from a user. Over the years this has changed, with new controls being introduced and finding widespread support across the various browsers. One of these new-ish input types (new-ish if you've been writing webapps for 20 years or so, anyway) is the `color` input:

\#442288#442288

You can click that color bar and you'll get a popup from which you can select a new color. When you change the color, the span next to it will update to tell you what the current color is.

### Available events[​](#available-events "Direct link to Available events")

[According to MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/color) there are a couple of events you can hook into:

* **input** input is fired on the input element every time the color changes
* **change** The change event is fired when the user dismisses the color picker

In React, you'd use `onInput` or `onChange` to bind to these events.

<!-- -->

### onInput[​](#oninput "Direct link to onInput")

For some usage scenarios, like if we want to immediately respond to the change in color as the user is using the color picker, it seems the `input` event would be a good choice. We can bind to that via React's `onInput` attribute:

```jsx
export function ColorExample1() {
    const [color, setColor] = useState("#442288")

    return <div>
        <input type="color" value={color} onInput={(e) => setColor(e.target.value)}/>
        <span style={{color:color}}>{color}</span>
    </div>
} 

```

This is the code we're using in the example above.

### onChange[​](#onchange "Direct link to onChange")

But what if we only want to take action when the user has made their final choice, and dismissed the picker? Then it seems the `change` event would be a good choice. We can bind to that via React's `onChange` attribute:

```jsx
export function ColorExample2() {
    const [color, setColor] = useState("#442288")

    return <div>
        <input type="color" value={color} onChange={(e) => setColor(e.target.value)}/>
        <span style={{color:color}}>{color}</span>
    </div>
}

```

What we're expecting to see here is the the label to the right of the color picker will change **after the user has dismissed the color picker**. Try it:

\#442288#442288

But what do we actually see? The color changes immediately - the same behaviour as if we had used `onInput`. This is not the behaviour we wanted or expected.

### Binding to the change event[​](#binding-to-the-change-event "Direct link to Binding to the change event")

In order to get the behaviour we want, we have to bind to the `change` event using the bare DOM approach:

```jsx
export function ColorExample3() {

    const input = useRef(null)
    const init = useRef(false)
    const [color, setColor] = useState("#442288")

    useEffect(() => {
        if(!init.current) {
            init.current = true
            input.current.addEventListener("change", (e) => {
                setColor(e.target.value)
            })
        }
    })

    return <div>
        <input type="color" defaultValue={color} ref={input}/>
        <span style={{color: color}}>{color}</span>
    </div>

}

```

Try opening the color picker here and selecting a few colors - you'll see the color picker update, but the label to the right of the picker will not be updated until you close the picker:

\#442288#442288

### Summary[​](#summary "Direct link to Summary")

React has a very powerful event binding mechanism, but in this particular case it doesn't behave correctly. Fortunately you can always fall back to the DOM. The DOM will (almost) never let you down.

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![VisuallyJs - industry standard diagramming and rich visual UI Javascript and Typescript library](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

Fault Tree Analysis

Combines a fault tree analysis diagram with charts showing risk and list of cut sets
