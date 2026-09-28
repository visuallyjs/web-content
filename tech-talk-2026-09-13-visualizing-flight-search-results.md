# Visualizing flight search results with charts

September 13, 2026 ·

<!-- -->

7 min read

[![Simon Porritt](https://avatars.githubusercontent.com/u/262720?s=60\&v=4)](https://github.com/sporritt)

[Simon Porritt](https://github.com/sporritt)

VisuallyJs Development

![Flight search bubble chart](https://static.visuallyjs.com/img/blog/flight-search/scatter-chart-results-no-border.png)

In a previous post I mentioned a book that introduced to me the concept of the "data-ink" ratio - the amount of ink used to represent data vs the total amount of ink used to draw the entire image. At that time I was working for a travel company, and I was so enamoured with this book that I instantly went off and started designing prototypes for alternative ways we could present our users with the results of their searches.

None of my ideas were adopted: I couldn't find a champion amongst the middle managers. But that didn't make me think they were no good. One of my favourites was what I'm going to talk about today - flight search results using a scatter chart.

## Searching for flights[​](#searching-for-flights "Direct link to Searching for flights")

When I search for a flight I most often have:

* a general idea of when I want to depart
* a budget
* a personal list of airline preferences
* a preference for getting there quickly, but
* an aversion to flights longer than 15 hours

<!-- -->

So I go to a booking engine and enter my details on the form, and I get a list of flights. I now have to go through this list of flights comparing them all to decide which one I want to book.

OriginLondon

DestinationSydney

Departure Date2026-11-28

Departure TimeAny time (12pm) (any)

Passengers1

Range (+/- days)1

Search

Sort by:Price: Low to High (price-asc)

### HorizonSkyway

Refundable1

<!-- -->

<!-- -->

bag

11:33 AM

London

1 stop

07:08 AM

Sydney

19h 35m

16993

<!-- -->

km

Nov 11

$

<!-- -->

561

### Emerald Express

Refundable1

<!-- -->

<!-- -->

bag

06:15 PM

London

1 stop

01:22 PM

Sydney

19h 7m

16993

<!-- -->

km

Nov 12

$

<!-- -->

674

### Swift Lines

Non-refundable1

<!-- -->

<!-- -->

bag

12:25 PM

London

2 stops

12:00 PM

Sydney

23h 35m

16993

<!-- -->

km

Nov 12

$

<!-- -->

685

### North Orbit

Refundable2

<!-- -->

<!-- -->

bags

03:44 PM

London

1 stop

12:23 PM

Sydney

20h 39m

16993

<!-- -->

km

Nov 12

$

<!-- -->

988

### Royal Express

Non-refundable1

<!-- -->

<!-- -->

bag

10:01 AM

London

1 stop

07:20 AM

Sydney

21h 19m

16993

<!-- -->

km

Nov 12

$

<!-- -->

1108

### North Orbit

Non-refundable1

<!-- -->

<!-- -->

bag

04:59 PM

London

1 stop

09:29 PM

Sydney

17h 30m

16993

<!-- -->

km

Nov 13

$

<!-- -->

1115

### Alpine Ways

Non-refundable2

<!-- -->

<!-- -->

bags

05:17 PM

London

1 stop

11:47 PM

Sydney

19h 30m

16993

<!-- -->

km

Nov 13

$

<!-- -->

1209

### Alpine Ways

Refundable2

<!-- -->

<!-- -->

bags

10:13 AM

London

1 stop

08:43 AM

Sydney

22h 30m

16993

<!-- -->

km

Nov 11

$

<!-- -->

1220

### Royal Express

Non-refundable2

<!-- -->

<!-- -->

bags

05:29 PM

London

2 stops

02:34 PM

Sydney

21h 5m

16993

<!-- -->

km

Nov 12

$

<!-- -->

1271

### BlueFly

Refundable1

<!-- -->

<!-- -->

bag

04:13 PM

London

2 stops

01:55 PM

Sydney

21h 42m

16993

<!-- -->

km

Nov 12

$

<!-- -->

1533

### Emerald Express

Non-refundable2

<!-- -->

<!-- -->

bags

02:41 PM

London

1 stop

01:04 PM

Sydney

22h 23m

16993

<!-- -->

km

Nov 12

$

<!-- -->

1628

### Emerald Express

Refundable1

<!-- -->

<!-- -->

bag

06:28 AM

London

1 stop

02:06 AM

Sydney

19h 38m

16993

<!-- -->

km

Nov 12

$

<!-- -->

1665

### Blue Air

Refundable2

<!-- -->

<!-- -->

bags

02:26 PM

London

1 stop

11:05 AM

Sydney

20h 39m

16993

<!-- -->

km

Nov 13

$

<!-- -->

1738

### Swift Lines

Refundable2

<!-- -->

<!-- -->

bags

04:03 PM

London

1 stop

01:47 PM

Sydney

21h 44m

16993

<!-- -->

km

Nov 13

$

<!-- -->

1763

### NorthWings

Refundable2

<!-- -->

<!-- -->

bags

05:40 PM

London

2 stops

04:31 PM

Sydney

22h 51m

16993

<!-- -->

km

Nov 13

$

<!-- -->

1835

### NorthWings

Refundable2

<!-- -->

<!-- -->

bags

05:19 PM

London

1 stop

12:19 PM

Sydney

18h 60m

16993

<!-- -->

km

Nov 12

$

<!-- -->

2001

### Royal Express

Refundable1

<!-- -->

<!-- -->

bag

05:07 PM

London

1 stop

01:58 PM

Sydney

20h 51m

16993

<!-- -->

km

Nov 11

$

<!-- -->

2010

### Swift Lines

Refundable2

<!-- -->

<!-- -->

bags

06:48 AM

London

1 stop

05:05 AM

Sydney

22h 17m

16993

<!-- -->

km

Nov 12

$

<!-- -->

2067

### Horizon Orbit

Non-refundable1

<!-- -->

<!-- -->

bag

09:58 AM

London

1 stop

07:29 AM

Sydney

21h 31m

16993

<!-- -->

km

Nov 13

$

<!-- -->

2072

### HorizonSkyway

Non-refundable1

<!-- -->

<!-- -->

bag

03:59 PM

London

2 stops

03:13 PM

Sydney

23h 14m

16993

<!-- -->

km

Nov 13

$

<!-- -->

2098

### Swift Lines

Non-refundable1

<!-- -->

<!-- -->

bag

03:58 PM

London

1 stop

01:09 PM

Sydney

21h 11m

16993

<!-- -->

km

Nov 11

$

<!-- -->

2207

### Swift Lines

Non-refundable2

<!-- -->

<!-- -->

bags

12:36 PM

London

2 stops

10:49 AM

Sydney

22h 13m

16993

<!-- -->

km

Nov 11

$

<!-- -->

2255

### NorthWings

Refundable1

<!-- -->

<!-- -->

bag

07:27 AM

London

1 stop

04:29 AM

Sydney

21h 2m

16993

<!-- -->

km

Nov 13

$

<!-- -->

2255

### Horizon Orbit

Refundable1

<!-- -->

<!-- -->

bag

01:54 PM

London

1 stop

10:35 AM

Sydney

20h 41m

16993

<!-- -->

km

Nov 11

$

<!-- -->

2313

### Blue Air

Non-refundable1

<!-- -->

<!-- -->

bag

06:31 AM

London

1 stop

04:09 AM

Sydney

21h 38m

16993

<!-- -->

km

Nov 13

$

<!-- -->

2350

### Swift Lines

Refundable2

<!-- -->

<!-- -->

bags

12:36 PM

London

1 stop

08:15 AM

Sydney

19h 39m

16993

<!-- -->

km

Nov 11

$

<!-- -->

2379

### Alpine Ways

Refundable1

<!-- -->

<!-- -->

bag

09:01 AM

London

1 stop

06:49 AM

Sydney

21h 48m

16993

<!-- -->

km

Nov 11

$

<!-- -->

2449

### North Orbit

Refundable1

<!-- -->

<!-- -->

bag

06:42 PM

London

1 stop

02:57 PM

Sydney

20h 15m

16993

<!-- -->

km

Nov 13

$

<!-- -->

2474

Making my choice from this list of flights is not just a question of which one is the cheapest - I have a list of criteria above that I want to apply to this decision, and being presented with a list, even if it has sorting functionality, still makes the task quite onerous.

## Scatter chart results[​](#scatter-chart-results "Direct link to Scatter chart results")

What if, instead, I could view this list of flights in a way that I could determine several facts at once? Enter the scatter chart.

In this view we show the price for each flight along the X axis, and the duration of the flight on the Y axis. Since I want the cheapest and quickest flight, I'm going to be looking for the one that is closest to the bottom left corner:

...and in this dataset there are two candidates - a Horizon Skyway flight for $561 that takes 19h 35m, and an Emerald Express flight for $674, taking 19 hours and 7 minutes. But what's that North Orbit flight at the bottom there? It's a little more expensive, but I can see it's only 17h 30m. This is a business flight...hang the expense, I'll take it. That was the sixth result in my flight list - but with the scatter chart view I was able to immediately see it was the one I wanted.

### Picking different criteria[​](#picking-different-criteria "Direct link to Picking different criteria")

We can choose a different value to plot on the y axis if we want to - here's a view where the Y axis plots how far away from my ideal departure time each flight departs:

Y-Axis:Departure Variance (departureVariance)

You can use the drop down to switch the y axis field.

### Adding extra dimensions[​](#adding-extra-dimensions "Direct link to Adding extra dimensions")

You may or may not have noticed, but the drop down contains a **Baggage Allowance** option - that's one of the fields stored for each flight. We can assign this to the Y axis if we want, but it doesn't give us the best result:

Aside from the fact that all of the flights are arranged in two lines (due to the fact that the flights in the dataset offer either one checked bag or two), the chart also suggests that there could be such a thing as "1.5 bags". We could fix that last issue by specifying our own labels, or specifying that the label step should be 1, but that would be to ignore the fact that baggage allowance does not really make sense for the Y axis. It would be great to show the user, though - so an alternative approach is to add this piece of knowledge to the markers in the scatter chart. We'll use the marker's outline for this - red means 1 bag, green means 2 bags:

Oh no! I've just discovered that the North Orbit flight I wanted to book only allows one checked bag. Maybe I should go for one of the others after all? Hmm no, the cheaper flights are one bag only too. Maybe I should look at that Alpine Ways flight that's reasonably short and not much more expensive? With this scatter chart view I can assess all of my options quickly and easily.

## ~~Polishing~~[​](#polishing "Direct link to polishing")

info

This section was in our original article, which we posted on Reddit. We then had an interesting discussion with `@s4074433` on the nature of the data/ink ratio, and how the color gradient was basically a massive fail. You can read their article on the topic here: [](https://scienceux.org/articles/data-ink-ideal-vs-minimal)<https://scienceux.org/articles/data-ink-ideal-vs-minimal>.

Here's the original paragraph:

Although we just discovered that the item closest to the bottom left corner is not always the one to pick, it is true that in general that the closer to the bottom left corner of the chart a flight is located, the more you'll want to consider it. So one nice piece we can add is a gradient which leads the user's eye to that point. We've also made the grid and the chart labels white against a dark background, and we switched our red/green outlines for baggage to use white/dark instead. In [my previous article about data ink](/tech-talk/2026/08/03/data-ink-ratio-fifa.md) I used red/green but I don't think that's the nicest experience for someone who has a color vision deficiency.

***

## Building scatter charts with VisuallyJs[​](#building-scatter-charts-with-visuallyjs "Direct link to Building scatter charts with VisuallyJs")

This page makes use of VisuallyJs's powerful and flexible charts API - it's a React app but we offer the exact same set of components for Angular, Vue and Svelte. Charts in VisuallyJs follow the same API design principles as the rest of VisuallyJs: sensible defaults, and a balance of API complexity to features.

To embed a chart in your app:

```jsx
<ScatterChartComponent data={flights} options={options}/>

```

Our options contains config for:

* the chart's data series;
* the title and labelling of the X axis
* the title and labelling of the Y axis (we use a custom label formatter in this chart, which returns different values based upon the current Y axis)
* a spec for a tooltip to show on hover

```javascript
return {
  series: [
  {
    id: "flights",
    xAxisField: "price",
    yAxisField: yAxisField || "durationHours",
    resolveMarker: (point) => getAirlineIcon(point.airline),
    markerSize: 32
  }],
  xAxis: {
    title: {
      text:"Price ($)"
    },
    labelPrefix: "$"
  },
  yAxis: {
    title: {
      text: isVariance ? "Departure Variance (hours)" : (isLuggage ? "Baggage Allowance (bags)" : "Duration (hours)")
    },
    labelFormatter: (value) => {
      if (isLuggage) {
        return `${value} bag${value === 1 ? '' : 's'}`;
      }
      const hours = Math.floor(value);
      const minutes = Math.round((value - hours) * 60);
      return `${hours}h${minutes}m`;
    }
  },
  tooltip: {
    format: "<b>{{point.airline}}</b><br/>Dep: {{point.departureTimeFormatted}}<br/>Arr: {{point.arrivalTimeFormatted}}<br/>{{point.duration}}<br/><b>${{point.price}}</b>"
  }
}

```

***

## Summary[​](#summary "Direct link to Summary")

Have any comments? Drop us a line via the [contact page](/contact.md) - we love to chat about this sort of stuff.

***

***

### Try VisuallyJs[​](#try-visuallyjs "Direct link to Try VisuallyJs")

VisuallyJs offers an extensive list of starter apps, diagrams, charts and dashboards to quick start your development, in React, Angular, Vue, Svelte and Typescript/Javascript.

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/callflow-1200.png)

Call Flow

Use VisuallyJs to build a visual Call Flow editor

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/ai-agent-builder-1200.png)

AI Agent Builder

Use VisuallyJs to create an advanced AI agent builder

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/chatbot-1200.png)

Chatbot

Use VisuallyJs to build a Chatbot editor, with actions, messages, input and choices

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/flowchart-1200.png)

Flowchart

Fully featured flowchart builder including support for custom shapes, edge routing to avoid vertices, shape resize/rotate, SVG/PNG/JPG export and more

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/bpmn-1200.png)

