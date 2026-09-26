# Overview

A VisuallyJs <!-- -->Svelte<!-- --> diagram has the following basic structure:

**********

**Controls**

**Miniview**

**Grid**

**Palette**

## Shapes[​](#shapes "Direct link to Shapes")

In a diagram, shapes are represented by SVG. Shapes are supplied by one or more `ShapeSets`, and when you create a diagram you tell VisuallyJs which shape set(s) you want to use. Each shape in your diagram has an associated `type`, which identifies it inside a `ShapeSet`, and it also optionally has a `category`, which identifies the shape set it belongs to.

VisuallyJs ships with three shape sets - `Flowchart`, `Basic` and `BPMN2`, and you can easily make your own. There are also examples of shape sets in the [Circuit Builder](/demonstrations/circuit-builder) and [Logic Gates](/demonstrations/logic-gates.md) starter applications.

Read more about shapes and shape sets [on this page](/svelte/docs/diagrams/shapes/shape-libraries.md).

## Edges[​](#edges "Direct link to Edges")

Edges join shapes, and they can be represented in several different ways - the representation of an edge is called a `Connector`. In the above example we use an `Orthogonal` connector, which consists of horizontal and vertical lines only; VisuallyJs ships with several connector types, including Straight (one or more straight line segments, optionally smoothed), Bezier (a cubic Bézier curve) and QuadraticBezier (a Bézier curve with a single control point), and you can also create your own.

In the diagram options, you can declare various aspect of how an edge appears, such as the connector used, where on the vertex the edge should be anchored, the appearance of the edge, its label, etc. You can also map event handlers to hook in to mouse/touch events with your edges.

## Mediator[​](#mediator "Direct link to Mediator")

The mediator is responsible for managing which operations are allowed in your diagram - such things as which tools should be available on shapes, what can be dropped where, etc. A mediator is optional, but it is a very powerful way to control your diagram in a declarative manner. Read more about the things you can do with a mediator [in the mediator docs](/svelte/docs/diagrams/controlling-diagram-actions.md).

## Controls[​](#controls "Direct link to Controls")

Common controls such as zoom to extents, undo/redo, clear dataset - and many more - are available in a dedicated component. Read about configuring the controls component [on this page](/svelte/docs/diagrams/controls).

## Miniview[​](#miniview "Direct link to Miniview")

Provides a summary view of your diagram and allows you to zoom (via pinch/mouse wheel), pan and center on specific elements. Read about configuring the controls component [on this page](/svelte/docs/diagrams/miniview).
