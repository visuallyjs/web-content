# Vertex avoidance

You can instruct VisuallyJs to attempt to route edges around vertices, either for all edges in your app or just for some specific type(s) of edge.

## Example[​](#example "Direct link to Example")

```html
<script setup>


const options = {
  edges: {
    connector: "Orthogonal",
    avoidVertices: true
  },
  grid: {
    size: {
      width: 20,
      height: 20
    }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

**********

The key option being `avoidVertices` in the `edges` config. Internally, vertex avoidance is computed using an A\* algorithm, which is based upon a grid, and so we do recommend you use a `grid` in your app if you've got `avoidVertices` set. Without a grid set you can sometimes see an effect where a path segment's location changes as you drag an element, and then snaps back to some multiple of the A\* grid. The A\* grid has a cell size of 10 pixels and so the best results are obtained from setting your own grid to a multiple of that.

## Path constrainment[​](#path-constrainment "Direct link to Path constrainment")

You can constrain the travel of the path in a few different ways.

### Orthogonal routing[​](#orthogonal-routing "Direct link to Orthogonal routing")

Orthogonal routing constrains path segments to travel either horizontally or vertically, as shown at the top of the page.

```html
<script setup>


const options = {
  edges: {
    avoidVertices: true,
    targetMarker: "Arrow",
    connector: {
      type: "Straight",
      options: {
        constrain: "orthogonal"
      }
    }
  },
  zoomToFit: true,
  grid: {
    size: {
      width: 20,
      height: 20
    }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

**********

### Any angle[​](#any-angle "Direct link to Any angle")

```html
<script setup>


const options = {
  edges: {
    avoidVertices: true,
    targetMarker: "Arrow",
    connector: {
      type: "Straight",
      options: {
        constrain: "none"
      }
    }
  },
  grid: {
    size: {
      width: 20,
      height: 20
    }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

With this setup path segments can travel at any angle:

**********

### Smooth connectors[​](#smooth-connectors "Direct link to Smooth connectors")

For some applications the above can look a little jerky, and so one thing you can do is set `smooth` on your connector, to get that Graphviz effect:

```html
<script setup>


const options = {
  edges: {
    avoidVertices: true,
    targetMarker: "Arrow",
    connector: {
      type: "Straight",
      options: {
        smooth: true
      }
    }
  },
  zoomToFit: true,
  grid: {
    size: {
      width: 20,
      height: 20
    }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

**********

info

Straight connectors with `smooth:true` set are aliased in VisuallyJs to the connector name `Smooth`:

```html
<script setup>


const options = {
  edges: {
    avoidVertices: true,
    connector: "Smooth"
  },
  grid: {
    size: {
      width: 20,
      height: 20
    }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

### Metro routing[​](#metro-routing "Direct link to Metro routing")

"Metro" routing constrains path segments to travel either horizontally, vertically, or at 45 degrees.

```html
<script setup>


const options = {
  edges: {
    avoidVertices: true,
    targetMarker: "Arrow",
    connector: {
      type: "Straight",
      options: {
        constrain: "metro"
      }
    }
  },
  zoomToFit: true,
  grid: {
    size: {
      width: 20,
      height: 20
    }
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

**********
