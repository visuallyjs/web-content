# Hierarchy Layout

The Hierarchy layout positions vertices in a hierarchy, oriented either vertically or horizontally, following a slightly modified version of the 'Sugiyama' method.

```html
<script setup>

import { HierarchyLayout } from "@visuallyjs/browser-ui"

const renderOptions = {
  layout: {
    type: HierarchyLayout.type
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

***

### Orientation[​](#orientation "Direct link to Orientation")

The layout at the top of this page shows the `horizontal` orientation, which is the default. Here we show the same dataset in the `vertical` orientation:

```html
<script setup>

import { HierarchyLayout } from "@visuallyjs/browser-ui"

const renderOptions = {
  layout: {
    type: HierarchyLayout.type,
    options: {
      axis: "vertical"
    }
  },
  defaults: {
    anchors: [
      "Right",
      "Left"
    ]
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

***

### Placement Strategy[​](#placement-strategy "Direct link to Placement Strategy")

You can use a few different "placement strategies" with the Hierarchy layout. By default, the child elements of some parent are positioned with respect to the center of their parent element (you can see this in the layouts above). This behaviour corresponds to a `placementStrategy` of `parent`.

You can, instead, instruct the layout to position elements with respect to the layout's main axis, should you wish to, using a `placementStrategy` of `center`, `start` or `end`.

Here we see `placementStrategy:'center'` in operation - each layer is positioned such that its center point lies on the main axis of the layout:

##### Hierarchy layout with placementStrategy<!-- -->:center[​](#hierarchy-layout-with-placementstrategy "Direct link to hierarchy-layout-with-placementstrategy")

In the next two examples we use `start` and `end`. Note how these roughly correlate to the way `flex-start` and `flex-end` function in a flex layout.

##### Hierarchy layout with placementStrategy<!-- -->:start[​](#hierarchy-layout-with-placementstrategy-1 "Direct link to hierarchy-layout-with-placementstrategy-1")

##### Hierarchy layout with placementStrategy<!-- -->:end[​](#hierarchy-layout-with-placementstrategy-2 "Direct link to hierarchy-layout-with-placementstrategy-2")

### Alignment[​](#alignment "Direct link to Alignment")

A separate, but related, concept to the `placementStrategy` is that of `alignment`, which instructs the layout how to place child elements with respect to their parent element, and is only used when `placementStrategy` is set to `parent`. Here's the first layout from above, but with `alignment:'start'` set:

```html
<script setup>

import { HierarchyLayout } from "@visuallyjs/browser-ui"

const renderOptions = {
  layout: {
    type: HierarchyLayout.type,
    options: {
      alignment: "start"
    }
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

### Determining the root node(s)[​](#determining-the-root-nodes "Direct link to Determining the root node(s)")

In the Hierarchy layout there are always one or more "root" vertices, which are vertices that are to be placed at the root of the hierarchy. The layout calculates these by looking for vertices that are not the target of any edges. If it finds none, an arbitrary vertex will be used as the initial root. From each root, edges are followed and connected vertices are placed, until there are no more edges to follow. There may be more than one root in a given dataset.

You can specify a root node by setting it as the `rootNode`:

```html
<script setup>

import { HierarchyLayout } from "@visuallyjs/browser-ui"

const renderOptions = {
  layout: {
    type: HierarchyLayout.type,
    options: {
      rootNode: rootNode,
      axis: "horizontal"
    }
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

Note that we said "a" root node, and not "the" root node, as after placing every node connected to your nominated root, the layout will continue to place other root nodes that it has found.

### Edge routing[​](#edge-routing "Direct link to Edge routing")

The Hierarchy layout can generate routing information for edges, via the `generateRouting` flag:

To setup edge routing you need 3 things:

* You must be using a `Hierarchy` layout and you need to have `generateRouting:true` in the layout options:

* You must be using the [Straight](/vue/docs/apps/edges/connectors.md#straight) connector type. This is the default connector type so if you haven't specifically set a connector anywhere you'll be using this.

* You need to enable the [edge routing plugin](/vue/docs/apps/plugins/edge-routing.md)

```html
<script setup>

import { HierarchyLayout, EdgeRoutingPlugin } from "@visuallyjs/browser-ui"

const renderOptions = {
  layout: {
    type: HierarchyLayout.type,
    options: {
      generateRouting: true
    }
  },
  plugins: [
    {
      type: EdgeRoutingPlugin.type
    }
  ]
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

A deeper discussion of edge routing can be on the [edge routing plugin page](/vue/docs/apps/plugins/edge-routing.md), but to whet your appetite, here's the Hierarchy layout configured to use [orthogonal routing](/vue/docs/apps/plugins/edge-routing.md#orthogonal):

***

### Parameters[​](#parameters "Direct link to Parameters")

HierarchyLayoutParameters

Optional parameters for a Hierarchy layout

| Name                             | Type                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------------------- | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| absoluteBacked?                  | boolean                        | Defaults to false. If true, then the layout will use any position values found in the data for a given vertex.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| alignment?                       | [HierarchyLayoutAlignment]()   | Optional, defaults to `HierarchyLayoutAlignmentValues.center`. Instructs the layout how to place child nodes with respect to their parent nodes. By default, a group of child nodes is centered on its parent. The layout also supports "start" and "end" for this value, which work in much the same way as "flex-start" and "flex-end" do in CSS: for a layout with the root at the top of the tree and the child nodes underneath, a value of "start" for align would cause the first child of the root to be placed immediately under the root, with its first child immediately underneath, etc. The remainder of the content would fan out to the right. This option also works in conjunction with invert and axis<!-- -->:HierarchyLayoutAxisValues<!-- -->.vertical. |
| axis?                            | [HierarchyLayoutAxis]()        | Either `horizontal` (the default, groups of child vertices are laid out in rows) or `vertical` (groups of child vertices are laid out in columns)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| gatherUnattachedRoots?           | boolean                        | If true root nodes that do not have children will be positioned adjacent to the last root node that does have children. When false (which is the default), unattached roots are spaced apart so that they do not overlap any child trees.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| generateRouting?                 | boolean                        | Defaults to false. If true, the layout generates routing information for the channels between layers and edge nodes, and for edge routing.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| getRootNode?                     | () => [AbstractEdgeTerminus]() | Optional function you can provide that will dynamically be invoked to get the root node to use.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| height?                          | number                         | Optional fixed height for the layout.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| invert?                          | boolean                        | If true, the layout will be inverted in its perpendicular axis. For instance, if `axis` is "horizontal" and `invert` is true, the root nodes of the layout will be placed at the bottom of the layout, and their children will be placed above them.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| leavesAtBottom?                  | boolean                        | If true, all of the leaf nodes will be placed at the bottom of the layout (or at the right hand side if the axis is `vertical`)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| locationFunction?                | [LocationFunction]()           | Optional function that, given some vertex, can provide the x/y location of the vertex on the canvas                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| maxIterations?                   | number                         | Maximum number of iterations to run. Defaults to 24.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| maxIterationsWithoutImprovement? | number                         | Number of iterations to try rearranging the graph without an improvement in legibility before accepting the current state. Defaults to 2.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| padding?                         | [PointXY]()                    | Optional padding to put around the elements.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| placementStrategy?               | PlacementStageStrategy         | The strategy to use when placing vertices. Default is 'center', meaning every row is centered around the axis orthogonal to the axis in which the vertices are laid out.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| rootNode?                        | any                            | Optional node to use as the root. If this is not provided the layout calculates the best candidate based upon incoming and outgoing edges for each vertex.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| width?                           | number                         | Optional fixed width for the layout.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
