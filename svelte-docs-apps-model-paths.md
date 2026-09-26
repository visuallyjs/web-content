# Paths

A `Path` represents the path from one vertex (a node/port/group) through a series of edges and intermediate vertices to another vertex. VisuallyJs provides several methods for the creation and manipulation of paths, as well as animating overlays along a path.

You can work with paths through both an instance of the VisuallyJs model and any Surfaces. The object representing a path differs slightly between the two, in that paths created from a Surface support a few extra (UI-related) methods, such as `setVisible`.

## Getting a Path[​](#getting-a-path "Direct link to Getting a Path")

To get a Path, you call `getPath` on either a model instance or a Surface, with a valid path spec. A quick example to kick off:

```javascript
model.getPath({
  source:someNode,
  target:someOtherNode
});

```

This will return you the **shortest path** from `someNode` to `someOtherNode`, where the path length is related to its `cost`.

### Paths including ports[​](#paths-including-ports "Direct link to Paths including ports")

By default, VisuallyJs will search for paths in "strict" mode, meaning if you supply a node/group as source/target, then only edges directly connected to that node/group will be traversed in the search for a path. Switching off "strict" mode relaxes this restriction, and also includes edges connected to any ports on the given node/group. See below.

## Path specs[​](#path-specs "Direct link to Path specs")

This is the full list of supported parameters to the `getPath` method.

PathOptions

Options for a Path.

| Name        | Type                    | Description                                                                                                                                                                                                                                                                         |
| ----------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| edgeFilter? | (n:[Edge]()) => boolean | This function is given each Edge's backing data and asked to return true or false - true means include the Edge, false means exclude it.                                                                                                                                            |
| nodeFilter? | (n:[Node]()) => boolean | This function is given each Node/Group's backing data and asked to return true or false - true means include the Node/Group, false means exclude it.                                                                                                                                |
| source      | string \| [Vertex]()    | Path source. Either a vertex (node/group/port) or a vertex id.                                                                                                                                                                                                                      |
| strict?     | boolean                 | Sets whether or not paths are searched strictly by the given source/target. If you supply a node as the source, but there are only edges connected to ports on that node, by default these edges will be ignored. Switching `strict` to false will mean these edges are considered. |
| target      | string \| [Vertex]()    | Path target. Either a vertex (node/group/port) or a vertex id.                                                                                                                                                                                                                      |

### Filtering nodes[​](#filtering-nodes "Direct link to Filtering nodes")

```javascript
model.getPath({
  source:someNode,
  target:someOtherNode,
  nodeFilter:(n) => {
    return n.data.type != "aTypeIWantToIgnore";
  }
});

```

Here we pass in a function that will be called for every prospective node in the path. If it returns false then the graph treats the node as if it were at a distance of Infinity - not reachable.

### Filtering edges[​](#filtering-edges "Direct link to Filtering edges")

You can also provide an `edgeFilter` to control which edges your path will traverse:

```javascript
model.getPath({
  source:someNode,
  target:someOtherNode,
  edgeFilter:function(e) {
    return e.data.type != "aTypeIWantToIgnore";
  }
});

```

tip

The arguments to these functions are `Node` or `Edge` objects from the model. You may wish to use information contained in those classes to make your decisions, but if you just want to access the original data, you use the `data` member as shown above.

***

## Paths in the UI[​](#paths-in-the-ui "Direct link to Paths in the UI")

Calling `getPath(...)` on a Surface returns you a `UIPath` object, which contains a `Path` and offers a few extra methods for manipulating the appearance of the components of the path. All of the class manipulation methods take a space-delimited string as argument. See below for a detailed list of the available methods on a `UIPath`.

note

Calling any of the methods from the basic Path object on the result of a `getPath` call to a Surface that result in a change to the data model will cause those data model changes to be communicated automatically to any other Surface registered on the given model instance.

### Animating paths[​](#animating-paths "Direct link to Animating paths")

The surface component supports tracing a path between a given source and target node using an overlay.

**********

```javascript

import { newInstance } from "@visuallyjs/browser-ui"

// setup two nodes and connect

let model = newInstance()
let renderer = model.render(someElement)
model.load({
  data:{
    nodes: [    a bunch of nodes. let's pretend they have IDs from 1 - 34 ],
    edges:[ a bunch of edges ]
  }
});

let transport = renderer.tracePath({
    source:1,
    target:23,
    overlay:"Arrow"
});

if (!transport.pathExists) {
    alert("There was no such path");
}


```

