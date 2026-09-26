# Removing edges

There are a few ways to remove edges in VisuallyJs. On this page we'll discuss edge deletion in the UI, but it's also possible (and quite common) to remove an edge programmatically, for which we direct you to our [model docs](/react/docs/apps/model/edges.md#removing-edges).

## Removing via drag/drop[​](#removing-via-dragdrop "Direct link to Removing via drag/drop")

By default, VisuallyJs will let you grab an edge near one of its anchors and then drag it off the vertex. In the canvas below we have applied a CSS class to make these zones visible on hover; by default this does not occur (the CSS classes we target are `.vjs-connector-source-drag` and `.vjs-connector-target-drag`)

**********

Note: in the canvas above you cannot drop the edge back on to a vertex it was removed from, as the vertices are not marked up with the appropriate attributes to accept drag/drop edges.

## Rettaching[​](#rettaching "Direct link to Rettaching")

VisuallyJs's default behaviour is to discard any edges that a user has dropped in whitespace. You can override this via a setting:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  edges: {
    reattach: true
  }
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

In this canvas if you drag one end of the edge and drop it in whitespace VisuallyJs will reattach it:

**********

## Allowing unattached edges[​](#allowing-unattached-edges "Direct link to Allowing unattached edges")

In some circumstances you may wish to allow your users to detach edges and leave one end (or both ends in fact) of the edge unattached, but without removing the edge. You can do this by setting `allowUnattachedEdges`.

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

In the canvas below, when you drag an edge off a vertex, you can drop it in whitespace:

**********

## Disabling detach[​](#disabling-detach "Direct link to Disabling detach")

You can disable detach via mouse/touch events with the `detachable` setting in the `edges` options:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  edges: {
    detachable: false
  }
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

In this canvas VisuallyJs will not allow you to detach the edge using the mouse/touch events:

**********

How, then, could your users delete an edge via the UI? One solution is to specify a **deleteButton**.

## Showing a delete button[​](#showing-a-delete-button "Direct link to Showing a delete button")

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  edges: {
    detachable: false
  }
}

  const viewOptions = {
  edges: {
    default: {
      deleteButton: true
    }
  }
}
  return <SurfaceComponent renderOptions={renderOptions} viewOptions={viewOptions}/>
}

```

**********

The delete button will be assigned a CSS class of `.jtk-edge-delete`.

### Custom CSS class[​](#custom-css-class "Direct link to Custom CSS class")

You can provide one or more extra classes to set on the delete button via the `deleteButtonClass` property:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  edges: {
    detachable: false
  }
}

  const viewOptions = {
  edges: {
    default: {
      deleteButton: true,
      deleteButtonClass: "foo bar etc"
    }
  }
}
  return <SurfaceComponent renderOptions={renderOptions} viewOptions={viewOptions}/>
}

```

### Showing on hover only[​](#showing-on-hover-only "Direct link to Showing on hover only")

`deleteButton` can be specified either as a boolean, or as a constant that specifies its `visibility`. To have a delete button that only appears on hover, for example:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { OVERLAY_VISIBILITY_HOVER } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  edges: {
    detachable: false
  }
}

  const viewOptions = {
  edges: {
    default: {
      deleteButton: OVERLAY_VISIBILITY_HOVER
    }
  }
}
  return <SurfaceComponent renderOptions={renderOptions} viewOptions={viewOptions}/>
}

```

**********

### Managing edge removal[​](#managing-edge-removal "Direct link to Managing edge removal")

You may want to manage the removal of some specific edge - perhaps some condition is met in your app that means the edge cannot be removed, or perhaps you want to hit the server to confirm edge deletion first, etc. For that you can use the `deleteConfirm` property:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const renderOptions = {
  edges: {
    detachable: false
  }
}

  const viewOptions = {
  edges: {
    default: {
      deleteButton: true,
      deleteConfirm: (p, proceed) =>  {
      if(confirm('Delete edge?')) {
          proceed() 
      }     
    }
    }
  }
}
  return <SurfaceComponent renderOptions={renderOptions} viewOptions={viewOptions}/>
}

```

**********

The argument for `deleteConfirm` should be a function of this type:

EdgeDeleteConfirmationFunction

Definition of the function you can provide as `deleteConfirm` on an edge definition. VisuallyJs gives you the edge to be possibly deleted and the pointer event that instigated the deletion. If you wish to delete the edge you must invoke the `proceed()` function.

`(params:{
  e:Event,
  edge:Edge
}, proceed:() => any) => any`

You are given the edge that is a candidate for deletion, and the event that initiated the deletion. If you wish to confirm the edge removal, you must invoke the `proceed` method.
