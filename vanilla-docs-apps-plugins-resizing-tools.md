# Resizing tools

Provides the tools to assist in resizing nodes/groups.

**********

The plugin automatically attaches resizing tools to any vertex that is added to VisuallyJs's current selection, and removes the resizing tools when the vertex is removed from the selection. This behaviour can be changed by setting `onDemand:true` in the plugin options.

The default settings for the resizing tools plugin attach a handle at each corner, and at the midpoint of each edge, that your users can drag to resize, but you can also instruct the plugin to allow users to resize by [dragging an element's borders](#resizing-by-border)

## Setup[​](#setup "Direct link to Setup")

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    ResizingToolsPlugin.type
  ]
})

```

We show the plugin here without any constructor options as it "just works" for the most part, but there are a few configurable options.

In the canvas above we've selected one of the vertices after loading the dataset. You can click on other vertices to select them.

## Resizing by handle[​](#resizing-by-handle "Direct link to Resizing by handle")

### Handle Shape[​](#handle-shape "Direct link to Handle Shape")

By default, the plugin will use circular handles. You can change this to use rectangular handles by setting `handleShape:"rectangle"` in the plugin options:

```javascript
import { newInstance,  } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        handleShape: "rectangle"
      }
    }
  ]
})

```

**********

<br />

#### Handle size[​](#handle-size "Direct link to Handle size")

You can also change the size of the handles by setting `handleSize`:

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        handleShape: "rectangle",
        handleSize: 20
      }
    }
  ]
})

```

**********

## Resizing by border[​](#resizing-by-border "Direct link to Resizing by border")

Instead of attaching a handle at each corner to enable resize, you can setup the resizing tools to allow resize by dragging the borders of the element:

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        resizeMethod: "borders"
      }
    }
  ]
})

```

**********

#### Border visibility[​](#border-visibility "Direct link to Border visibility")

By default, the borders for resizing will be visible to the user. You can set `bordersVisible:false` to hide the borders - the user will still see the cursor change when hovering over a border, but the border itself will not be shown:

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        resizeMethod: "borders",
        bordersVisible: false
      }
    }
  ]
})

```

**********

## Rotation[​](#rotation "Direct link to Rotation")

You can allow your users to rotate objects by setting `rotatable:true` on the plugin options:

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        rotatable: true
      }
    }
  ]
})

```

**********

### Per-vertex disable[​](#per-vertex-disable "Direct link to Per-vertex disable")

If you have the rotation tool enabled but you wish to switch it off for some specific vertex, you can do so by setting a `data-vjs-rotatable` attribute on the vertex element:

```html
<div data-vjs-rotatable="false">
    <h2>My non-rotatable vertex</h2>
</div>

```

In this example, every node except node 2 is rotatable - but node 2 has `data-vjs-rotatable:false` set:

**********

### Rotation stops[​](#rotation-stops "Direct link to Rotation stops")

The default behaviour is to support rotation to any angle, but you can specify the number of rotation stops VisuallyJs should use:

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        rotatable: true,
        rotationStops: 12
      }
    }
  ]
})

```

**********

## Grids[​](#grids "Direct link to Grids")

When the associated surface has a grid, this plugin will constrain node/group resizing so that the dimensions of the vertex are a multiple of the grid in each axis.

**********

This is controlled by the `ignoreGrid` option, which is set to false by default. You can change that:

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        ignoreGrid: true
      }
    }
  ]
})

```

**********

## Constraining size[​](#constraining-size "Direct link to Constraining size")

There are 3 options you can use to constrain the size when resizing elements:

* **minimumWidth** The minimum width the user can drag any element to
* **minimumHeight** The minimum height the user can drag any element to
* **constrainGroups** When true, the minimum size for groups when resizing will be calculated as the bounds of their child elements.

note

The resizing tools plugin will not resize collapsed groups.

## Attaching tools on demand[​](#attaching-tools-on-demand "Direct link to Attaching tools on demand")

By default the resizing tools will attach themselves to any element that is in VisuallyJs's current selection, but you can switch to "on demand" mode like this:

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        onDemand: true
      }
    }
  ]
})

```

