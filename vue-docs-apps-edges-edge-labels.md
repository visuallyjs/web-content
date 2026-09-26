# Edge Labels

There are several properties on an edge mapping that you can use to configure labels for your edges.

## Static labels[​](#static-labels "Direct link to Static labels")

Here, we hardcode a label for every edge by setting it as a string on the default edge type:

```html
<script setup>

function viewOptions() {
  return {
  edges: {
    default: {
      label: "Edge"
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

```

**********

## Rotating labels[​](#rotating-labels "Direct link to Rotating labels")

By default, an edge label will be drawn horizontally. You can instruct VisuallyJs to rotate edge labels so that they match the angle of the connector at the point at which they are located via the `labelsRotatable` flag:

```html
<script setup>

function viewOptions() {
  return {
  edges: {
    default: {
      label: "Edge",
      labelsRotatable: true,
      targetMarker: "PlainArrow"
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

```

**********

### Strict rotation[​](#strict-rotation "Direct link to Strict rotation")

In the above example, the edge's source is to the right of the target, and so, strictly speaking, if the label were rotated to match the slope of the connector, it would be flipped. Since this is not easy to read for a user, by default we rotate labels in `"legible"` mode - when the angle of rotation lies between 90 and 270 degrees, we flip it.

If you want VisuallyJs to strictly honour the slope of the connector, you can set `strict` for `labelsRotatable`:

```html
<script setup>

function viewOptions() {
  return {
  edges: {
    default: {
      label: "Edge",
      labelsRotatable: "strict",
      targetMarker: "PlainArrow"
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

```

**********

## Dynamic labels[​](#dynamic-labels "Direct link to Dynamic labels")

You can extract the value of each edge's `label` from the edge's backing data:

```html
<script setup>

function viewOptions() {
  return {
  edges: {
    default: {
      label: "{{label}}"
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

```

**********

## Custom CSS class[​](#custom-css-class "Direct link to Custom CSS class")

You can provide your own class/classes to set on the element VisuallyJs uses for the edge label:

```html
<script setup>

function viewOptions() {
  return {
  edges: {
    default: {
      label: "{{label}}",
      labelClass: "myLabel"
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

```

Provide a space-separated list if you wish to provide more than one class.

## Label location[​](#label-location "Direct link to Label location")

By default, an edge label will be assigned a location of `0.5` - meaning it will be halfway along the edge path. You can change this by providing a `labelLocation` in your edge data:

```html
<script setup>

function viewOptions() {
  return {
  edges: {
    default: {
      label: "{{label}}",
      labelLocation: 0.25
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

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

```html
<script setup>

function viewOptions() {
  return {
  edges: {
    default: {
      label: "{{label}}"
    }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="viewOptions()" />
</template>

```

**********

instructed VisuallyJs to put the label at 0.25, and we did not need to set `labelLocation` in the edge mapping in the view.
