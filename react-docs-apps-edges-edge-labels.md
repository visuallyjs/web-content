# Edge Labels

There are several properties on an edge mapping that you can use to configure labels for your edges.

## Static labels[​](#static-labels "Direct link to Static labels")

Here, we hardcode a label for every edge by setting it as a string on the default edge type:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const viewOptions = {
  edges: {
    default: {
      label: "Edge"
    }
  }
}
  return <SurfaceComponent viewOptions={viewOptions}/>
}

```

**********

## Rotating labels[​](#rotating-labels "Direct link to Rotating labels")

By default, an edge label will be drawn horizontally. You can instruct VisuallyJs to rotate edge labels so that they match the angle of the connector at the point at which they are located via the `labelsRotatable` flag:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const viewOptions = {
  edges: {
    default: {
      label: "Edge",
      labelsRotatable: true,
      targetMarker: "PlainArrow"
    }
  }
}
  return <SurfaceComponent viewOptions={viewOptions}/>
}

```

**********

### Strict rotation[​](#strict-rotation "Direct link to Strict rotation")

In the above example, the edge's source is to the right of the target, and so, strictly speaking, if the label were rotated to match the slope of the connector, it would be flipped. Since this is not easy to read for a user, by default we rotate labels in `"legible"` mode - when the angle of rotation lies between 90 and 270 degrees, we flip it.

If you want VisuallyJs to strictly honour the slope of the connector, you can set `strict` for `labelsRotatable`:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const viewOptions = {
  edges: {
    default: {
      label: "Edge",
      labelsRotatable: "strict",
      targetMarker: "PlainArrow"
    }
  }
}
  return <SurfaceComponent viewOptions={viewOptions}/>
}

```

**********

## Dynamic labels[​](#dynamic-labels "Direct link to Dynamic labels")

You can extract the value of each edge's `label` from the edge's backing data:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const viewOptions = {
  edges: {
    default: {
      label: "{{label}}"
    }
  }
}
  return <SurfaceComponent viewOptions={viewOptions}/>
}

```

**********

## Custom CSS class[​](#custom-css-class "Direct link to Custom CSS class")

You can provide your own class/classes to set on the element VisuallyJs uses for the edge label:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const viewOptions = {
  edges: {
    default: {
      label: "{{label}}",
      labelClass: "myLabel"
    }
  }
}
  return <SurfaceComponent viewOptions={viewOptions}/>
}

```

Provide a space-separated list if you wish to provide more than one class.

## Label location[​](#label-location "Direct link to Label location")

By default, an edge label will be assigned a location of `0.5` - meaning it will be halfway along the edge path. You can change this by providing a `labelLocation` in your edge data:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const viewOptions = {
  edges: {
    default: {
      label: "{{label}}",
      labelLocation: 0.25
    }
  }
}
  return <SurfaceComponent viewOptions={viewOptions}/>
}

```

**********

You can also control this via a `labelLocation` value in your edge's backing data. For example, this edge:

```javascript
{
    source:"someNode",
    target:"someOtherNode",
    data:{
        labelLocation:0.25
    }
}

```

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

export default function MyComponent() {

  const viewOptions = {
  edges: {
    default: {
      label: "{{label}}"
    }
  }
}
  return <SurfaceComponent viewOptions={viewOptions}/>
}

```

**********

instructed VisuallyJs to put the label at 0.25, and we did not need to set `labelLocation` in the edge mapping in the view.
