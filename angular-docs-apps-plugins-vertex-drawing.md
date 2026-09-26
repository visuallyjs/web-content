# Vertex drawing

This plugin provides a means for users to draw new nodes and groups onto the canvas, or into existing groups. When drawing a group users can snag existing vertices on the canvas for inclusion in the new group.

## Instantiation[​](#instantiation "Direct link to Instantiation")

### Manual mode[​](#manual-mode "Direct link to Manual mode")

To use this plugin "manually" (discussed [below](#manual-usage)), you declare it in the `plugins` section of the render options for some Surface:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { VertexDrawingPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  useModelForSizes: true,
  plugins: [
    VertexDrawingPlugin.type
  ]
};
}

```

Note the `useModelForSizes:true` declaration: this is recommended, if you intend to let your users drag new vertices via a lasso. There is also a mode in which your users can click on the canvas to add new vertices, and in that mode you may not need to use the model for sizes. This is [discussed below](#clicking-to-add-vertices)

### Integrated with ShapePalette[​](#integrated-with-shapepalette "Direct link to Integrated with ShapePalette")

To use this plugin with a `ShapePalette`, you need to instruct the palette to run in "tap" mode:

```typescript

import { SURFACE_MODE_TAP } from "@visuallyjs/browser-ui"

@Component({
  selector:"app-component",
  template:`<div>
        <vjs-surface [viewOptions]="viewOptions"/>
        <vjs-shape-palette [dataGenerator]="dataGenerator" [mode]="SURFACE_MODE_TAP"/>
</div>`
</div>
})

export class AppComponent {

    viewOptions = {... }
    
    dataGenerator(el:Element) {
        return {
            ...
        }
    }    
}


```

With this setup, the `ShapeLibraryPalette` will register a suitable configured instance of the vertex drawing plugin on the surface. It also handles setting the surface into `vertexDrawing` mode in order to activate the plugin at the appropriate time.

For a full discussion of dragging/drawing new SVG shapes, please see [this page](/angular/docs/apps/nodes-and-groups/shape-libraries)

***

## Manual usage[​](#manual-usage "Direct link to Manual usage")

With the declaration shown above you get a default setup of the plugin, which will draw groups, of type `default`. In order to switch on the plugin, you have to set the appropriate mode in the surface:

```javascript
import { SURFACE_MODE_VERTEX_DRAWING  } from "@visuallyjs/browser-ui"

mySurface.setMode(SURFACE_MODE_VERTEX_DRAWING)

```

In this first example we've declared a vertex drawing plugin and then made the call shown above to activate the plugin. Try clicking and dragging on the canvas below - the plugin will add new groups. You can also draw groups inside other groups.

**********

We setup the surface using the code snippet shown above - with the default options on the vertex drawing plugin, but also with `useModelForSizes` switched on:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { VertexDrawingPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  useModelForSizes: true,
  plugins: [
    VertexDrawingPlugin.type
  ]
};
}

```

note

For comparison, here's the same setup but without `useModelForSizes:true`. Notice how the groups you add always end up the same size, regardless of the size you draw them:

**********

### Specifying vertex details[​](#specifying-vertex-details "Direct link to Specifying vertex details")

The default setup of this plugin will always create new groups, and those groups will have `type` of `default`. For a more fine-grained control of the plugin, you have a few options.

### Specifying group type[​](#specifying-group-type "Direct link to Specifying group type")

You can instruct the plugin to use a specific group type via the `groupType` parameter:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { VertexDrawingPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  useModelForSizes: true,
  plugins: [
    {
      type: VertexDrawingPlugin.type,
      options: {
        groupType: "userDrawn"
      }
    }
  ]
};
}

