# Editing edge paths

VisuallyJs supports editing the path of edges for each of the different [connector types](/react/docs/apps/edges/connectors.md) that VisuallyJs ships with. The selection of the appropriate editor tool is managed automatically by VisuallyJs.

## Setup[​](#setup "Direct link to Setup")

To setup your app for path editing, you need to set the `editable` flag in the `edges` section of your render options:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  edges: {
    editable: true
  }
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

Once you've setup path editing you'll need to invoke it at some point, for which you need to invoke the `startEditingPath` method on your surface. One common way to do this is by responding to a tap or click event on an edge:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { EVENT_CLICK, DEFAULT } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const viewOptions = {
  edges: {
    [DEFAULT]: {
      events: {
        [EVENT_CLICK]: (p) => { p.ui.startEditingPath(p.edge) }
      }
    }
  }
}
  return <SurfaceComponent viewOptions={viewOptions}/>
}

```

The path editor will now stay active until you subsequently call `stopEditingPath()`. Another common setup for this is to do so in response to a click on a surface canvas (ie. a click on whitespace):

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { EVENT_CANVAS_CLICK, EVENT_CLICK, DEFAULT } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  events: {
    [EVENT_CANVAS_CLICK]: (p) => { p.renderer.stopEditingPath() }
  }
}

  const viewOptions = {
  edges: {
    [DEFAULT]: {
      events: {
        [EVENT_CLICK]: (p) => { p.ui.startEditingPath(p.edge) }
      }
    }
  }
}
  return <SurfaceComponent renderOptions={renderOptions} viewOptions={viewOptions}/>
}

```

Each editor offers a different interface for working with path edits.

## Orthogonal editors[​](#orthogonal-editors "Direct link to Orthogonal editors")

The orthogonal editor draws a handle on each segment of an edge, which can be dragged at 90 degrees to the direction of travel of the segment, ie. for a vertical segment, you can shift it horizontally, and for a horizontal segment you can shift it vertically.

When you are shifting a segment, if you release the mouse at such a point that the segment you just dragged forms a straight line with a previous or subsequent segment, the segments are coalesced into one. If you drag some segment such that an existing segment ceases to be a straight line, the segment is split and new segment is inserted between them.

#### Static anchors[​](#static-anchors "Direct link to Static anchors")

In this example we use an edge editor to edit the path of some edge whose anchors are at fixed points (in this case, `AnchorLocations.Bottom` and `AnchorLocations.Top`). We've also already called `startEditingPath(..)` on the surface for you:

**********

#### Dynamic anchors[​](#dynamic-anchors "Direct link to Dynamic anchors")

