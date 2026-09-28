# Introduction

VisuallyJs is a flexible, standards-based library for building interactive node-based applications, diagrams and charts. Whether you need to build a complex node-based editor, a data-driven diagram, or an insightful dashboard with various chart types, VisuallyJs provides the tools you need to create a seamless user experience.

<!-- -->

## What can you build with VisuallyJs?[​](#what-can-you-build-with-visuallyjs "Direct link to What can you build with VisuallyJs?")

### Node-based applications[​](#node-based-applications "Direct link to Node-based applications")

Apps use <!-- -->Svelte<!-- --> components to render each node/group in the display. Functionality can be encapsulated in these components. Node/group sizes in an App are typically dependent on CSS and are managed automatically by VisuallyJs. Apps are great when you need rich content in your nodes/groups and you don't want to be limited to using SVG.

[![When you've reached the limits with SvelteFlow, VisuallyJs has what you need](https://static.visuallyjs.com/img/app-card/callflow-2400.png)](/demonstrations/callflow.md)

[Call Flow](/demonstrations/callflow.md)

### Diagrams[​](#diagrams "Direct link to Diagrams")

Diagrams are pure SVG applications, that draw SVG shapes into an SVG canvas, and provide an API to manipulate each cell/link individually. VisuallyJs offers a <!-- -->Svelte<!-- --> component that you can use to seamlessly embed a Diagram into your application, as well as several other components such as a miniview, a palette (from which shapes can be dragged onto the canvas), and basic controls such as pan/zoom/undo/redo etc.

VisuallyJs comes with built-in shape sets like Flowchart and BPMN, and you can easily create your own.

[![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/flowchart-2400.png)](/demonstrations/flowchart.md)

[Flowchart](/demonstrations/flowchart.md)

### Charts[​](#charts "Direct link to Charts")

VisuallyJs includes a wide range of chart types—from standard Line and Bar charts to more specialized Pie, Donut, and Scatter charts, which can be rendered standalone, or integrated with the data model that is powering an App or Diagram on the same page.

[![VisuallyJs - build diagrams and rich visual UIs fast](https://static.visuallyjs.com/img/app-card/area-line-chart-2400.png)](/demonstrations/area-line-chart.md)

[Area & Line charts](/demonstrations/area-line-chart.md)

### Dashboards[​](#dashboards "Direct link to Dashboards")

A powerful feature of VisuallyJs is the ability to mix and match different types of components on a single page. You can create a dashboard that combines a rich node-based canvas or a diagram with real-time charts, all powered by the same underlying data model.

For example, you might have an app representing a manufacturing process where clicking on a machine (a node in the app) updates a set of charts showing that machine's performance metrics. Or a supply chain visualizer with an attached sankey diagram giving you insights into the flow of materials - there are endless possibilities.

<!-- -->

[![VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](https://static.visuallyjs.com/img/app-card/supply-chain-2400.png)](/demonstrations/supply-chain.md)

[Supply Chain Analyzer](/demonstrations/supply-chain.md)

## Flexible and Standards-Based[​](#flexible-and-standards-based "Direct link to Flexible and Standards-Based")

VisuallyJs is built on modern web standards. It uses SVG for diagrams and charts, and HTML/SVG for Apps, and exposes a wide range of CSS classes for you to hook into. This ensures that your visualizations are accessible, performant, and easy to style. The library's architecture is highly extensible, allowing you to create custom connectors, shapes, layouts and new charts to suit your specific needs.