## Constraining resize axes[​](#constraining-resize-axes "Direct link to Constraining resize axes")

By default, the resizing tools plugin will allow users to resize an element's width and height. This behaviour can be changed, in one of two ways:

* By setting the attribute `data-vjs-y-resize` or `data-vjs-x-resize` to "false" on some node/group template:

```html
<div data-vjs-x-resize="false">...</div>

```

* By setting `resizeX` or `resizeY` to "false" in the plugin options.

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        resizeX: false
      }
    }
  ]
})

```

The above configuration would result in a setup where your users can only resize the height of elements:

**********

## Excluding elements[​](#excluding-elements "Direct link to Excluding elements")

You can exclude specific elements from being resizable by writing a `data-vjs-resizable` attribute on them:

```html
<div data-vjs-resizable="false">{{name}}</div>

```

## Custom payloads[​](#custom-payloads "Direct link to Custom payloads")

You can provide a `payloadGenerator` to the resizing tools which will be invoked before the resizing tools commits a change to a model object. This method allows you to customize the changes that will be made to the model object (or it can be used as a hook to make other changes in your model of course):

```text
payloadGenerator?:(v:any, p:any) => any

```

```javascript
import { newInstance, ResizingToolsPlugin } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  plugins: [
    {
      type: ResizingToolsPlugin.type,
      options: {
        payloadGenerator: (vertex, data) => {
                 return {
                     someDynamicValue:data.w * something etc
                 } 
             }
      }
    }
  ]
})

```

In this example the model object's data will be updated with the `someDynamicValue` we calculated.

caution

A payload generator function cannot override the value of any attributes the resizing tools needs to set, ie. the position or size of the object. The resizing tools will merge its attributes on top of any you return from a payload generator.

## Updating the model on resize[​](#updating-the-model-on-resize "Direct link to Updating the model on resize")

In some applications you may wish to respond to a vertex resize by making additional changes to the model. An example of this is in our <!-- -->[BPMN](/demonstrations/bpmn.md) starter app - when you resize a `pool` you also want to resize the pool's `lanes`.

To support this, the resizing tools allow you to provide a `handlerFactory`. This is a function that is invoked when a resize starts, and it returns a function that will be called for each mouse move during the resize. The type definition of `ResizingToolsHandlerFactory` is:

`(ui:Surface, vertex:Node | Group, resizeDirection:ResizeDirection, defaultHandler:ResizeFunction) => ResizeFunction`

* `ui` is the surface on which the vertex is displayed
* `vertex` is the vertex being resized
* `resizeDirection` is the [ResizeDirection]().
* `defaultHandler` is the function that the resizing tools would normally use to resize the element. Your custom handler can call this default handler and then modify the result, or it can return an entirely custom set of changes.

### Example: BPMN Lanes and Pools[​](#example-bpmn-lanes-and-pools "Direct link to Example: BPMN Lanes and Pools")

In the BPMN starter app, we use a `handlerFactory` to ensure that when a pool is resized, its lanes are also resized to match, and vice versa.

```typescript
import { Surface, Node, Group, ResizeFunction } from "@visuallyjs/core"

export const resizeFactory: ResizingToolsHandlerFactory = (
    ui: Surface, 
    vertex: Node | Group, 
    direction: string, 
    defaultHandler: ResizeFunction
) => {
     if (vertex.type === 'POOL') {
         const lanes = vertex.getMembers().filter(m => m.type === 'LANE')
         
        return (dx: number, dy: number) => {
             // Get the default resize changes
             const def = defaultHandler(dx, dy)
             def.updates = {}

            if (lanes.length > 0) {
                // ... calculate new sizes for lanes ...
                lanes.forEach((lane, i) => {
                    def.updates[lane.id] = {
                        width: def.width - 20,
                        height: newHeight,
                        y: currentY
                    }
                    currentY += newHeight
                })
                // Adjust pool height to match sum of lanes
                def.height = currentY
            }
            return def
        }
    }
    // ... handle other types or return default ...
}