In this example we've attempted to trace an arrow overlay along the *shortest path* from node 1 to node 23, using the default animation options, which are:

* travel at 100 pixels per second
* use a frame rate of 30 frames per second
* dwell on each intermediate element for 250 milliseconds

The return values from the `tracePath` method is a `PathTransport` object, which offers the following methods:

* `play()` Starts the animation
* `pause()` Pauses the animation
* `cancel()` Cancels the animation
* `bind(event:string, handler:Function)` Binds an event handler. Only one event - "state" - is fired, in fact, and it's generally better practise to supply a `listener` to the `tracePath` method call instead, because binding to the transport after it has been created means you will miss the initial `start` state event change.

We can enhance the previous call, then, with an event listener like this:

```javascript

import { newInstance } from "@visuallyjs/browser-ui"

function stateChange(newState) {
    console.log("The new state is " + newState);
}

// setup two nodes and connect
let model = newInstance()
let renderer = model.render(someElement)
model.load({
  data:{
    nodes: [    a bunch of nodes. let's pretend they have IDs from 1 - 34 ],
    edges:[ a bunch of edges ]
  }
});

let transport = renderer.tracePath({
    source:1,
    target:23,
    overlay:"Arrow",
    listener: stateChange
});

if (!transport.pathExists) {
    alert("There was no such path");
}


```

The DemoLink title="Path Tracing demonstration" id="paths" /> has an example of a full setup with an event listener and play/pause/cancel controls.

### Animation Options[​](#animation-options "Direct link to Animation Options")

You can change the default animation options if you need to:

```javascript
const transport = renderer.tracePath({
    source:1,
    target:23,
    overlay:"Arrow",
    options:{
      speed: 25,   // pixels per second
      rate: 60     // frames per second
      dwell: 50    // dwell on intermediate elements for 50 milliseconds
    }
});

```

### Tracing a specific Path[​](#tracing-a-specific-path "Direct link to Tracing a specific Path")

The two examples given so far do not mandate any specific path to travel from the source to the target, so VisuallyJs will pick the shortest path (which is controlled by both number of hops and edge *cost* if you have provided that for any of your edges). However, you can supply any path to this method, should you want to.

To get a path that is not the shortest path you will need to make use of a `nodeFilter` and/or `edgeFilter` when you call `getPath` on some model instance, as discussed above. An example:

```javascript
let path = model.getPath({
    source:1,
    target:23,
    edgeFilter:(edge) => {
      return !edge.data.type === "aTypeIWouldIgnore"
    }
});

```

This path can then be passed to `tracePath` instead of providing a `source` and `target`:

```javascript
renderer.tracePath({
    path:path,
    overlay:"Arrow",
    options:{
      speed: 25,   // pixels per second
      rate: 60,     // frames per second
      dwell: 50    // dwell on intermediate elements for 50 milliseconds
    }
});

```

***

### CSS Classes[​](#css-classes "Direct link to CSS Classes")

ClassTable id="pathTraversal"/>

***

### Events[​](#events "Direct link to Events")

These events will be fired by the renderer during a path traversal:

EventTable id="surface" topic="pathTraversal"/>

## API details[​](#api-details "Direct link to API details")

### The Path object[​](#the-path-object "Direct link to The Path object")

API docs for the basic Path object, as used by an instance of VisuallyJs, can be found [Path]()

Path

Models the path between two vertices, which consists of a series of vertices connected by edges.

| Name           | Type | Description    |
| -------------- | ---- | -------------- |
| contains       |      | no description |
| deleteAll      |      | no description |
| deleteEdges    |      | no description |
| deleteVertices |      | no description |
| each           |      | no description |
| eachEdge       |      | no description |
| eachGroup      |      | no description |
| eachNode       |      | no description |
| eachVertex     |      | no description |
| exists         |      | no description |
| filter         |      | no description |
| getAllEdgesFor |      | no description |
| getCost        |      | no description |
| getEdgeAt      |      | no description |
| getEdgeCount   |      | no description |
| getNodeAt      |      | no description |
| getVertex      |      | no description |
| getVertexCount |      | no description |
| getVertices    |      | no description |
| isEmpty        |      | no description |

caution

Once you have executed one of the `delete***` methods on a path, your path may contain references to objects that no longer exist in VisuallyJs.

### The UIPath object[​](#the-uipath-object "Direct link to The UIPath object")

API docs for the UIPath object, returned from a `getPath` call on a Surface, can be found [UIPath]()
