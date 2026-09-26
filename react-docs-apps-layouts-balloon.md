# Balloon Layout

This layout groups vertices into clusters.

This layout is useful for unstructured data - database schemas, mind maps, graphs, etc. For a given input graph the structure of the layout will always be the same, but this layout does not extend the [Absolute](/react/docs/apps/layouts/absolute.md) layout as the [ForceDirected](/react/docs/apps/layouts/force-directed.md) layout does, so all vertex placement is decided upon by the layout.

## Parameters[​](#parameters "Direct link to Parameters")

BalloonLayoutParameters

Constructor parameters for a Balloon layout.

| Name              | Type                                                    | Description                                                                                                                                                                                                                                                                                                                                                            |
| ----------------- | ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| absoluteBacked?   | boolean                                                 | Defaults to false. If true, then the layout will use any position values found in the data for a given vertex.                                                                                                                                                                                                                                                         |
| getChildEdges     | [ChildEdgesFunction]()                                  | The function that retrieves child edges for a given vertex. This function defines how the<br />layout walks your data model to generate the output.                                                                                                                                                                                                                    |
| getChildVertices? | [HierarchicalLayoutChildVerticesFunction<]()[Vertex]()> | Optional function used to determine the edges to traverse to find children from some node                                                                                                                                                                                                                                                                              |
| getRootNode?      | (dataSource:[DataSource]()) => Array<[Vertex]()>        | Optional. A function that is given the data source instance as argument and is expected to return either a<br />single node/group, or an array of nodes/groups, to use as the root(s) for the layout                                                                                                                                                                   |
| groupPadding?     | number                                                  | Minimum distance between a group of vertices and its neighbours. Defaults to 100 pixels.                                                                                                                                                                                                                                                                               |
| height?           | number                                                  | Optional fixed height for the layout.                                                                                                                                                                                                                                                                                                                                  |
| ignoreLoops?      | boolean                                                 | Defaults to true. If a loop is found during the layout it is usually ignored, unless this is set to true.                                                                                                                                                                                                                                                              |
| ignorePorts?      | boolean                                                 | Defaults to false, meaning that ports are taken into account when figuring the list of edges from some vertex.<br />If you set this to `true`, ports will be ignored and the layout will only consider edges connected directly to<br />each vertex.                                                                                                                   |
| locationFunction? | [LocationFunction]()                                    | Optional function that, given some vertex, can provide the x/y location of the vertex on the canvas                                                                                                                                                                                                                                                                    |
| padding?          | [PointXY]()                                             | Optional padding to put around the elements.                                                                                                                                                                                                                                                                                                                           |
| rootNode?         | Array<[Vertex]()>                                       | Optional. Defines the nodes/groups to use as the root of the tree. These may be provided as an array of either a<br />node/group id or a node/group object. If this parameter is not specified and multipleRoots is not false then the<br />layout uses the result(s) of the `getRootNode` function; otherwise it uses the first node/group found in the<br />dataset. |
| width?            | number                                                  | Optional fixed width for the layout.                                                                                                                                                                                                                                                                                                                                   |

## Example[​](#example "Direct link to Example")

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BalloonLayout } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  layout: {
    type: BalloonLayout.type
  }
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

## Behaviour after relayout[​](#behaviour-after-relayout "Direct link to Behaviour after relayout")

A relayout will generate the exact same arrangement of vertices, since this layout is deterministic. But any changes to node/group dimensions will be taken into account.

## Behaviour after refresh[​](#behaviour-after-refresh "Direct link to Behaviour after refresh")

A refresh will generate the exact same arrangement of nodes/groups, since this layout is deterministic. But any changes to node/group dimensions will be taken into account.
