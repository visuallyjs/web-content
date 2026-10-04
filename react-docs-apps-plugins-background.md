# Backgrounds

The surface widget supports the addition of backgrounds via a plugin. Two different background types are supported - images, and generated grids.

## Setup[​](#setup "Direct link to Setup")

As this is a plugin, you will provide its configuration in the `plugins` section of the render parameters for a surface.

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, SimpleBackground } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: SimpleBackground.type,
        url: "/img/351032562.jpg"
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

## Image backgrounds[​](#image-backgrounds "Direct link to Image backgrounds")

Images can be used as a background in one of two ways - either as an image that is retrieved in one piece and displayed, or as a set of tiles.

### Simple backgrounds[​](#simple-backgrounds "Direct link to Simple backgrounds")

These are backgrounds consisting of a single image, positioned at the Surface's origin. This type of background can be useful, for example, if you're building an app in which your users can markup drawings.

### Single image example[​](#single-image-example "Direct link to Single image example")

In this example (using the code shown above) we load a simple background, ie. a static image:

**********

Remember that we paste the image at the canvas origin, at its original size. So in this case the image has loaded but we cannot see all of it. It is possible to get a notification when the background image has loaded, though, so we can hook into that and have the image fully visible after load:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, SimpleBackground } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: SimpleBackground.type,
        url: "/img/351032562.jpg",
        onBackgroundReady: (bg, surface) => {
        surface.zoomToBackground()               
      }
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

**********

<!-- -->

### Tiled backgrounds[​](#tiled-backgrounds "Direct link to Tiled backgrounds")

This type of background consists of a set of tiles, which the Surface element requests from you as the canvas is panned and zoomed. This type of background has various usages: if you have a large background image, for instance, you may wish to serve it in pieces as the Surface needs it. Alternatively, you may wish to change the background based on the current zoom (in the way that Google maps does). Another great use for this type of background is to provide a grid for your canvas.

### Tiled image example[​](#tiled-image-example "Direct link to Tiled image example")

In this example we use a tiled background. Each of our tiles looks like this:

![VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](data:image/jpeg;base64,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)

When the surface has rendered, only the required tiles will have been loaded. If you tap on one of the nodes, the display will pan left and up by 350 pixels in each axis, and you will (probably) see new tiles appearing as they get loaded (unless the network is too fast for the load to be evident):

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, TiledBackground, TilingStrategies } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: TiledBackground.type,
        tiling: TilingStrategies.absolute,
        url: "/img/tiles/{z}/{x}_{y}.jpg",
        tileSize: {
          width: 200,
          height: 200
        },
        width: 800,
        height: 800,
        maxZoom: 0
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

**********

### Tiling strategies[​](#tiling-strategies "Direct link to Tiling strategies")

You may have noticed that in the example above we declared `tiling:TilingStrategies.absolute` in the background options. The tiled background supports two different approaches to the way tiles are arranged:

* `TilingStrategies.absolute` - Divides the entire image dimensions by the tile size. For instance, if you declare your background has a width and height of 800px, and your tiles are of width and height 50px, then - at zoom 0 - the background expects 16 tiles in each axis. At zoom 1, the expected value is doubled to 32, at zoom 2 it doubles again to 64, etc. With this strategy, each zoom level has the same number of tiles.

* `TilingStrategies.logarithmic` - With this strategy, there are (2^level+1) tiles in each axis. For instance at zoom 0, there are 2 tiles. At zoom 1 there are 4. At zoom 2, there are 8. Etc. This strategy is how applications like Google maps operate.

A tiled background is served as a series of layers, one for each zoom level supported. The number of zoom levels you intend to support is specified by the `maxZoom` option, which is a zero-indexed integer value. A value of 0 is the base value, covering the entire background. The background will determine which zoom level is appropriate based upon the current zoom of the surface.

There is no need to support any zoom level beyond 0; the background will retrieve tiles for the most appropriate level that is available to it, but serving up different tiles at different levels can allow you to implement things like serving more visual complexity the further a user zooms in.

### URL pattern[​](#url-pattern "Direct link to URL pattern")

The URL you supply for a tiled background should have a placeholder for each of `z` (zoom), `x` (index in horizontal axis) and `y` (index in vertical axis), as in the example above. In the above example we provided this url pattern:

