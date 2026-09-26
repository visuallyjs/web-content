# Line crossings

The line crossings plugin draws bridge when two orthogonal connectors cross. By default this bridge is painted as an arc (on either the vertical or horizontal segment), but you can also show a gap in one connector, or mark the intersection with a dot.

info

This plugin requires that your edges are painted using Orthogonal connectors.

**********

## Instantiation[​](#instantiation "Direct link to Instantiation")

The line crossings plugin can be specified in the `plugins` of the render options for some surface/paper. To use the defaults, you need only specify the plugin name:

```javascript
import { newInstance, PLUGIN_TYPE_LINE_CROSSINGS, CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    PLUGIN_TYPE_LINE_CROSSINGS
  ],
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
})

```

This will draw arch bridges on the horizontal segment at each intersection.

## Bridge type[​](#bridge-type "Direct link to Bridge type")

The "bridge" is the artifact that the plugin draws to mark a crossing, and can be "dot", "arch" or "gap".

### Arch[​](#arch "Direct link to Arch")

This is the default bridge type. The arch is drawn on the segment that matches the orientation the plugin is setup for (see below for a discussion of orientation).

```javascript
import { newInstance, PLUGIN_TYPE_LINE_CROSSINGS, CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: PLUGIN_TYPE_LINE_CROSSINGS,
      options: {
        orientation: "h",
        bridgeType: "arch"
      }
    }
  ],
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
})

```

**********

### Gap[​](#gap "Direct link to Gap")

This bridge type draws a gap in the edge that is not in the axis that the plugin is configured for. In the canvas below, the plugin is using "h" - horizontal - axis, and so the horizontal segment is drawn but the vertical segment has a gap.

```javascript
import { newInstance, PLUGIN_TYPE_LINE_CROSSINGS, CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: PLUGIN_TYPE_LINE_CROSSINGS,
      options: {
        orientation: "h",
        bridgeType: "gap"
      }
    }
  ],
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
})

```

**********

### Dot[​](#dot "Direct link to Dot")

This bridge type draws a dot at each intersection. By default, the dot has a radius of 5px, and is painted the same color as the segment in the plugin's orientation.

```javascript
import { newInstance, PLUGIN_TYPE_LINE_CROSSINGS, CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: PLUGIN_TYPE_LINE_CROSSINGS,
      options: {
        orientation: "h",
        bridgeType: "dot"
      }
    }
  ],
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
})

```

**********

#### Changing radius and color[​](#changing-radius-and-color "Direct link to Changing radius and color")

```javascript
import { newInstance, PLUGIN_TYPE_LINE_CROSSINGS, CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: PLUGIN_TYPE_LINE_CROSSINGS,
      options: {
        orientation: "h",
        bridgeType: "dot",
        dotRadius: 10,
        dotColor: "forestgreen"
      }
    }
  ],
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
})

```

**********

## Orientation[​](#orientation "Direct link to Orientation")

The plugin operates in either the horizontal ("h") or vertical ("v") axis. Behaviour of the different bridge types with respect to the axis is discussed above. The default is to use the horizontal axis, but this can be changed:

```javascript
import { newInstance, PLUGIN_TYPE_LINE_CROSSINGS, CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: PLUGIN_TYPE_LINE_CROSSINGS,
      options: {
        orientation: "v",
        bridgeType: "arch"
      }
    }
  ],
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
})

```

**********

## Editable paths[​](#editable-paths "Direct link to Editable paths")

The plugin works seamlessly with the path editor. Each of the canvases above are setup to start edit on click, but here we've done it for you - try moving a segment and see how the bridges update:

**********

## SVG Export[​](#svg-export "Direct link to SVG Export")

The bridges drawn by the plugin are included in the output of the SVG exporter

Export :*[SVG](#)**[PNG](#)**[JPG](#)*

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

Line crossings are drawn as SVG elements, and several CSS classes are exposed to allow you to control their appearance.

| Class                   | Description                                                                                               |
| ----------------------- | --------------------------------------------------------------------------------------------------------- |
| `vjs-bridge`            | Assigned to all bridges (of any type) that mark a line crossing.                                          |
| `vjs-bridge-arch`       | Assigned to all arch bridges that mark a line crossing.                                                   |
| `vjs-bridge-dot`        | Assigned to all dot bridges that mark a line crossing.                                                    |
| `vjs-bridge-gap`        | Assigned to all gap bridges that mark a line crossing.                                                    |
| `vjs-bridge-horizontal` | Assigned to all bridges (of any type) that mark a line crossing when the bridge is on the horizontal axis |
| `vjs-bridge-vertical`   | Assigned to all bridges (of any type) that mark a line crossing when the bridge is on the vertical axis   |

LineCrossingsPluginOptions

Options for the line crossings plugin.

| Name        | Type                                                                              | Description                                                                                                                                                                                                                                                                |
| ----------- | --------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| bridgeType  | "gap" \| "dot" \| "arch"                                                          | Type of bridge to use. Defaults to 'arch'.                                                                                                                                                                                                                                 |
| dotColor?   | string                                                                            | Color to use for dot bridges. Defaults to null, and the dot is painted with the stroke color of the dominant segment. You can also control this via the CSS class defined by the constant CLASS\_LINE\_CROSSING\_BRIDGE\_DOT, but using CSS will be lost in an SVG export. |
| dotRadius?  | number                                                                            | Radius to use for dot bridges. Defaults to 5.                                                                                                                                                                                                                              |
| onTap?      | (edge1:[Edge](), edge2:[Edge](), canvasLocation:[PointXY](), e:MouseEvent) => any | Optional function to invoke when the user taps on a bridge. This will only fire for bridge types that draw extra components - arch and dot - but the gap bridge just masks                                                                                                 |
| orientation | "v" \| "h"                                                                        | Whether to apply the bridge to the horizontal or the vertical segment in a crossing. Defaults to horizontal.                                                                                                                                                               |