BPMN

BPMN editor for modelling the steps of a business process. Pools, lanes, and a full set of task, event and gateway types

![VisuallyJs - callflow builders, sankey charts, database schemas, ERD diagrams and more](https://static.visuallyjs.com/img/app-card/erd-1200.png)

ERD

ERD editor for modelling the steps of a business process

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/gantt-1200.png)

Gantt

Interactive Gantt chart featuring tasks, task groups and milestones

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/kanban-1200.png)

Kanban

Fully featured Kanban board. Drag items between columns and use the inspector to update items and columns

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/schema-1200.png)

Database Schema

Database Schema builder with support for tables, views, multiple columns types, and column relationships

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/orgchart-1200.png)

Org Chart

Uses the classic org chart layout and provides an inspector from which the user can navigate around

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/circuit-diagram-1200.png)

Circuit Diagram

Fully featured starter app containing a circuit diagram builder

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/scada-hmi-1200.png)

Scada/HMI

Professional and modern Scada/HMI application with fluid, heating/cooling & instrumentation shapes, adhering to the HMI ISA-101 Design Standard

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/mindmap-1200.png)

Mindmap

The mindmap builder highlights several advanced features, such as custom layouts, parsers and exporters

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/neighbourhood-views-1200.png)

Neighbourhood Views