```

In this example we've added a couple of groups manually, whose type is "default", and so, per the view above, they are drawn with an orange-red box. But if you drag new groups in this canvas, their type will be `userDrawn`, resulting in a `cadetblue` box (one of my favourite default HTML colors).

**********

### Drawing nodes[​](#drawing-nodes "Direct link to Drawing nodes")

To draw nodes instead of groups, supply a `nodeType` parameter to the plugin:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { VertexDrawingPlugin } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  useModelForSizes: true,
  plugins: [
    {
      type: VertexDrawingPlugin.type,
      options: {
        nodeType: "userDrawn"
      }
    }
  ]
};
}

```

For the sake of clarity here we've declared a `default` and also a `userDrawn` type for groups and for nodes. On the canvas we've added a group and a node, both of type `default`. But if you now draw a new vertex on here, the `nodeType` parameter set on the plugin will instruct the plugin to draw nodes, of type `userDrawn`, in this case. So you'll see a box that is coloured `darkmagenta` when you draw:

**********

### Choosing type at runtime[​](#choosing-type-at-runtime "Direct link to Choosing type at runtime")

A common use case for this plugin is to draw vertices of some type that a user has selected in the UI (that's the case for the `ShapePalette`, for instance, which is discussed below). To support this, instead of supply a hard-coded `groupType` or `nodeType`, you can supply a `typeGenerator`, which allows you to not only choose the type of vertex to create, it allows you to choose between a node or a group, and also to provide an initial payload. The signature for the `typeGenerator` function is:

```javascript
export type VertexDrawingPluginTypeGenerator = (origin:PointXY, e:MouseEvent) => {objectType:typeof Node.objectType | typeof Group.objectType, type:string, data?:ObjectData}

```

So it is given the `origin` of the event (in canvas coordinates) and the originating mouse event, and is expected to return an object of this type:

```javascript
{
    type:string,
    objectType:"Group"|"Node",
    data?:ObjectData
}

```

Here we have the same example as just above, but in this case we've added radio button to allow you to specify what type of object to draw. Remember, groups are `cadetblue` and nodes are `darkmagenta`.

Our plugin spec looks like this:

```javascript
plugins:[
    {
        type:tk.VertexDrawingPlugin.type,
        options:{
            typeGenerator:(origin, evt) => {
              return {
                  objectType:document.querySelector("[type='radio']:checked").value,
                  type:"userDrawn"
              }
          }
        }
    }
]

```

...we return the value of the currently checked radio button. How you go about determining this value will depend on your app. Notice also that here we've hard-coded the `type`, but that is also, of course, something you can derive dynamically.

**********

\[ ]Group\[x]Node

### Clicking to add vertices[​](#clicking-to-add-vertices "Direct link to Clicking to add vertices")

All of the preceding examples have been focused on the user dragging an area on the screen to draw new vertices, but it is also possible to allow "click to add":

```javascript
plugins:[
    {
        type:tk.VertexDrawingPlugin.type,
        options:{
            typeGenerator:(origin, evt) => {
              return {
                  objectType:document.querySelector("[type='radio']:checked").value,
                  type:"userDrawn"
              },
              allowClickToAdd:true
          }
        }
    }
]

```

**********

\[ ]Group\[x]Node

When you have this enabled, the plugin will use a default size for nodes of 80 pixels width and height, and for groups of 250 pixels width and height. You can set those values:

```javascript
plugins:[
    {
        type:tk.VertexDrawingPlugin.type,
        options:{
            typeGenerator:(origin, evt) => {
              return {
                  objectType:document.querySelector("[type='radio']:checked").value,
                  type:"userDrawn",
                  defaultNodeSize:{width:100, height:80},
                  defaultGroupSize:{width:500, height:350}
              },
              allowClickToAdd:true
          }
        }
    }
]

```

## Advanced usage[​](#advanced-usage "Direct link to Advanced usage")

### Providing a vertex preview element[​](#providing-a-vertex-preview-element "Direct link to Providing a vertex preview element")

By default, the vertex drawing plugin uses a `[lasso](plugins-overview#lasso)` to draw an area on the canvas that the new vertex will occupy. You can, though, provide a function that will generate an element at the start of a drag to be drawn as a child of the lasso:

```javascript
vertexPreviewGenerator?:(p:PointXY, e:MouseEvent) => BrowserElement

```

**********

This is the code for the example above:

```javascript
plugins:[
    {
        type:tk.VertexDrawingPlugin.type,
        options:{
            vertexPreviewGenerator:(p, e) => {

                const div = document.createElement("div")
                div.style.position="absolute"
                div.style.width="100%"
                div.style.height="100%"
                div.style.display="flex"
                div.style.alignItems="center"

                const d = document.createElement("marquee")
                d.style.width="100%"
                d.setAttribute("scrollamount", 15)
                d.innerHTML = "I am drawing a new element"
                div.appendChild(d)

                return div
            }
        }
    }
]

```

It's almost certain if you use this functionality you'll do something more sensible with it. The `ShapeLibraryPalette`, for example, draws the current selected shape into an element and returns that.

### Updating the preview element[​](#updating-the-preview-element "Direct link to Updating the preview element")

Depending on what the HTML for your preview element looks like, you may need to update it as the user drags. In our example above we did not; we used some HTML elements and had CSS take care of the positioning for us. But in some cases - particularly if working with SVG - you might want to update the element. For that you can provide a `vertexPreviewUpdater`:

```javascript
vertexPreviewUpdater?:(p:PointXY, size:Size, el:BrowserElement) => any

```

Try dragging a new group here:

**********

For this we provided a `vertexPreviewGenerator` and also a `vertexPreviewUpdater`:

```javascript
plugins:[
    {
        type:VertexDrawingPlugin.type,
        options:{
            vertexPreviewGenerator:(p, e) => {

                const svg = document.createElementNS("http://www.w3.org/2000/svg", "svg")
                const rect = document.createElementNS("http://www.w3.org/2000/svg", "rect")
                rect.setAttribute("fill", "#567567")
                rect.setAttribute("x", "0")
                rect.setAttribute("y", "0")
                rect.setAttribute("width", "50%")
                rect.setAttribute("height", "50%")
                svg.appendChild(rect)

                const rect2 = document.createElementNS("http://www.w3.org/2000/svg", "rect")
                rect2.setAttribute("fill", "#984267")
                rect2.setAttribute("x", "50%")
                rect2.setAttribute("y", "50%")
                rect2.setAttribute("width", "50%")
                rect2.setAttribute("height", "50%")
                svg.appendChild(rect2)

                return svg
            },
            vertexPreviewUpdater:(p, size, el) => {
                el.setAttribute("width", size.width)
                el.setAttribute("height", size.height)
            }
        }
    }
]

```

The preview element is an SVG element, and the updater sets its width and height. It could probably be argued, in fact, that this case could also have been handled via CSS, but there are internal use cases in VisuallyJs that cannot, and so there may well be use cases in your app that cannot either.

***

### Usage with ShapePalette[​](#usage-with-shapepalette "Direct link to Usage with ShapePalette")

The `ShapePalette` can integrate with a vertex drawing plugin. The way to switch this on is to set the `mode` flag on the palette to `SURFACE_MODE_TAP` (or "tap", if you just want to use a string):

```javascript

import { SURFACE_MODE_TAP, ShapeLibraryPalette, ShapeLibraryImpl } from "@visuallyjs/browser-ui"

const shapeLibrary = new ShapeLibraryImpl(...)

new ShapePalette({
    container:document.querySelector(".node-palette"),
    surface,
    mode:SURFACE_MODE_TAP,
    shapeLibrary,
    dataGenerator:(el) => {
        return {
            name:el.getAttribute("data-type"),
            details:""
        }
    }
})

```

The palette will now create a vertex drawing plugin and attach it to the surface. The palette takes advantage of several of the capabilities discussed above:

* A `typeGenerator` is provided to the plugin which returns the `objectType` and `type` of the currently selected item in the palette. Additionally, any `dataGenerator` set on the palette will be invoked and used to prepare an initial dataset for a new vertex.
* A `vertexPreviewGenerator` is provided, which draws a copy of the currently selected element (which is SVG).
* A `vertexPreviewUpdater` function is provided, which redraws the SVG according to the new dimensions.

Try clicking an element in the palette here and dragging new nodes on the canvas:

**********

***

### Grids[​](#grids "Direct link to Grids")

When the associated surface has a grid, this plugin will constrain node/group sizes so that the dimensions of new vertices are a multiple of the grid in each axis.

***

### CSS[​](#css "Direct link to CSS")

ClassTable id="vertexDrawing"/>

***

### Options[​](#options "Direct link to Options")

VertexDrawingPluginOptions

Options for the vertex drawing plugin

| Name                    | Type                                                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowClickToAdd?        | boolean                                                      | Defaults to false. When true, users can click on the canvas to "draw" a new element, and the plugin will use a default size for the element. When this flag is set, drag to add is still also enabled.                                                                                                                                                                                                                          |
| autoExit?               | boolean                                                      | When true (which is the default) the lasso exits after a group has been drawn                                                                                                                                                                                                                                                                                                                                                   |
| clickToAddOnly?         | boolean                                                      | Defaults to false. When true, the plugin only supports click to add new vertices, not drag. This flag is forced to true if the associated UI does not have `useModelForSizes` set, since there is no point in allowing a user to drag a vertex to some size if its not going to be honoured. When you set this flag and associated UI does have `useModelForSizes` set, the plugin will use default sizes for new nodes/groups. |
| defaultGroupSize?       | [Size]()                                                     | Optional default size for groups, used when `allowClickToAdd` is set to true. Defaults to width and height of 250 pixels.                                                                                                                                                                                                                                                                                                       |
| defaultNodeSize?        | [Size]()                                                     | Optional default size for nodes, used when `allowClickToAdd` is set to true. Defaults to width and height of 80 pixels.                                                                                                                                                                                                                                                                                                         |
| groupType?              | string                                                       | The type identifier for new groups. If you have also provided a typeGenerator this will be ignored. If you have not provided a typeGenerator but you have provided a nodeType, this will be ignored.                                                                                                                                                                                                                            |
| invert?                 | boolean                                                      | Defaults to false, meaning the lasso is drawn as a rectangle. If true, the lasso is drawn as a set of masks, with the lasso area drawn as a "hole" in the masks.                                                                                                                                                                                                                                                                |
| lassoClass?             | string                                                       | Optional extra class(es) to set on the lasso used for drawing.                                                                                                                                                                                                                                                                                                                                                                  |
| minSize?                | [Size]()                                                     | The minimum size for vertices. If your user draws a vertex smaller than this it will be discarded. Defaults to a width/height of 50 pixels.                                                                                                                                                                                                                                                                                     |
| nodeType?               | string                                                       | The type identifier for new nodes. If you have also provided a typeGenerator this will be ignored.                                                                                                                                                                                                                                                                                                                              |
| onVertexAdded?          | (v:[Vertex]()) => any                                        | Callback to invoke when a vertex has been added                                                                                                                                                                                                                                                                                                                                                                                 |
| typeGenerator?          | [VertexDrawingPluginTypeGenerator]()                         | Optional function that will be invoked when a new drag commences, and which is responsible for returning the type of object to add (Node or Group), as well as that object's own type, and, optionally, an initial payload for the new object.                                                                                                                                                                                  |
| vertexPreviewGenerator? | (p:[PointXY](), e:MouseEvent) => [BrowserElement]()          | A function that will be invoked at the start of a drawing operation, and can return an element to draw into the lasso. This is an optional function; if you don't provide it VisuallyJs will draw a basic SVG rectangle to indicate the drawing area.                                                                                                                                                                           |
| vertexPreviewUpdater?   | (p:[PointXY](), size:[Size](), el:[BrowserElement]()) => any | A function that is invoked during mouse drag, to be used in conjunction with `vertexPreviewGenerator`. This function gives you a hook to use to make any changes to your preview element, should you need to. This is optional.                                                                                                                                                                                                 |