```

By returning a `updates` object in the result of your handler, you can specify additional changes to be made to other elements in the model.

## Handle offset[​](#handle-offset "Direct link to Handle offset")

## CSS[​](#css "Direct link to CSS")

| Class                                 | Description                                                                                                                                                      |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-resize-border`                   | Set on the border handles                                                                                                                                        |
| `vjs-resize-border-b`                 | Set on the bottom border handle                                                                                                                                  |
| `vjs-resize-border-l`                 | Set on the left border handle                                                                                                                                    |
| `vjs-resize-border-r`                 | Set on the right border handle                                                                                                                                   |
| `vjs-resize-border-t`                 | Set on the top border handle                                                                                                                                     |
| `vjs-resize-frame`                    | Set on the frame the resize tool draws around an object it is currently editing.                                                                                 |
| `vjs-resize-handle`                   | Set on the resize handles by the resizing/diagram tools                                                                                                          |
| `vjs-resize-handle-active`            | Set on a resize handle when it is being actively used                                                                                                            |
| `vjs-resize-handle-b`                 | Set on the bottom center resize handle                                                                                                                           |
| `vjs-resize-handle-bl`                | Set on the bottom left corner resize handle                                                                                                                      |
| `vjs-resize-handle-br`                | Set on the bottom right corner resize handle                                                                                                                     |
| `vjs-resize-handle-l`                 | Set on the left center resize handle                                                                                                                             |
| `vjs-resize-handle-r`                 | Set on the right center resize handle                                                                                                                            |
| `vjs-resize-handle-t`                 | Set on the top center resize handle                                                                                                                              |
| `vjs-resize-handle-tl`                | Set on the top left corner resize handle                                                                                                                         |
| `vjs-resize-handle-tr`                | Set on the top right corner resize handle                                                                                                                        |
| `vjs-resize-skeleton`                 | Set on the element that is the parent of drag handles when in `handles` resize mode.                                                                             |
| `vjs-resize-skeleton-borders`         | Set on the element that is the parent of drag borders when in `borders` resize mode.                                                                             |
| `vjs-resize-skeleton-borders-visible` | Set on the resize tool's main group element for some vertex when `bordersVisible` is set to true and the resize mode is RESIZING\_TOOLS\_RESIZE\_METHOD\_BORDERS |
| `vjs-rotate-handle`                   | Set on the rotation handle                                                                                                                                       |
| `vjs-rotate-leader`                   | Set on the leader to the rotation handle.                                                                                                                        |

## Options[​](#options "Direct link to Options")

ResizingToolsPluginOptions

Options for the resizing tool plugin.

