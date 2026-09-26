# Line crossings

The line crossings plugin draws bridge when two orthogonal connectors cross. By default this bridge is painted as an arc (on either the vertical or horizontal segment), but you can also show a gap in one connector, or mark the intersection with a dot.

info

This plugin requires that your edges are painted using Orthogonal connectors.

**********

## Instantiation[​](#instantiation "Direct link to Instantiation")

The line crossings plugin can be activated for a diagram in its options:

```jsx
import { CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  lineCrossings: true,
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

This will draw arch bridges on the horizontal segment at each intersection.

## Bridge type[​](#bridge-type "Direct link to Bridge type")

The "bridge" is the artifact that the plugin draws to mark a crossing, and can be "dot", "arch" or "gap".

### Arch[​](#arch "Direct link to Arch")

This is the default bridge type. The arch is drawn on the segment that matches the orientation the plugin is setup for (see below for a discussion of orientation).

```jsx
import { CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  lineCrossings: {
    orientation: "h",
    bridgeType: "arch"
  },
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

### Gap[​](#gap "Direct link to Gap")

This bridge type draws a gap in the edge that is not in the axis that the plugin is configured for. In the canvas below, the plugin is using "h" - horizontal - axis, and so the horizontal segment is drawn but the vertical segment has a gap.

```jsx
import { CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  lineCrossings: {
    orientation: "h",
    bridgeType: "gap"
  },
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

### Dot[​](#dot "Direct link to Dot")

This bridge type draws a dot at each intersection. By default, the dot has a radius of 5px, and is painted the same color as the segment in the plugin's orientation.

```jsx
import { CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  lineCrossings: {
    orientation: "h",
    bridgeType: "dot"
  },
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

#### Changing radius and color[​](#changing-radius-and-color "Direct link to Changing radius and color")

```jsx
import { CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  lineCrossings: {
    orientation: "h",
    bridgeType: "dot",
    dotRadius: 10,
    dotColor: "forestgreen"
  },
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

## Orientation[​](#orientation "Direct link to Orientation")

The plugin operates in either the horizontal ("h") or vertical ("v") axis. Behaviour of the different bridge types with respect to the axis is discussed above. The default is to use the horizontal axis, but this can be changed:

```jsx
import { CONNECTOR_TYPE_ORTHOGONAL } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  lineCrossings: {
    orientation: "v",
    bridgeType: "arch"
  },
  edges: {
    connector: CONNECTOR_TYPE_ORTHOGONAL
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

**********

## Editable paths[​](#editable-paths "Direct link to Editable paths")

The plugin works seamlessly with the path editor. Each of the canvases above are setup to start edit on click, but here we've done it for you - try moving a segment and see how the bridges update:

**********

## SVG Export[​](#svg-export "Direct link to SVG Export")

The bridges drawn by the plugin are included in the output of the SVG exporter. Try clicking one of the export buttons on this canvas:

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
