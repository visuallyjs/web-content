# Vertex avoidance

You can instruct VisuallyJs to attempt to route edges around vertices, either for all edges in your app or just for some specific type(s) of edge.

## Example[​](#example "Direct link to Example")

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
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
})

```

**********

The key option being `avoidVertices` in the `edges` config. Internally, vertex avoidance is computed using an A\* algorithm, which is based upon a grid, and so we do recommend you use a `grid` in your app if you've got `avoidVertices` set. Without a grid set you can sometimes see an effect where a path segment's location changes as you drag an element, and then snaps back to some multiple of the A\* grid. The A\* grid has a cell size of 10 pixels and so the best results are obtained from setting your own grid to a multiple of that.

## Path constrainment[​](#path-constrainment "Direct link to Path constrainment")

You can constrain the travel of the path in a few different ways.

### Orthogonal routing[​](#orthogonal-routing "Direct link to Orthogonal routing")

Orthogonal routing constrains path segments to travel either horizontally or vertically, as shown at the top of the page.

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  edges: {
    avoidVertices: true,
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
})

```

**********

### Any angle[​](#any-angle "Direct link to Any angle")

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  edges: {
    avoidVertices: true,
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
})

```

With this setup path segments can travel at any angle:

**********

### Smooth connectors[​](#smooth-connectors "Direct link to Smooth connectors")

For some applications the above can look a little jerky, and so one thing you can do is set `smooth` on your connector, to get that Graphviz effect:

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  edges: {
    avoidVertices: true,
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
})

```

**********

info

Straight connectors with `smooth:true` set are aliased in VisuallyJs to the connector name `Smooth`:

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
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
})

```

### Metro routing[​](#metro-routing "Direct link to Metro routing")

"Metro" routing constrains path segments to travel either horizontally, vertically, or at 45 degrees.

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  edges: {
    avoidVertices: true,
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
})

```

**********

***

## Applying to specific edge types only[​](#applying-to-specific-edge-types-only "Direct link to Applying to specific edge types only")

If you want to setup your app such that only specific edge types will use the A\* router, you can do this via your view. In this example, we map two edge types, and the `orthogonal` edge type has this key set:

```javascript
{
    avoidVertices:true
}

```

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  edges: {
    connector: {
      type: "Straight",
      options: {
        constrain: "orthogonal"
      }
    }
  },
  grid: {
    size: {
      width: 20,
      height: 20
    }
  },
  view: {
    edges: {
      straight: {
        connector: "Straight",
        paintStyle: {
          stroke: "red",
          strokeWidth: 2
        }
      },
      orthogonal: {
        avoidVertices: true,
        connector: "Orthogonal",
        paintStyle: {
          stroke: "red",
          strokeWidth: 2
        }
      }
    }
  }
})

```

So the red lines - with the straight connector - travel through vertices without avoiding them, while the green lines route themselves around vertices:

**********

## Routing considerations[​](#routing-considerations "Direct link to Routing considerations")

To get the best results from the edge avoidance routine, it's helpful to understand what's happening under the hood.

Path computation is a two stage process:

1. First, we compute a path through the A\* grid;
2. We then convert that path into what the user sees.

### Borders and Buffers[​](#borders-and-buffers "Direct link to Borders and Buffers")

For each vertex, VisuallyJs assigns a border and a buffer. The element below is 100 pixels wide by 80 pixels high. The green border is 20 pixels in width, and the orangered buffer is also 20 pixels in width.

In the first phase of path computation - computing a path through the grid - **both the `border` and `buffer` are taken into account**. Paths are computed such that they do not pass through any vertex or its border or buffer. The second phase of path computation - converting the grid path to what the user sees - **only avoids passing through the `border` zone**. Paths are allowed to travel through any element's buffer.

This two-pass approach provides a balance between clearance of vertices and the visual smoothness of the final path. Including border and buffer in the first pass encourages the grid search to choose routes that provide breathing space around vertices; relaxing the buffer constraint in the second pass gives the renderer more leeway to simplify bends or to smooth corners.

### Specifying border, buffer and cell size[​](#specifying-border-buffer-and-cell-size "Direct link to Specifying border, buffer and cell size")

You can fine-tune the behaviour of the edge avoidance routine with three edge options:

BrowserUIEdgeOptions

Common options for edges in the Browser UI package.

| Name               | Type   | Description                                                                                                                                                                                                                                                                                                                               |
| ------------------ | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| astarGridCellSize? | number | Size of each cell in the grid that the AStar routine uses to calculate paths that avoid vertices. This defaults to 10 pixels and is not something you'll really need to change. If you do change it, keep in mind that a) a smaller grid size increases the runtime of the routine, and b) a large grid size will render the UI unusable. |
| astarVertexBuffer? | number | Number of cells to pad each vertex with that act as its buffer: edges will be routed around the buffer wherever possible. Defaults to 2 - but note this value is added the vertex border, whose default is 2, so the computed default is 4 grid cells.                                                                                    |
| astarVertexBorder? | number | Number of cells to pad each vertex with that act as its border: edges will be routed around the border wherever possible. Defaults to 2                                                                                                                                                                                                   |

You set these in the `edges` section of your `renderOptions`:

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  edges: {
    astarGridCellSize: 20,
    astarVertexBorder: 1,
    astarVertexBuffer: 2
  }
})

```