```javascript
{
    url:"/img/tiles/{z}/{x}_{y}.jpg",
}

```

Tiles are zero-indexed, so, for example, the top left tile at zoom level 0 would, in the previous example, expand to this url:

```javascript
tiles/0/tile_0_0.png

```

The surface's tiled background does not support the concept of a "continuous world", in which tiles with negative indices may be requested.

### Clamping to the background image[​](#clamping-to-the-background-image "Direct link to Clamping to the background image")

Depending on your use case, you may wish to force the surface to clamp the pan/zoom such that some portion of the background image is always visible. You do this by setting the `clampToBackground` parameter on a `render` call:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, SimpleBackground } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  clampToBackground: true,
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: SimpleBackground.type,
        url: "myBackground.png"
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

### Zooming to the background image[​](#zooming-to-the-background-image "Direct link to Zooming to the background image")

If you wish to zoom out to the point that the entire background image is visible:

```javascript
surface.zoomToBackground()

```

***

## Generated grid backgrounds[​](#generated-grid-backgrounds "Direct link to Generated grid backgrounds")

Generated grid backgrounds place an SVG element into the background of the UI, repositioning and resizing it as needed as the bounds of your content changes. You can choose between a background using lines or dots. The default is for lines.

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, GeneratedGridBackground } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  grid: {
    size: {
      width: 50,
      height: 50
    }
  },
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: GeneratedGridBackground.type
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

**********

In this example we didn't specify the size of the grid in the background's options: the background will get this information from the surface, if possible. You can override the surface grid, however, should you wish to, or you may use the grid background on a surface that does not have a drag grid in effect.

### Dotted backgrounds[​](#dotted-backgrounds "Direct link to Dotted backgrounds")

The background in this example is rendered as lines, which is the default. Here's the same example with `gridType:GridTypes.dotted`:

**********

The full list of options for the generated grid background are:

GeneratedGridBackgroundOptions

Options for the generated grid background.

| Name               | Type                          | Description                                                                                                                                                                                                                                                                                                                                         |
| ------------------ | ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| autoShrink?        | boolean                       | Defaults to true, and instructs the grid that if the grid has grown beyond any minimum value set in either axis, if the content bounds subsequently shrink in that axis below the minimum, the grid should shrink back to the minimum. If you set this to false the grid will never shrink back to its minimum values once they have been exceeded. |
| dotRadius?         | number                        | The radius for dots representing grid positions (when gridType id GridTypes.dotted). Defaults to 2.                                                                                                                                                                                                                                                 |
| grid?              | [Grid]()                      | The grid to use. This is optional; if you do not supply one the background will attempt to read the grid definition from the Surface. If that is also not set then a default grid of 50x50 pixels will be used.                                                                                                                                     |
| gridType?          | [GridType]()                  | Type of grid - lines or dots. Defaults to lines.                                                                                                                                                                                                                                                                                                    |
| maxHeight?         | number                        | The maximum height for the grid. The value you provided is divided by 2 and then the grid is guaranteed to never exceed the range of (-maxHeight / 2) - (maxHeight / 2). maxHeight takes precedence over minHeight.                                                                                                                                 |
| maxWidth?          | number                        | The maximum width for the grid. The value you provided is divided by 2 and then the grid is guaranteed to never exceed the range of (-maxWidth / 2) - (maxWidth / 2). maxWidth takes precedence over minWidth.                                                                                                                                      |
| minHeight?         | number                        | The minimum height for the grid. The value you provided is divided by 2 and then the grid is guaranteed to always at least span the range of (-minHeight / 2) - (minHeight / 2). Defaults to 20 000.                                                                                                                                                |
| minWidth?          | number                        | The minimum width for the grid. The value you provided is divided by 2 and then the grid is guaranteed to always at least span the range of (-minWidth / 2) - (minWidth / 2). Defaults to 20 000.                                                                                                                                                   |
| onBackgroundReady? | [OnBackgroundReadyCallback]() | Optional function to call when the image has loaded (or otherwise claims to be ready)                                                                                                                                                                                                                                                               |
| showBorder?        | boolean                       | Whether or not to show a thick border around the entire background. Defaults to false.                                                                                                                                                                                                                                                              |
| showTickMarks?     | boolean                       | Defaults to false. If true, the grid will also draw tick marks between the grid lines.                                                                                                                                                                                                                                                              |
| tickDotRadius?     | number                        | The radius for dots representing grid tick marks (when gridType id GridTypes.dotted). Defaults to 1.                                                                                                                                                                                                                                                |
| tickMarksPerCell?  | number                        | Number of tick marks to draw per cell. Defaults to 2.                                                                                                                                                                                                                                                                                               |
| type               | string                        | Type of background to render.                                                                                                                                                                                                                                                                                                                       |
| visible?           | boolean                       | Whether or not the background is initially visible. Defaults to true.                                                                                                                                                                                                                                                                               |

