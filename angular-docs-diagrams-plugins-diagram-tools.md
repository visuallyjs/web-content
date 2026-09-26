# Diagram tools

Provides a set of tools for working with shapes in a Diagram - resizing, rotating, cloning, deleting, and creating links.

**********

The plugin automatically attaches tools to any shape that is added to VisuallyJs's current selection, and removes the tools when the shape is removed from the selection.

## Setup[​](#setup "Direct link to Setup")

This plugin is installed on an editable Diagram by default, and configured indirectly via various diagram options.

By default, these tools are enabled:

* [**Resize**](#resizing) Places a handle at each corner of a shape, with which the user can alter the shape's size
* [**Rotate**](#rotation) Places a rotate handle above the shape, which the user can drag to rotate the shape.
* [**Clone**](#cloning-a-shape) Places a clone button at the top right corner, which a user can click on to create a clone of the shape
* [**Link**](#linking) Places a link handle at the bottom right, from which a user can drag a link to another shape

The default settings for the diagram tools plugin attach a handle at each corner that your users can drag to resize, but you can also instruct the plugin to allow users to resize by [dragging an element's borders](#resize-by-border)

## Resizing[​](#resizing "Direct link to Resizing")

The default resize mechanism is to place handles at each corner and halfway along each edge on a vertex's perimeter:

**********

### Handle shape[​](#handle-shape "Direct link to Handle shape")

By default, the plugin will use circular handles. You can change this to use rectangular handles by setting `handleShape:"rectangle"` in the cell options:

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  cells: {
    resize: {
      handleShape: "rectangle"
    }
  }
}
}

```

**********

<br />

### Handle size[​](#handle-size "Direct link to Handle size")

The default handle size is 10 pixels. You can change this to use rectangular handles by setting `handleSize`:

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  cells: {
    resize: {
      handleShape: "rectangle",
      handleSize: 20
    }
  }
}
}

```

**********

<br />

## Resize by border[​](#resize-by-border "Direct link to Resize by border")

Instead of attaching a handle at each corner to enable resize, you can setup the diagram tools to allow resize by dragging the borders of the element:

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  cells: {
    resize: {
      method: "borders"
    }
  }
}
}

```

**********

#### Border visibility[​](#border-visibility "Direct link to Border visibility")

By default, the borders for resizing will be visible to the user. You can set `bordersVisible:false` to hide the borders - the user will still see the cursor change when hovering over a border, but the border itself will not be shown:

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  cells: {
    resize: {
      method: "borders",
      bordersVisible: false
    }
  }
}
}

```

**********

## Rotation[​](#rotation "Direct link to Rotation")

By default, the rotation tool is enabled.

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {}
}

```

**********

### Disabling rotation[​](#disabling-rotation "Direct link to Disabling rotation")

You can switch off the rotate tool by setting `rotatable:false` in the `cells` diagram option:

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  cells: {
    rotatable: false
  }
}
}

```

**********

### Rotation stops[​](#rotation-stops "Direct link to Rotation stops")

The default behaviour is to support rotation to any angle, but you can specify the number of rotation stops VisuallyJs should use:

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  cells: {
    rotationStops: 12
  }
}
}

```

**********

## Grids[​](#grids "Direct link to Grids")

When the associated diagram has a grid, this plugin will constrain node/group resizing so that the dimensions of the vertex are a multiple of the grid in each axis.

**********

### Ignoring the grid[​](#ignoring-the-grid "Direct link to Ignoring the grid")

Constraining resize to the grid is controlled by the `ignoreGrid` option, which is set to false by default. You can change that:

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  cells: {
    resize: {
      ignoreGrid: true
    }
  }
}
}

```

**********

## Constraining resize axes[​](#constraining-resize-axes "Direct link to Constraining resize axes")

By default, the diagram tools plugin will allow users to resize an element's width and height. This behaviour can be changed, by setting `resizeX` or `resizeY` to "false" in the plugin options.

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular";
import {Component} from "@angular/core";

@Component({
    template:`<div style="width:100%;height:500px">
<vjs-diagram [data]="data" [options]="options"/>
</div>`
export class MyComponent {
    data = ...
    
    options = {
  cells: {
    resizeX: false
  }
}
}

```

The above configuration would result in a setup where your users can only resize the height of elements:

**********

## Excluding elements[​](#excluding-elements "Direct link to Excluding elements")

You can exclude specific elements from being resizable by writing a `data-vjs-resizable` attribute on them:

```html
<div data-vjs-resizable="false">{{name}}</div>

```

## Custom payloads[​](#custom-payloads "Direct link to Custom payloads")

You can provide a `payloadGenerator` to the diagram tools which will be invoked before the diagram tools commits a change to a model object. This method allows you to customize the changes that will be made to the model object (or it can be used as a hook to make other changes in your model of course):

```typescript
payloadGenerator?:(v:Node, p:ObjectData) => ObjectData

```

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { ResizingToolsPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
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
};
}

```

In this example the model object's data will be updated with the `someDynamicValue` we calculated.

caution

A payload generator function cannot override the value of any attributes the diagram tools needs to set, ie. the position or size of the object. the diagram tools will merge its attributes on top of any you return from a payload generator.

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
