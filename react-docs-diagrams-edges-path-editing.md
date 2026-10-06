# Editing edge paths

VisuallyJs supports editing the path of edges for each of the different [connector types](/react/docs/diagrams/edges/connectors.md) that VisuallyJs ships with. The selection of the appropriate editor tool is managed automatically by VisuallyJs.

## Setup[​](#setup "Direct link to Setup")

In a diagram, edge path editing is enabled by default (as long as the diagram is not marked `editable:false`). If you want to disable path editing, without marking the diagram readonly, you need to set the `editable` flag in the `edges` section of your render options:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  edges: {
    editable: false
  }
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

Path editing begins when the user taps on an edge, and stays active until they click on whitespace, or perform some other operation such as editing a cell,

Each editor offers a different interface for working with path edits.

## Orthogonal editors[​](#orthogonal-editors "Direct link to Orthogonal editors")

The orthogonal editor draws a handle on each segment of an edge, which can be dragged at 90 degrees to the direction of travel of the segment, ie. for a vertical segment, you can shift it horizontally, and for a horizontal segment you can shift it vertically.

When you are shifting a segment, if you release the mouse at such a point that the segment you just dragged forms a straight line with a previous or subsequent segment, the segments are coalesced into one. If you drag some segment such that an existing segment ceases to be a straight line, the segment is split and new segment is inserted between them.

#### Static anchors[​](#static-anchors "Direct link to Static anchors")

In this example we use an edge editor to edit the path of some edge whose anchors are at fixed points (in this case, `AnchorLocations.Bottom` and `AnchorLocations.Top`). We've also already called `startEditingPath(..)` on the surface for you:

**********

#### Dynamic anchors[​](#dynamic-anchors "Direct link to Dynamic anchors")

If the edge you are editing has [dynamic anchors](/react/docs/diagrams/edges/anchors.md#dynamic), the edge editor will draw a placeholder at each end of the edge, which you can drag around to any supported position for the given anchor - here we use the `AutoDefault` dynamic anchor, which is an anchor that has one position on each of the four sides of the element on which it resides:

**********

When you start to drag an anchor placeholder, you'll see VisuallyJs adds an element indicating an allowed position to which that anchor can be moved.

#### Continuous anchors[​](#continuous-anchors "Direct link to Continuous anchors")

If your edge is using anchor of type `AnchorLocations.Continuous` (which is the default), when you drag an anchor placeholder VisuallyJs will highlight the candidate face for the anchor relocation:

**********

### Avoiding vertices[​](#avoiding-vertices "Direct link to Avoiding vertices")

By default, the orthogonal connector editor will avoid getting into a situation where either end of the connector intersects the source or target vertex. This is best illustrated with a picture:

![Orthogonal connector avoiding vertices - VisuallyJs - leading alternative to GoJS, JointJS, ReactFlow and SvelteFlow](/assets/images/orthogonal-vertex-avoid-9fcefb5d55b5b5adae49eab8cea35f12.gif)

info

This functionality is only applied to the segments at either end of a connector. If you have some connector path that intersects the source or target vertex somewhere in the middle of the path, the path will not be re-routed to avoid the vertex.

If you want to switch this behaviour off, you can do so in the connector spec:

```javascript
connector:{
    type:"Orthogonal",
    options:{
        vertexAvoidance:false
    }
}

```

This will be the resulting behaviour:

![Orthogonal connector intersecting vertices - VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](/assets/images/orthogonal-vertex-overlap-f3e8fb219b8294131ab7fbd8194b790f.gif)

Your users can still route the connector around in this setup but they'll have to move a lot more segments.

***

## Straight editors[​](#straight-editors "Direct link to Straight editors")

The straight editor draws a handle at the end of each segment of an edge, which can be dragged in any direction to alter its location. You can split a segment by clicking and holding the mouse at the location you wish to split the segment, and then dragging the new handle.

To delete a handle, click on it.

#### Static anchors[​](#static-anchors-1 "Direct link to Static anchors")

In this example we use an edge editor to edit the path of some edge whose anchors are at fixed points (in this case, `AnchorLocations.Right` and `AnchorLocations.Top`). We've also already called `startEditingPath(..)` for you:

**********

#### Dynamic anchors[​](#dynamic-anchors-1 "Direct link to Dynamic anchors")

If the edge you are editing has [dynamic anchors](/react/docs/diagrams/edges/anchors.md#dynamic), the edge editor will draw a placeholder at each end of the edge, which you can drag around to any supported position for the given anchor - here we use the `AutoDefault` dynamic anchor, which is an anchor that has one position on each of the four sides of the element on which it resides:

**********

When you start to drag an anchor placeholder, you'll see VisuallyJs adds an element indicating an allowed position to which that anchor can be moved.

#### Continuous anchors[​](#continuous-anchors-1 "Direct link to Continuous anchors")

If your edge is using anchor of type `AnchorLocations.Continuous`, when you drag an anchor placeholder VisuallyJs will highlight the candidate face for the anchor relocation:

**********

### Smoothed connectors[​](#smoothed-connectors "Direct link to Smoothed connectors")

When you have `smooth:true` set on your connector, the editor functions slightly differently - the drag handles now represent the location of the control points for the splines that make up the Bezier curve, and when you drag them, the control points are moved accordingly. Also when `smooth` is set, the editor draws a guideline for each segment.

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  edges: {
    editable: true,
    connector: {
      type: "Straight",
      options: {
        smooth: true
      }
    }
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

***

## Bezier editors[​](#bezier-editors "Direct link to Bezier editors")

The bezier editor draws two handles - one for each control point in the connector. They are placed where the control point is, and as you drag them around the control points are updated accordingly.

#### Static anchors[​](#static-anchors-2 "Direct link to Static anchors")

In this example we use an edge editor to edit the path of some edge whose anchors are at fixed points (in this case, `AnchorLocations.Bottom` and `AnchorLocations.Top`). We've also already called `startEditingPath(..)` on the surface for you:

**********

***

## QuadraticBezier editors[​](#quadraticbezier-editors "Direct link to QuadraticBezier editors")

The QuadraticBezier editor draws one handle, located at the connector's control point. As you drag the handle around, the connector's control point is updated.

**********

***

## Overlays[​](#overlays "Direct link to Overlays")

You can supply a set of overlays to render on an edge for the duration of the edit, for example:

```javascript

diagram.startEditingPath(someEdge, {
  overlays:[
    {
      type:LabelOverlay.type,
      options:{
        label:"editing...",
        location:0.1
      }
    }    
  ]
})

```

With this call we get a label overlay at location 0.1:

**********

## Delete button[​](#delete-button "Direct link to Delete button")

The edge path editor offers a shortcut method to attach a delete button:

```javascript
diagram.startEditingPath(someEdge, {
  deleteButton:true
})

```

This results in:

**********

This will delete the edge without prompting the user. If you'd like to hook into the edge deletion, you can provide an `onMaybeDelete` function.

```javascript
diagram.selectEdge(someEdge, {
  deleteButton:true,
  onMaybeDelete:(edge, connection, doDelete) => {
      if (confirm(`Delete edge ${edge.id}`)) {
          doDelete()
      }
  }
})

```

**********

Note that the operation is asynchronous - in the example above we use the windows `prompt` method, but you can invoke the `doDelete` callback at any stage.

## Clearing path edits[​](#clearing-path-edits "Direct link to Clearing path edits")

Edits made to a path can be cleared via `clearPathEdits` method on the `Diagram` object.

```javascript
clearPathEdits (edgeOrLink:Edge|DiagramLink):boolean


```