If the edge you are editing has [dynamic anchors](/react/docs/apps/edges/anchors.md#dynamic), the edge editor will draw a placeholder at each end of the edge, which you can drag around to any supported position for the given anchor - here we use the `AutoDefault` dynamic anchor, which is an anchor that has one position on each of the four sides of the element on which it resides:

**********

When you start to drag an anchor placeholder, you'll see VisuallyJs adds an element indicating an allowed position to which that anchor can be moved.

#### Continuous anchors[​](#continuous-anchors "Direct link to Continuous anchors")

If your edge is using anchor of type `AnchorLocations.Continuous` (which is the default), when you drag an anchor placeholder VisuallyJs will highlight the candidate face for the anchor relocation:

**********

#### User specified anchor positions[​](#user-specified-anchor-positions "Direct link to User specified anchor positions")

If you have specified `anchorPositions` for some given vertex in your view, eg:

```javascript
nodes:{
   default:{
       ...,
       anchorPositions:[
        { x:0, y:0.5, ox:-1, oy:0, id:"left" },
        { x:1, y:0.5, ox:1, oy:0, id:"right" },
        { x:0.5, y:0, ox:0, oy:-1, id:"top" },
        { x:0.5, y:1, ox:0, oy:1, id:"bottom" }
     ]
   }
}

```

...then the path editor will find these when you call `startEditingPath(...)`, and offer the ability to drag the end points of the edge to each of the available positions:

**********

### Avoiding vertices[​](#avoiding-vertices "Direct link to Avoiding vertices")

By default, the orthogonal connector editor will avoid getting into a situation where either end of the connector intersects the source or target vertex. This is best illustrated with a picture:

![Orthogonal connector avoiding vertices - VisuallyJs - build diagrams and rich visual UIs fast](/assets/images/orthogonal-vertex-avoid-9fcefb5d55b5b5adae49eab8cea35f12.gif)

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

![Orthogonal connector intersecting vertices - VisuallyJs - fully featured alternative to ReactFlow and ngDiagram](/assets/images/orthogonal-vertex-overlap-f3e8fb219b8294131ab7fbd8194b790f.gif)

Your users can still route the connector around in this setup but they'll have to move a lot more segments.

***

## Straight editors[​](#straight-editors "Direct link to Straight editors")

The straight editor draws a handle at the end of each segment of an edge, which can be dragged in any direction to alter its location. You can split a segment by clicking and holding the mouse at the location you wish to split the segment, and then dragging the new handle.

To delete a handle, click on it.

#### Static anchors[​](#static-anchors-1 "Direct link to Static anchors")

In this example we use an edge editor to edit the path of some edge whose anchors are at fixed points (in this case, `AnchorLocations.Right` and `AnchorLocations.Top`). We've also already called `startEditingPath(..)` for you:

**********

#### Dynamic anchors[​](#dynamic-anchors-1 "Direct link to Dynamic anchors")

If the edge you are editing has [dynamic anchors](/react/docs/apps/edges/anchors.md#dynamic), the edge editor will draw a placeholder at each end of the edge, which you can drag around to any supported position for the given anchor - here we use the `AutoDefault` dynamic anchor, which is an anchor that has one position on each of the four sides of the element on which it resides:

**********

When you start to drag an anchor placeholder, you'll see VisuallyJs adds an element indicating an allowed position to which that anchor can be moved.

#### Continuous anchors[​](#continuous-anchors-1 "Direct link to Continuous anchors")

If your edge is using anchor of type `AnchorLocations.Continuous`, when you drag an anchor placeholder VisuallyJs will highlight the candidate face for the anchor relocation:

**********

#### User specified anchor positions[​](#user-specified-anchor-positions-1 "Direct link to User specified anchor positions")

If you have specified `anchorPositions` for some given vertex in your view, eg:

```text
nodes:{
   default:{
       ...
       anchorPositions:[
        { x:0, y:0.5, ox:-1, oy:0, id:"left" },
        { x:1, y:0.5, ox:1, oy:0, id:"right" },
        { x:0.5, y:0, ox:0, oy:-1, id:"top" },
        { x:0.5, y:1, ox:0, oy:1, id:"bottom" }
     ]
   }
}

```

...then the path editor will find these when you call `startEditingPath(...)`, and offer the ability to drag the end points of the edge to each of the available positions:

**********

### Smoothed connectors[​](#smoothed-connectors "Direct link to Smoothed connectors")

When you have `smooth:true` set on your connector, the editor functions slightly differently - the drag handles now represent the location of the control points for the splines that make up the Bezier curve, and when you drag them, the control points are moved accordingly. Also when `smooth` is set, the editor draws a guideline for each segment.

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
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
  return <SurfaceComponent renderOptions={renderOptions}/>
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

surface.startEditingPath(someEdge, {
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
surface.startEditingPath(someEdge, {
  deleteButton:true
})

```

This results in:

**********

This will delete the edge without prompting the user. If you'd like to hook into the edge deletion, you can provide an `onMaybeDelete` function.

```javascript
surface.startEditingPath(someEdge, {
  deleteButton:true,
  onMaybeDelete:(edge, connection, doDelete) => {
      if (confirm(`Delete edge ${edge.id}?`)) {
          doDelete()
      }
  }
})

```

**********

Note that the operation is asynchronous - in the example above we use the windows `prompt` method, but you can invoke the `doDelete` callback at any stage.

## Clearing path edits[​](#clearing-path-edits "Direct link to Clearing path edits")

Edits made to a path can be cleared via `clearPathEdits` method on the `Surface` object.

```javascript
clearPathEdits (edgeOrConnection:string|Edge|Connection<BrowserElement>):boolean


```
