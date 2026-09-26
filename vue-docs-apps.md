# Overview

A VisuallyJs <!-- -->Vue<!-- --> app has the following basic structure:

**********

**Controls**

**Miniview**

## Nodes[​](#nodes "Direct link to Nodes")

You can provide arbitrary JSX to render your nodes. In the above example we have drawn our nodes as basic coloured boxes, but your JSX can be as complex or as simple as you want, interacting with other parts of your app, communicating to the backend - whatever you like. VisuallyJs will take care of rendering and unloading nodes as needed. This is extremely powerful and its possibilities are only limited by your imagination (or perhaps your manager's budget).

Nodes are mapped by their `type` in VisuallyJs by an object we call a `View`, which allows you to configure different JSX for different types of nodes, and these mappings can inherit from each other - you can setup some behaviour in a base node type and then extend this type for specific subtypes. VisuallyJs also lets you declare various other behaviours for a node type - events such as tap, click, mouseover, etc can be mapped to listeners.

You can provide any valid Vue component to render your nodes. In the above example we have drawn our nodes as basic coloured boxes, but your components can be as complex or as simple as you want, interacting with other parts of your app, communicating to the backend - whatever you like. VisuallyJs will take care of rendering and unloading nodes as needed. This is extremely powerful and its possibilities are only limited by your imagination (or perhaps your manager's budget).

Nodes are mapped by their `type` in VisuallyJs by an object we call a `View`, which allows you to configure different components for different types of nodes, and these mappings can inherit from each other - you can setup some behaviour in a base node type and then extend this type for specific subtypes. VisuallyJs also lets you declare various other behaviours for a node type - events such as tap, click, mouseover, etc can be mapped to listeners.

For a full discussion of rendering nodes, see the [Nodes and Groups documentation](/vue/docs/apps/nodes-and-groups/overview.md).

## Groups[​](#groups "Direct link to Groups")

A group contains nodes or other groups (which may be nested to an arbitrary level). As with nodes, you provide the JSX you wish to use to render each group, and any group specific behaviours, by mapping a group type inside a view.

A group contains nodes or other groups (which may be nested to an arbitrary level). As with nodes, you provide the component you wish to use to render each group, and any group specific behaviours, by mapping a group type inside a view.

Groups offer a number of options for how to control their child nodes or groups: the above example prevents the node from being dragged outside of the group, but you can instruct VisuallyJs to allow nodes to be dragged out of groups, and you can also control what nodes/groups can be dropped on a group.

For a full discussion of rendering groups, see the [Nodes and Groups documentation](/vue/docs/apps/nodes-and-groups/overview.md).

## Edges[​](#edges "Direct link to Edges")

Edges join nodes/groups, and they can be represented in several different ways - the representation of an edge is called a `Connector`. In the above example we use a straight connector, which is the default, but VisuallyJs ships with `Orthogonal` (horizontal and vertical lines only), `Bezier` (a cubic Bézier curve) and `QuadraticBezier` (a Bézier curve with a single control point), and you can also create your own.

As with nodes and groups, edges are mapped via a `type` in a view. This type can declare various aspect of how an edge appears, such as the connector used, where on the vertex the edge should be anchored, the appearance of the edge, its label, etc. You can also map event handlers in an edge type to hook in to mouse/touch events with your edges.

### Anchors[​](#anchors "Direct link to Anchors")

A key concept with edges is where they are anchored to the vertices to which they are connected.

### Overlays[​](#overlays "Direct link to Overlays")

Edges can have any number of `Overlays` attached to them. In the above example each edge has a `Label` overlay positioned halfway along the path, and an `Arrow` overlay at the target vertex.

### Markers[​](#markers "Direct link to Markers")

Edges can have a source and or target `Marker` - these are overlays which are positioned at the start/end of an edge, so using markers provides a shortcut to having to configure an overlay's location, but they also have another advantage: VisuallyJs takes markers into account when computing the path for an edge, making the path start and end at marker boundaries.

***

For a full discussion of how to render edges, see the [Edges documentation](/vue/docs/apps/edges/overview.md).

## Controls[​](#controls "Direct link to Controls")

This component provides a set of controls for a surface - such operations as zoom to extents, undo/redo, clear, etc. The operations that are available can be specified on the controls element, and you can also add your own buttons.

The reference page for this component can be [found here](/vue/docs/reference/ControlsComponent.md).

## Miniview[​](#miniview "Direct link to Miniview")

Provides a miniaturized view of a surface, showing the nodes/groups in the surface canvas. Users can pan/zoom the surface via pointer/touch events on the miniview, and click on specific vertices to have the surface center itself on the clicked vertex.

The reference page for this component can be [found here](/vue/docs/reference/MiniviewComponent.md).

## Next Steps[​](#next-steps "Direct link to Next Steps")

[Building an app](/vue/docs/apps/building-an-app.md)

[A guided step-by-step on building your first app](/vue/docs/apps/building-an-app.md)

[Edges](/vue/docs/apps/edges/overview.md)

[Read about the various ways you can create and interact with edges](/vue/docs/apps/edges/overview.md)

[Nodes and Groups](/vue/docs/apps/nodes-and-groups/overview.md)

[Read about the various ways you can create and interact with nodes and groups](/vue/docs/apps/nodes-and-groups/overview.md)

[Data Model](/vue/docs/apps/model/overview.md)

[Read an in-depth guide to the VisuallyJs data model](/vue/docs/apps/model/overview.md)