### Autoscaling[​](#autoscaling "Direct link to Autoscaling")

The grid background has a minimum width and height, which are set by default to quite large numbers, and so users typically do not see the edges of the grid. However, you can supply your own `minWidth` and/or `minHeight` values, and if these are quite small with respect to the bounds of the dataset, VisuallyJs will autoscale the grid as necessary.

In this example we've set our grid minimum width and height to be 500 pixels. If you drag one of the nodes in the canvas below towards the edge of the grid, you'll see the grid expand in order to ensure there are always at least 2 grid squares between the content bounds and the edge of the grid. The grid will also shrink subsequently back to any minimum boundaries if the content bounds shrinks appropriately.

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, GeneratedGridBackground } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  grid: {
    size: {
      width: 50,
      height: 50
    }
  },
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: GeneratedGridBackground.type,
        minWidth: 500,
        minHeight: 500,
        autoShrink: false
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

**********

### Autoshrink[​](#autoshrink "Direct link to Autoshrink")

In the above example the grid scales up and down as the bounds of the content changes. If you wish, you can switch off the `autoShrink` functionality:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, GeneratedGridBackground } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  grid: {
    size: {
      width: 50,
      height: 50
    }
  },
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: GeneratedGridBackground.type,
        minWidth: 1500,
        minHeight: 1500,
        autoShrink: false
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

**********

### Tick marks[​](#tick-marks "Direct link to Tick marks")

By default, the grid will be drawn without tick marks in each cell. You can change this behaviour with the `showTickMarks` and `tickMarksPerCell` options. In this first example we show the tick marks:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, GeneratedGridBackground } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  grid: {
    size: {
      width: 50,
      height: 50
    }
  },
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: GeneratedGridBackground.type,
        showTickMarks: true
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

**********

In this next example, we leave the drag grid at 50x50 on the Surface, but we expand the background grid to 250x250, and request 4 tick marks per cell:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, GeneratedGridBackground } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  grid: {
    size: {
      width: 50,
      height: 50
    }
  },
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: GeneratedGridBackground.type,
        showTickMarks: true,
        tickMarksPerCell: 5,
        grid: {
          width: 250,
          height: 250
        }
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

**********

### Grid border[​](#grid-border "Direct link to Grid border")

You can add a border to the background grid with the `showBorder` option:

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { BackgroundPlugin, GeneratedGridBackground } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  grid: {
    size: {
      width: 50,
      height: 50
    }
  },
  plugins: [
    {
      type: BackgroundPlugin.type,
      options: {
        type: GeneratedGridBackground.type,
        minWidth: 1500,
        minHeight: 1500,
        showBorder: true
      }
    }
  ]
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

**********

### CSS classes[​](#css-classes "Direct link to CSS classes")

VisuallyJs exposes a number of CSS classes to assist you in managing the appearance of grid backgrounds.

| Class                              | Description                                                                                                                   |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `vjs-background`                   | The css class that will be added to a grid background's main element                                                          |
| `vjs-background-border`            | The css class that will be added to a grid background's border                                                                |
| `vjs-background-grid`              | The css class that will be added to the major and minor dots/lines in a grid background                                       |
| `vjs-background-grid-dotted-major` | The class that will be added to the dots representing a grid background's grid lines (when gridType is GridTypes.dotted)      |
| `vjs-background-grid-dotted-minor` | The class that will be added to the dots representing a grid background's grid tick marks (when gridType is GridTypes.dotted) |
| `vjs-background-grid-major`        | The class that will be added to the lines representing a grid background's grid lines (when gridType is GridTypes.lines)      |
| `vjs-background-grid-minor`        | The class that will be added to the lines representing a grid background's tick marks (when gridType is GridTypes.lines)      |

***
