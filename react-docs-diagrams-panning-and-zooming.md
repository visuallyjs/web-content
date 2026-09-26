# Panning and zooming

VisuallyJs has the smoothest pan/zoom for miles around, and exposes a number of hooks for you to inject your own behaviour.

By default, the UI is setup to support an infinite canvas. This means the canvas element is positioned `absolute`, we set `overflow:hidden` on the container element (which disables the browser's scrolling mechanism), and the transform origin for the canvas is set to wherever the user last used the mouse or performed a pinch to zoom.

## Panning[​](#panning "Direct link to Panning")

In the default configuration, panning is performed by dragging the canvas with the mouse, or via touch, and more often than not you won't need to provide any `pan` options at all. If you want to, though, you can configure pan options via the `pan` property:

<!-- -->

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  pan: {
    axis: "x",
    useMetaKey: true
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

Auto pan

The default behaviour of the UI is to automatically pan the canvas whenever a vertex is dragged out of the viewport. We're mentioning it here as it is related to pan, but this is controlled in the vertex drag options.

For more information see [this page](/react/docs/apps/shapes/dragging#auto-pan).

### Filtering Panning[​](#filtering-panning "Direct link to Filtering Panning")

It's a fairly common use case that there be some set of elements in your canvas on which a drag should not cause a pan to occur. To handle this, the surface's pan options has the `filter` parameter. This is a function from which you should return true if you would like a pan to begin. You must return boolean true from this function in order for panning to be enabled.

<!-- -->

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  pan: {
    filter: (eventTarget:BrowserElement) => {
    return someLogic(eventTarget);
  }
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

### Pan Axis[​](#pan-axis "Direct link to Pan Axis")

The surface will pan in both the horizontal and vertical axes by default, as you might expect! But you can instruct the surface to pan only in one direction, should you wish to, via the `axis` property:

<!-- -->

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  pan: {
    axis: "x"
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

Valid values are `x`, `y` and `both` (which is the default).

### Panning with wheel[​](#panning-with-wheel "Direct link to Panning with wheel")

If you want to use the wheel for panning rather than zooming, you can:

<!-- -->

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  pan: {
    wheel: true
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

### Pan Options[​](#pan-options "Direct link to Pan Options")

PanOptions

Options to control how a user pans the canvas.

| Name        | Type                    | Description                                                                                                                                                                                        |
| ----------- | ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| axis?       | [PanAxis]()             | Optional axes in which to constrain pan - 'x', 'y' or 'both'. Defaults to 'both'.                                                                                                                  |
| enabled?    | boolean                 | Defaults to true, meaning panning is enabled.                                                                                                                                                      |
| filter?     | (el:Element) => boolean | Optional function which is called at the start of panning and can return false to reject pan starting.                                                                                             |
| useMetaKey? | boolean                 | Optional, defaults to false. When true, the user must hold down the meta key (ctrl on windows) in order to pan.                                                                                    |
| wheel?      | boolean                 | Defaults to false, meaning panning works via canvas drag. If you set this to true, the mousewheel (or move events on a touchpad) will pan the canvas. This will also override any zoom wheel flag. |

## Zooming[​](#zooming "Direct link to Zooming")

The canvas supports zooming both programmatically and via the mouse wheel (or pinch, on touch devices or a trackpad). A Surface has an associated `zoom range`, which is the minimum and maximum zoom that can be applied. When using the mouse wheel or pinch, these limits are applied automatically. If you attempt to set a zoom value outside of the zoom range programmatically (via `setZoom`), the zoom value will be clamped to the current range.

Zooming is configured via the `zoom` property.

<!-- -->

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  zoom: {
    range: [
      0.1,
      5
    ],
    step: 0.1
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

### Zoom options[​](#zoom-options "Direct link to Zoom options")

ZoomOptions

Options to control how a user manages zoom on the canvas.

| Name                  | Type          | Description                                                                                                                                                                                                                                          |
| --------------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| fixedTransformOrigin? | [PointXY]()   | Optional fixed transform origin for the canvas. Defaults to null.When this is supplied the zoom function does not change the transform origin You can still zoom and pan but the zoom/pan is applied relative to the top/left corner of the content. |
| initialValue?         | number        | Initial zoom value. Defaults to 1.                                                                                                                                                                                                                   |
| range?                | [ZoomRange]() | Zoom range to support. The default is \[0.05, 3]                                                                                                                                                                                                     |
| step?                 | number        | When zooming by step, this defines the change in zoom for each step. Defaults to 0.25.                                                                                                                                                               |
| wheel?                | boolean       | When true - which is the default - the wheel will be used for zoom.                                                                                                                                                                                  |

## Wheel[​](#wheel "Direct link to Wheel")

You configure whether the wheel manages pan or zoom inside the `pan` and `zoom` options. To configure the wheel's behaviour, use the `wheel` section of the render options.

### Filtering wheel events[​](#filtering-wheel-events "Direct link to Filtering wheel events")

If you want to control what parts of your UI respond to wheel events, you can do that in one of two ways.

#### CSS Filter[​](#css-filter "Direct link to CSS Filter")

`cssFilter` lets you provide a CSS3 selector identifying elements that should not fire wheel events.

<!-- -->

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  wheel: {
    cssFilter: ".someElementClass"
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

#### Filter[​](#filter "Direct link to Filter")

If you need more fine-grained control than just specifying a CSS selector, `filter` lets you provide a function which can determine whether or not a wheel event should fire.

<!-- -->

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  wheel: {
    filter: (e:MouseEvent) => { return someLogic(e) }
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

### Meta key[​](#meta-key "Direct link to Meta key")

By default, wheel events fire whenever the wheel is manipulated. If you wish, you can tell VisuallyJs only to respond to wheel events when the "meta" key (Ctrl on Windows/Linux, CMD on Mac) is pressed:

<!-- -->

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  wheel: {
    useMetaKey: true
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

### Wheel direction[​](#wheel-direction "Direct link to Wheel direction")

By default, wheel up zooms in and wheel down zooms out. If you want to switch that, set `reverse:true`, and then wheel up zooms out, and wheel down zooms in.

<!-- -->

```jsx

import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  wheel: {
    reverse: true
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

The full list of wheel options is:

WheelOptions

Options for how to respond to wheel events.

| Name               | Type                      | Description                                                                                                                                                                                                                                            |
| ------------------ | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| cssFilter?         | string                    | Optional CSS 3 selector to check if the wheel should be enabled for the current event target.                                                                                                                                                          |
| filter?            | (e:MouseEvent) => boolean | Optional function to call to check if wheel zooming should be enabled for the current event target.                                                                                                                                                    |
| reverse?           | boolean                   | Defaults to false. If true, the zoom direction is reversed: wheel up zooms out, and wheel down zooms in.                                                                                                                                               |
| sensitivity?       | number                    | How sensitive the wheel should be.                                                                                                                                                                                                                     |
| shiftToChangeMode? | boolean                   | Defaults to true. When true, holding the SHIFT key while using the mouse wheel will toggle the wheel's mode:<br />if the wheel is currently set to pan, it will zoom. If it is currently set to zoom, it will pan.                                     |
| useMetaKey?        | boolean                   | If true, the "meta" key (CMD on Mac, Ctrl on windows/linux) must be pressed in order for wheel zoom to operate. This can be useful if your UI fills the screen in one or more axes and your users would not be able to scroll past the Surface widget. |

Note that if you set `wheel: true` in `panOptions`, the mouse wheel will pan the canvas, and this will take precedence over any zoom wheel configuration.
