# Unattached edges

By default, edges are expected to have a `source` and `target` vertex. But there are some use cases - in particular when diagramming - where you may want to support edges where the source and/or target of the edge is in whitespace and not attached to a vertex.

## Configuration[​](#configuration "Direct link to Configuration")

Unattached edges are switched off by default. To turn them on, set `allowUnattached` in your render options:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  edges: {
    allowUnattached: true
  }
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

**********

## Data model[​](#data-model "Direct link to Data model")

When an edge is unattached at the source or target, the data object for the replaces the ID of a vertex with a point on the canvas. In the example above, for instance, the dataset looks like this:

```javascript
{
  nodes:[
    { id:"1", left:50, top:50 },
    { id:"2", left:250, top:250 }
  ], 
  edges:[
    { source:"1", target:{x:80, y:230} }
  ]
}

```

## Rettaching an unattached edge[​](#rettaching-an-unattached-edge "Direct link to Rettaching an unattached edge")

You can relocate an unattached edge in the same way as an edge that is connected to a vertex - VisuallyJs writes a drag handle at the source and target which is not visible (although it could be, if you wanted, via CSS), but which changes the cursor on hover.

Here's the same example as before, but we've applied a few CSS styles so that you can see the hidden elements - the blue boxes are the handles with which you can drag the edge; the red box is the dummy element.

```css
    .vjs-connector-target-drag {
        fill:cornflowerblue;
    }
    
    .vjs-connector-source-drag {
        fill:cornflowerblue;
    }

    .vjs-dummy-vertex {
        width:10px !important;
        height:10px !important;
        background-color:orangered;
    }

```

**********

If you drag the edge to the unconnected vertex you'll see the dummy vertex gets removed from the canvas. Dragging it off and dropping it on whitespace will cause a new dummy vertex to be added at the appropriate location.
