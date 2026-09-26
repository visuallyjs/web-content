# Absolute Layout

This layout, by default, retrieves positioning values from the `left` and `top` values in your vertex data and uses these as the \`left\` and \`top\` CSS properties in the DOM. However, you can provide your own function to extract appropriate values, should you need to.

For applications in which the positions of the nodes is determined by your users, the `Absolute` layout is a good choice. If you need to render a dataset that a human being has never manipulated, you can use the [ForceDirected layout](./force-directed), which extends the `Absolute` layout and only calculates a position for vertices that do not have values set for their position.

This is the default layout used by VisuallyJs.

<!-- -->

<!-- -->

## Parameters[​](#parameters "Direct link to Parameters")

AbsoluteLayoutParameters

Constructor parameters for an AbsoluteLayout.

| Name              | Type                 | Description                                                                                                    |
| ----------------- | -------------------- | -------------------------------------------------------------------------------------------------------------- |
| absoluteBacked?   | boolean              | Defaults to false. If true, then the layout will use any position values found in the data for a given vertex. |
| height?           | number               | Optional fixed height for the layout.                                                                          |
| locationFunction? | [LocationFunction]() | Optional function that, given some vertex, can provide the x/y location of the vertex on the canvas            |
| padding?          | [PointXY]()          | Optional padding to put around the elements.                                                                   |
| width?            | number               | Optional fixed width for the layout.                                                                           |

## Calculation of location[​](#calculation-of-location "Direct link to Calculation of location")

#### Location Function[​](#location-function "Direct link to Location Function")

If you provide a `locationFunction`, it will be passed each vertex and is expected to return a position for the given vertex in the form `{x:number, y:number}`

```javascript
locationFunction:(v:Vertex):PointXY =>{
  return {x:node.data.xPosition, y:node.data.yPosition }
}

```

### Location inside a group[​](#location-inside-a-group "Direct link to Location inside a group")

If a node is a child of a group, when the group performs a layout of its child nodes, it will pass itself as the second argument to the location function:

```javascript
locationFunction:(v:Vertex, parent:Group):PointXY =>{
  // perhaps here you want to do something unique to each group
}

```

`group` is only ever assigned a value during the group layout phase. When processing the layout of nodes and groups, `group` will be null.

## Positioning properties[​](#positioning-properties "Direct link to Positioning properties")

For Surface/Paper UIs the default positioning properties are `left` and `top`, for instance:

```json
{
  "id": "node1",
  "left": 50,
  "top": 250
}

```

For Diagram UIs the default positioning properties are `x` and `y`:

```json
{
  "id": "node1",
  "type": "process",
  "x": 50,
  "y": 250
}

```
