# ForceDirected Layout

This layout models edges as springs, placing connected elements nearby, and ensuring adequate space between all elements. [Wikipedia](http://en.wikipedia.org/wiki/Force-directed_graph_drawing) has a good introduction to these types of layouts. It is useful for unstructured data - database schemas, mind maps, graphs, etc. Force-directed algorithms initially position nodes with a degree of randomness and so do not ever produce exactly the same result twice (try reloading this page) - for this reason it is recommended that you read the note on \[refresh vs re-layout]/lib/layouts#refreshvsrelayout)

### Parameters[​](#parameters "Direct link to Parameters")

ForceDirectedLayoutParameters

Parameters for the force directed layout

| Name              | Type                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| absoluteBacked?   | boolean              | Defaults to false. If true, then the layout will use any position values found in the data for a given vertex.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| height?           | number               | Optional fixed height for the layout.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| iterations?       | number               | Maximum number of iterations to run. Defaults to 50. Increasing this number may result in a nicer output, at the expense of run time.                                                                                                                                                                                                                                                                                                                                                                                                         |
| locationFunction? | [LocationFunction]() | Optional function that, given some vertex, can provide the x/y location of the vertex on the canvas                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| padding?          | [PointXY]()          | Optional padding to put around the elements.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| r?                | number               | The amount of travel to impose on each element every time a repulsion or attraction event occurs during the calculation of the layout. This is expressed as a fraction of the distance the two elements would travel in order to be `spacing` pixels apart. Defaults to 0.25. A value of 1 here may seem desirable but in general will not provide the best results: moving one pair of elements by their ideal amount can negatively affect many others. It is better to provide a fractional value here and allow the layout to compromise. |
| spacing?          | number               | Ideal spacing to leave between elements. Defaults to 250px, but this does not mean that elements end up separated by exactly 250px.                                                                                                                                                                                                                                                                                                                                                                                                           |
| width?            | number               | Optional fixed width for the layout.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

### Example[​](#example "Direct link to Example")

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { ForceDirectedLayout } from "@visuallyjs/browser-ui"
  const renderOptions = {
  layout: {
    type: ForceDirectedLayout.type
  }
}
</script>

<SurfaceComponent {renderOptions}/>

```

### Placement of vertices[​](#placement-of-vertices "Direct link to Placement of vertices")

#### Absolute Backing[​](#absolute-backing "Direct link to Absolute Backing")

The `ForceDirected` layout extends [AbsoluteLayout](/svelte/docs/diagrams/layouts/absolute.md), which means that, by default, the layout will defer to positions that are stored in the backing data for each vertex. This is a very useful feature for the majority of applications: you do not typically want the layout to run if a human being has already taken a look at the data and perhaps moved things around to be more to their liking.

##### Specifying Position[​](#specifying-position "Direct link to Specifying Position")

The default parameters used by `AbsoluteLayout` are, for Surfaces and Papers, `left` and `top`. So for instance you might have these nodes in your data:

```javascript
nodes:[
  { id:"1", left:50, top:150, label:"One" },
  { id:"2", left:150, top:250, label:"Two" }
]

```

For Diagrams the default positioning parameters are `x` and `y`.

By default, the Force Directed layout will honour these values if they are present, rather than processing the nodes.

If you do not wish to use `left` and `top`, you can provide your own `locationFunction`. This is discussed in the [documentation for the Absolute layout](/svelte/docs/diagrams/layouts/absolute.md#location-function).

##### Switching off Absolute backing[​](#switching-off-absolute-backing "Direct link to Switching off Absolute backing")

You can switch off Absolute backing via the `absoluteBacked` parameter:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { ForceDirectedLayout } from "@visuallyjs/browser-ui"
  const renderOptions = {
  layout: {
    type: ForceDirectedLayout.type,
    options: {
      absoluteBacked: false
    }
  }
}
</script>

<SurfaceComponent {renderOptions}/>

```

### Behaviour after relayout[​](#behaviour-after-relayout "Direct link to Behaviour after relayout")

A relayout will generate a brand new arrangement of elements, due to the fact that elements are placed randomly initially.

### Behaviour after refresh[​](#behaviour-after-refresh "Direct link to Behaviour after refresh")

A refresh of the layout locks the positions of any vertices that were positioned in a previous run of the layout, and these vertices do not move: only vertices that have not yet been positioned by the layout algorithm will move.

### Fine tuning positioning[​](#fine-tuning-positioning "Direct link to Fine tuning positioning")

For vertices without positioning information, the layout will optimise their placement relative to vertices to which they are connected, and ensure that vertices do not overlap.

When placing vertices dynamically, an initial random position is computed for each vertex. The bounding box that limits possible values for this random position is taken to be the size of the viewport in which the layout is being displayed, not the bounds of the dataset. This is to ensure that the new vertex appears somewhere the user can see it. Whilst initial positions are computed to lie within the bounds of the viewport, when the algorithm runs there is no reason that vertices won't be pushed out of the viewport.

The layout works by alternately pushing apart vertices so they do not overlap, and then pulling together vertices that have one or more edges between them. This is controlled by three parameters:

* **iterations** The maximum number of iterations to run through until accepting the state of the layout as it is. More iterations will typically result in a finer grained output, but will take longer. This defaults to 50.

* **spacing** This is the measure of how much padding you want to see between the vertices. It defaults to 250px. Note that the layout will never result in exactly this much padding between every vertex (unless, perhaps you have a very small number of vertices in the dataset); rather this number is your "ideal" padding, and the layout will strive to establish this amount of padding but will be constrained by the number of iterations it is allowed to run for and the complexity of the dataset.

* **r** This is a measure of how far each vertex will be moved when two vertices need to be repelled or attracted. Mathematically, this number is the ratio of the amount of travel applied to each vertex versus the amount of travel that would be applied for the two vertices to be spaced according to the value of `spacing`. It defaults to 0.25. Increasing this number will result in a shorter run time but the quality of the output will be degraded. Reducing this value can improve the quality of the output but you may find you also need to increase the number of iterations you allow the layout to run for.
