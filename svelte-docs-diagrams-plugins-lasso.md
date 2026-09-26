# Lasso

The lasso plugin allows users to select nodes, group and edges with the mouse. We've activated it on page load so you can try it out below. After you've tried it once the surface will revert to pan mode and you'll need to select the lasso from the controls.

Any vertices snagged by your lasso are added to the model's current selection.

The lasso works like the lasso in AutoCAD: when you drag from left to right, any vertices that intersect with your lasso are added to the selection. When you drag from right to left, though, only vertices that your lasso fully encloses are added to the selection.

When the user lassos outside of the visible area, the lasso will automatically pan the canvas.

**********

## Setup[​](#setup "Direct link to Setup")

The lasso plugin does not need any options set in order to function, so the simplest setup is just to reference it in the plugin list:

<!-- -->

```html
<script>
import { LassoPlugin } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  lasso: true
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

## Mask lasso[​](#mask-lasso "Direct link to Mask lasso")

The lasso, by default, draws a rectangle over the canvas, but VisuallyJs can also draw the lasso as a set of overlays which mask the whole browser window except for the lassoed area - to do this, set `invert:true`:

**********

<!-- -->

```html
<script>
import { LassoPlugin } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  lasso: {
    invert: true
  }
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

## Auto arm[​](#auto-arm "Direct link to Auto arm")

From 1.2.4 onwards the lasso supports the concept of "auto arm" - the lasso will arm itself if the user long-presses on the canvas. Try pressing and holding the left mouse button on this canva. After 500ms, you will see the controls component switch to show that the lasso is engaged:

**********

<!-- -->

```html
<script>
import { LassoPlugin } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  lasso: {
    autoArm: true
  }
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

### Auto arm timeout[​](#auto-arm-timeout "Direct link to Auto arm timeout")

The default timeout is 500ms before the lasso will arm itself. In some use cases you might want to reduce that time, which you can do via the `armTimeout` option on the lasso. One such use case, for instance, is when you've setup your canvas to use the wheel for pan instead of zoom - in the canvas below, the wheel pans the content, and the `armTimeout` is set to 0 for the lasso, so it switches on as soon as you begin to drag with the left mouse button:

**********

<!-- -->

```html
<script>
import { LassoPlugin } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  pan: {
    wheel: true
  },
  lasso: {
    autoArm: true,
    armTimeout: 0
  }
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

You can also, of course, choose to reduce the `armTimeout` without altering the behaviour of the wheel.

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

| Class                   | Description                                                                                                                                                                                                         |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-lasso`             | Assigned to the DOM element representing a lasso                                                                                                                                                                    |
| `vjs-lasso-mask`        | Assigned to each DOM element representing part of the lasso mask, when the lasso is inverted mode. The lasso mask consists of four parts, one to the left, right, top and bottom of the area that has been lassoed. |
| `vjs-lasso-mask-bottom` | Assigned to the DOM element representing the bottom part of the lasso mask, when the lasso is inverted mode.                                                                                                        |
| `vjs-lasso-mask-left`   | Assigned to the DOM element representing the left part of the lasso mask, when the lasso is inverted mode.                                                                                                          |
| `vjs-lasso-mask-right`  | Assigned to the DOM element representing the right part of the lasso mask, when the lasso is inverted mode.                                                                                                         |
| `vjs-lasso-mask-top`    | Assigned to the DOM element representing the top part of the lasso mask, when the lasso is inverted mode.                                                                                                           |

## Options[​](#options "Direct link to Options")

LassoPluginOptions

| Name                  | Type                                                     | Description                                                                                                                                                                                                                                                                                                             |
| --------------------- | -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| armTimeout?           | number                                                   | Timeout in ms for autoArm long press. Defaults to 500ms.                                                                                                                                                                                                                                                                |
| autoArm?              | boolean                                                  | Defaults to false. If true, the lasso will arm itself after a long press.                                                                                                                                                                                                                                               |
| autoExit?             | boolean                                                  | When true (which is the default) the lasso exits after a selection has been made.                                                                                                                                                                                                                                       |
| cssClass?             | string                                                   | Extra class(es) to add to the lasso's DOM element                                                                                                                                                                                                                                                                       |
| enableInGroups?       | boolean \| "metaKey"                                     | Optional setting for whether lasso inside groups is enabled - it is by default. Setting this to `false` will mean that the user cannot lasso items inside a group. Setting to `"metaKey"` will mean that lasso is supported inside groups if the user is holding the meta key down (ie the Window key, or Cmd on macs). |
| filter?               | string \| (e:MouseEvent) => boolean                      | Optional CSS3 filter identifying elements you do not want to lasso                                                                                                                                                                                                                                                      |
| generateLassoContent? | (origin:[PointXY](), e:MouseEvent) => [BrowserElement]() | Optional function that generates the DOM element for the lasso to use. This is<br />for advanced usage scenarios and most users will not need to supply this.                                                                                                                                                           |
| includeEdges?         | boolean                                                  | Defaults to false. If true, edges are included in the lasso selection.                                                                                                                                                                                                                                                  |
| invert?               | boolean                                                  | Defaults to false, meaning the lasso is drawn as a rectangle. If true, the lasso is drawn as a set of masks,<br />with the lasso area drawn as a "hole" in the masks.                                                                                                                                                   |
| onEnd?                | Function                                                 | Optional function to call when lasso selection ends.                                                                                                                                                                                                                                                                    |
| onSelect?             | (vertices:Array<[Vertex]()>) => any                      | Optional function to call when one or more objects has been selected by the lasso.                                                                                                                                                                                                                                      |
| onStart?              | Function                                                 | Optional function to call when lasso selection starts.                                                                                                                                                                                                                                                                  |
| selectionFilter?      | (o:[Edge]() \| [Vertex]()) => boolean                    | Optional filter that is passed every vertex/edge that the lasso would ordinarily select, and if this function returns false<br />then the vertex/edge is not added to the selection                                                                                                                                     |