Demonstrates how to include multiple views of a dataset on one page

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/logic-gates-1200.png)

Logic Gates

Fully featured starter app containing a logic gates diagram builder

![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/template-1200.png)

Template

Basic starter app demonstrating how to setup VisuallyJs and its main features

![When you've reached the limits with ReactFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/area-line-chart-1200.png)

Area & Line charts

Use VisuallyJs to create area and line charts

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](https://static.visuallyjs.com/img/app-card/bar-column-chart-1200.png)

Bar & Column charts

Multiple series, stacked, grouped, pivoted, and much more

![When you've reached the limits with ngDiagram, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/scatter-bubble-chart-1200.png)

Scatter & Bubble charts

Circle, rectangle, triangle or custom markers, multiple series, fully customizable

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/sankey-1200.png)

Sankey chart

Use VisuallyJs to create a professional Sankey chart, with support for pivoting

![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/supply-chain-1200.png)

Supply Chain Analyzer

Dashboard for managing and analyzing supply chains

![VisuallyJs - JavaScript and Typescript diagramming library that fuels exceptional UIs](https://static.visuallyjs.com/img/app-card/network-infrastructure-1200.png)

Network Infrastructure

Combine a network management diagram with charts showing projected cost and resource usage

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/list-manager-1200.png)

Scrolling Lists

Use the ListManager plugin to manage scrolling lists: as elements are scrolled out of the view, their edges are moved to the list container

![VisuallyJs - effortlessly build professional node based UIs with Javascript, Typescript, React, Svelte, Angular and Vue](https://static.visuallyjs.com/img/app-card/fifaworldcup-1200.png)

FIFA World Cup

A visualizer for the FIFA World cup - group stages, team journeys and a tournament view.

![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/fault-tree-analysis-1200.png)

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
* [scatter chart](/tech-talk/tags/scatter-chart.md)
* [bubble chart](/tech-talk/tags/bubble-chart.md)
* [amadeus](/tech-talk/tags/amadeus.md)
* [GDS](/tech-talk/tags/gds.md)
