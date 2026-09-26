# Bowtie Layout

The Bowtie layout positions vertices branching out from a central "focus" vertex. It is useful for visualizing processes or relationships that have both upstream and downstream components relative to a specific node.

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { BowtieLayout } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  layout: {
    type: BowtieLayout.type,
    options: {
      rootNode: "1",
      getUpstream: (ds, v) => ds.getVertex(v.id).getAllSourceEdges().filter(e => e.target.data.downstream).map(e => e.target),
      getDownstream: (ds, v) => ds.getVertex(v.id).getAllSourceEdges().filter(e => e.target.data.upstream).map(e => e.target)
    }
  }
};
}

```

In this example, we find upstream nodes with this code:

```javascript
filter(e => e.target.data.upstream)

```

and downstream nodes like this:

```javascript
filter(e => e.target.data.downstream)

```

In this dataset, our nodes have an optional `downstream` or `upstream` data member:

```javascript
{
    id:"2",
    upstream:true
}

```

You can implement whatever strategy you need for determining the upstream and downstream nodes. The `getUpstream` and `getDownstream` methods are given the datasource and the focus vertex as arguments.

***

### Orientation[​](#orientation "Direct link to Orientation")

The Bowtie layout defaults to a `horizontal` orientation, where upstream nodes are placed to the left and downstream nodes to the right. You can switch to a `vertical` orientation using the `axis` parameter:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { BowtieLayout } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  layout: {
    type: BowtieLayout.type,
    options: {
      rootNode: "1",
      axis: "vertical",
      getUpstream: (ds, v) => ds.getVertex(v.id).getAllSourceEdges().filter(e => e.target.data.downstream).map(e => e.target),
      getDownstream: (ds, v) => ds.getVertex(v.id).getAllSourceEdges().filter(e => e.target.data.upstream).map(e => e.target)
    }
  }
};
}

```

***

### Configuration[​](#configuration "Direct link to Configuration")

The Bowtie layout requires you to specify a focus vertex and how to identify its upstream and downstream neighbors.

#### rootNode / getRootNode[​](#rootnode--getrootnode "Direct link to rootNode / getRootNode")

You must provide either `rootNode` (the ID or vertex object of the focus node) or `getRootNode` (a function that returns the ID or vertex object). `getRootNode` has this method signature:

```typescript
getRootNode:(dataSource:DataSource) => Vertex|string

```

#### getUpstream / getDownstream[​](#getupstream--getdownstream "Direct link to getUpstream / getDownstream")

These functions are invoked for the focus vertex to determine which of its immediate neighbors should be considered "upstream" (placed to the left/top) and which should be "downstream" (placed to the right/bottom).

```typescript
getUpstream:(dataSource:DataSource, vertex:HasIdAndType) => Array<HasIdAndType>
getDownstream:(dataSource:DataSource, vertex:HasIdAndType) => Array<HasIdAndType>

```

#### childVerticesFunction[​](#childverticesfunction "Direct link to childVerticesFunction")

For all nodes other than the focus vertex, the layout uses `childVerticesFunction` to find their children. If not provided, the layout defaults to finding all vertices that are targets of edges where the current vertex is the source.

***

### Parameters[​](#parameters "Direct link to Parameters")

BowtieLayoutParameters

Options for the Bowtie layout

| Name                   | Type                                                                            | Description                                                                                                                                                                                                                                                                                                                                       |
| ---------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| axis?                  | "horizontal" \| "vertical"                                                      | Whether to draw the layout horizontally or vertically. Defaults to "horizontal".                                                                                                                                                                                                                                                                  |
| childVerticesFunction? | (node:[HasIdAndType](), dataSource:[DataSource]()) => Array<[HasIdAndType]()>   | Optional function to invoke on any non-focus vertex, to get the vertex's children. Will not be invoked with the focus vertex. If this function returns the focus vertex in its set it will be filtered out. When you do not provide this function, VisuallyJs will find all vertices that are targets of edges for which this vertex is a source. |
| getDownstream          | (dataSource:[DataSource](), vertex:[HasIdAndType]()) => Array<[HasIdAndType]()> | Gets immediate downstream nodes for the focus vertex. Only invoked with the focus vertex.                                                                                                                                                                                                                                                         |
| getRootNode?           | (dataSource:[DataSource]()) => string \| [Vertex]()                             | Optional function you can provide that will dynamically be invoked to get the root node to use. You must provide this or `rootNode`.                                                                                                                                                                                                              |
| getUpstream            | (dataSource:[DataSource](), vertex:[HasIdAndType]()) => Array<[HasIdAndType]()> | Gets immediate upstream nodes for the focus vertex. Only invoked with the focus vertex.                                                                                                                                                                                                                                                           |
| height?                | number                                                                          | Optional fixed height for the layout.                                                                                                                                                                                                                                                                                                             |
| locationFunction?      | [LocationFunction]()                                                            | Optional function that, given some vertex, can provide the x/y location of the vertex on the canvas                                                                                                                                                                                                                                               |
| padding?               | [PointXY]()                                                                     | Optional padding to put around the elements.                                                                                                                                                                                                                                                                                                      |
| rootNode?              | string \| [Vertex]()                                                            | Optional node to use as the root. You must provide this or `getRootNode`.                                                                                                                                                                                                                                                                         |
| width?                 | number                                                                          | Optional fixed width for the layout.                                                                                                                                                                                                                                                                                                              |