| Name                | Type                                                                               | Description                                                                                                                                                                                                                                                                                                                                                        |
| ------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| borderHandleSize?   | number                                                                             | Size of handles when using "border" resize. Defaults to 6 pixels.                                                                                                                                                                                                                                                                                                  |
| bordersVisible?     | boolean                                                                            | When resizeMethod is "borders", set this to make the borders visible. Internally this just sets a CSS class on the draw skeleton's parent DOM element, and the appearance of the borders is then controlled via CSS.                                                                                                                                               |
| canResizeFilter?    | (v:[Vertex](), el:[BrowserElement]()) => boolean                                   | Optional function that can decide on whether or not the given vertex should be resizable                                                                                                                                                                                                                                                                           |
| canRotateFilter?    | (v:[Vertex](), el:[BrowserElement]()) => boolean                                   | Optional function that can decide on whether or not the given vertex should be rotatable                                                                                                                                                                                                                                                                           |
| constrainGroups?    | boolean                                                                            | Defaults to true, meaning groups will not be shrunk to the point that one or more of their child vertices is no longer visible.                                                                                                                                                                                                                                    |
| handleOffset?       | number                                                                             | How much to offset the resize frame and handles from the bounds of the shape. Defaults to 5 pixels.                                                                                                                                                                                                                                                                |
| handlerFactory?     | [ResizingToolsHandlerFactory]()                                                    | Optional factory that can return a resize handler for some given vertex. You can use this to override the default behaviour for any vertex you choose                                                                                                                                                                                                              |
| handleShape?        | "circle" \| "rectangle"                                                            | Shape of resize handles. Defaults to circle.                                                                                                                                                                                                                                                                                                                       |
| handleSize?         | number                                                                             | Width/height to use for handles. Defaults to 20 pixels.                                                                                                                                                                                                                                                                                                            |
| heightAttribute?    | string                                                                             | Attribute to use for vertex height - defaults to 'height'                                                                                                                                                                                                                                                                                                          |
| ignoreGrid?         | boolean                                                                            | Defaults to false, meaning size changes conform to an underlying grid, if present                                                                                                                                                                                                                                                                                  |
| leftAttribute?      | string                                                                             | Attribute to use for vertex left position - defaults to 'left'                                                                                                                                                                                                                                                                                                     |
| minimumHeight?      | number                                                                             | Minimum height the user can shrink a vertex to. Defaults to 30.                                                                                                                                                                                                                                                                                                    |
| minimumWidth?       | number                                                                             | Minimum width the user can shrink a vertex to. Defaults to 30.                                                                                                                                                                                                                                                                                                     |
| modelUpdater?       | [ResizingToolsModelUpdater]()                                                      | Optional function that can inject extra model updates each time a vertex is resized.                                                                                                                                                                                                                                                                               |
| onDemand?           | boolean                                                                            | Defaults to false, meaning the resizing tool plugin switches on whenever a new vertex is selected.                                                                                                                                                                                                                                                                 |
| onEdit?             | (o:[Node]() \| [Group](), surface:[Surface](), toolkit:[VisuallyJsModel]()) => any | Optional callback invoked after an edit has occurred                                                                                                                                                                                                                                                                                                               |
| payloadGenerator?   | (v:[Node](), p:[ObjectData]()) => [ObjectData]()                                   | Optional function to invoke when a resize has occurred. The values the resizing plugin wants to write for the vertex are merged on top of the value returned from this function, and the combined payload is written as an update to the vertex in the data model. This exists for internal use mostly but there's no harm in it being exposed for your enjoyment. |
| resizeMethod?       | [ResizingToolsResizeMethod]()                                                      | Method to use for resize - handles on the corners, or borders. Defaults to handles.                                                                                                                                                                                                                                                                                |
| resizeX?            | boolean                                                                            | Whether or not to support resize in the X axis. Defaults to true.                                                                                                                                                                                                                                                                                                  |
| resizeY?            | boolean                                                                            | Whether or not to support resize in the Y axis. Defaults to true.                                                                                                                                                                                                                                                                                                  |
| rotatable?          | boolean                                                                            | Whether or not to support rotation on all elements.. Defaults to false.                                                                                                                                                                                                                                                                                            |
| rotateHandleSize?   | number                                                                             | Size of the rotate handle. Defaults to 16 pixels.                                                                                                                                                                                                                                                                                                                  |
| rotateLeaderLength? | number                                                                             | Length of the leader line to the resize handle when using the resizing tools in an SVG container. Defaults to 30 pixels.                                                                                                                                                                                                                                           |
| rotationStops?      | number                                                                             | Optional number of stops to use when rotating. If not provided vertices can be rotated to any angle. If provided, the value is divided into 360 and the result is the angle between each stop. For example, a value of 12 means each stop is 30 degrees.                                                                                                           |
| topAttribute?       | string                                                                             | Attribute to use for vertex top position - defaults to 'top'                                                                                                                                                                                                                                                                                                       |
| widthAttribute?     | string                                                                             | Attribute to use for vertex width - defaults to 'width'                                                                                                                                                                                                                                                                                                            |
