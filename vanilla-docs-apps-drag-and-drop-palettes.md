# Palettes

A common use case in the sorts of applications for which VisuallyJs is useful is the requirement to be able to drag and drop new nodes/groups onto the workspace.

## Setup[​](#setup "Direct link to Setup")

The `Palette` provides a means for you to configure part of your UI as a palette from which users can drag new nodes/groups onto the canvas.

At the bare minimum, you need to provide these parameters when you create an instance of the `Palette`:

```javascript
import { Palette } from "@visuallyjs/browser-ui"

new Palette({
    source:someElement,
    selector:"[data-vjs-type]",
    ui:renderer
});

```

* **source** The element containing other elements that are draggable
* **selector** a CSS3 selector identifying elements within `source` that are draggable
* **ui** The Surface to attach to

`source`, as mentioned above, identifies the DOM element that contains the draggable elements, and `selector` identifies the elements within that element that are draggable. It is your responsibility to write out the HTML for `source`. For example, a simple setup could be:

```html
<div>
    <div data-vjs-type="process">Process element</div>
    <div data-vjs-type="question">Question element</div>
</div>

```

#### Enabling/disabling[​](#enablingdisabling "Direct link to Enabling/disabling")

Use the `setEnabled(enabled:boolean)` method on a Palette to enable/disable it.

In Vanilla VisuallyJs, the `Palette` component can automatically manage its own content by using a template and a data set. This is particularly useful when you want the palette to be data-driven rather than manually defining every DOM element in your HTML.

### `contentTemplate` and `data`[​](#contenttemplate-and-data "Direct link to contenttemplate-and-data")

These two options work together to allow the Palette to render its own items, rather than requiring you to have drawn the palette out in the HTML before initialising it.

* **`contentTemplate`**: A string representing the HTML template to use for each item in the palette. It can contain placeholders that correspond to keys in your data objects.
* **`data`**: An array of objects (or a single object) containing the information for each item you want the palette to display.

When these options are provided, the Palette uses an internal `PaletteContentGenerator` to process the template for each entry in the `data` array and inject the resulting elements into the palette's `source` container.

### Example Usage[​](#example-usage "Direct link to Example Usage")

```javascript
const palette = new Palette(ui, {
    source: document.getElementById("my-palette"),
    // Define a template with placeholders
    contentTemplate: `<div class="palette-item" data-vjs-type="{{type}}">
                        <span>{{label}}</span>
                      </div>`,
    // Provide the data to fill the template
    data: [
        { type: "task", label: "New Task" },
        { type: "decision", label: "Decision Point" },
        { type: "output", label: "Final Output" }
    ],
    // ... other options
});

```

### Dynamic Updates[​](#dynamic-updates "Direct link to Dynamic Updates")

If your palette needs to change after initialization, you can use the `setData` method to refresh the content:

```javascript
// Replace the existing data and re-render the palette items
palette.setData([
    { type: "new-type", label: "Updated Item" }
]);

// You can also optionally provide a new template during the update
palette.setData(newData, `<div class="new-style">{{label}}</div>`);

```

This approach simplifies palette management by keeping your UI structure defined in a template and your palette items managed as a collection of data objects.

## Providing data for a dragged element[​](#providing-data-for-a-dragged-element "Direct link to Providing data for a dragged element")

Internally, the palette uses a `dataGenerator` function to get a suitable piece of backing data for some element that is being dragged. You do not need to provide a `dataGenerator`: the default behaviour is to retrieve data values from `data-vjs-***` attributes on the element a user is dragging. For instance with this element:

```html
<div data-vjs-type="process" data-vjs-label="Process" data-vjs-width="120" data-vjs-height="80">Process</div>

```

VisuallyJs will prepare this payload for the object representing the drag:

```javascript
{
    "type":"process",
    "label":"Process",
    "width":"120",
    "height":"80"
}

```

tip

The default mechanism used by VisuallyJs for determining the type of some object is to test the `type` member. Providing `type` as we have here (via the `data-vjs-type` attribute) allows VisuallyJs to determine which template to use to render the node, how it will behave, etc.

You can provide a `dataGenerator` if you want more control over the dataset that is created:

```javascript
new Palette({
    source:someElement,
    ui:renderer,
    dataGenerator: (el) => {
        return {
            label:el.getAttribute("data-vjs-label"),
            type:el.getAttribute("data-vjs-type"),
            width:el.getAttribute("data-vjs-width"),
            height:el.getAttribute("data-vjs-height")
        };
    }
});

```

In this example, we provide a data object with `label`, `type`, `width` and `height` properties - it creates the same dataset as what you'd get from the default data generator. But you can return whatever you like.

## Distinguishing between a node and a group[​](#distinguishing-between-a-node-and-a-group "Direct link to Distinguishing between a node and a group")

By default, VisuallyJs will look for a `data-vjs-is-group` attribute on a dragged element. If the value of this attribute is `"true"`, VisuallyJs will assume the element represents a group. You can provide your own `groupIdentifier` if you wish.

## Specifying the size for a new element[​](#specifying-the-size-for-a-new-element "Direct link to Specifying the size for a new element")

By default, the Palette clones the DOM element on which the user started a drag and then sets the size of the element that is being dragged to match the bounding client rectangle of the element that was cloned.

In some situations, particularly when you have a grid in your surface, you may wish to mandate the size for any new elements that are being dragged on to the surface, which you can do by providing a `dragSize` object:

```javascript
const palette = new Palette({
    source:someElement,
    selector:"[data-vjs-type]",
    ui:renderer,
    dragSize:{ width:250, height: 100 }
})

```

## Filtering draggable elements[​](#filtering-draggable-elements "Direct link to Filtering draggable elements")

It is possible, when drag starts, to decide whether or not you want the dragged element to be droppable on the canvas:

```javascript
new Palette({    
    ui:SomeSurfaceWidget,
    source:someElement,
    selector:".draggable-child",
    canvasDropFilter:(data:ObjectData):boolean => {
        return data.type === "someDroppableOnCanvasType";    
    }  
})

```

## Rotating dragged elements[​](#rotating-dragged-elements "Direct link to Rotating dragged elements")

Since:

<!-- -->

1.2.5

You can rotate an element that you are dragging from the palette before dropping it, if you have the `ResizingToolsPlugin` installed on your canvas and you have *not* explicitly set `allowRotation:false` on the palette.

To configure the palette to allow rotation, set `rotatable` to be true in the `ResizingToolsPlugin` options:

```javascript
import { Palette } from "@visuallyjs/browser-ui"

const surface = null // your Surface instance

const renderOptions = {
    plugins:[
        {
            type:`%ResizingToolsPlugin.type`,
            options:{
                rotatable:true
            }
        }
    ]
}

new Palette({
    source:document.getElementById("my-palette"),
    selector:"[data-vjs-type]",
    ui:surface
});

```

Hold down the meta key (CMD on mac) to rotate an element as you are dragging it from the palette in this canvas:

FOO

BAR

### Rotation stops[​](#rotation-stops "Direct link to Rotation stops")

If you specify `rotationStops` in your resizing tools options, the palette will honour them:

```javascript
import { Palette } from "@visuallyjs/browser-ui"

const surface = null // your Surface instance

const renderOptions = {
    plugins:[
        {
            type:`%ResizingToolsPlugin.type`,
            options:{
                rotatable:true,
                rotationStops:4
            }
        }
    ]
}

new Palette({
    source:document.getElementById("my-palette"),
    selector:"[data-vjs-type]",
    ui:surface
});

```

Tap the meta key (CMD on mac) to rotate an element by steps as you are dragging it from the palette in this canvas:

FOO

BAR

### Rotation speed[​](#rotation-speed "Direct link to Rotation speed")

With free rotation (no `rotationStops` specified), elements will take 2000ms to perform an entire 360 degree rotation. This can be changed via the `rotationSpeed` setting on the resizing tools plugin:

```javascript
{
    type:ResizingToolsPlugin.type,
    options:{
        rotatable:true,
        rotationStops:4
    }
}

```

## Drop on edge[​](#drop-on-edge "Direct link to Drop on edge")

To configure the palette to allow dropping a new vertex onto an existing edge, which will then be split, set `allowDropOnEdge` to be true on the palette options:

```javascript
import { Palette } from "@visuallyjs/browser-ui"

const surface = null // your Surface instance

new Palette({
    source:document.getElementById("my-palette"),
    selector:"[data-vjs-type]",
    ui:surface,
    allowDropOnEdge:true
});

```

FOO

BAR

This is the simplest configuration, in which we instruct the palette to allow any vertex to be dropped on an edge. If you want more fine-grained control, you can supply a function instead, of this type:

```typescript
export type CanDropOnEdgeFilter = (d: ObjectData) => boolean;

```

The function is invoked with the payload for the item that is currently being dragged.

## Getting notification of a new vertex[​](#getting-notification-of-a-new-vertex "Direct link to Getting notification of a new vertex")

You can create a `Palette` with an `onVertexAdded` callback, which will be invoked whenever a new vertex has been dropped onto the canvas:

```javascript
new Palette({    
    ui:SomeSurfaceWidget,
    source:someElement,
    selector:".draggable-child",
    onVertexAdded(vertex, dropTarget) => {
        
    }  
})

```

`vertex` is the new vertex that was added. In the event that the new vertex was dropped on top of some existing node, `dropTarget` will be provided, containing information about the node onto which the new vertex was dropped, as well as its position and size.

## Working with decorators[​](#working-with-decorators "Direct link to Working with decorators")

If you have any Decorators in your UI, you may wish to inform the Palette about the elements they have created, because without doing this the Palette will not be able to recognise them as background. To do this, you use the `canvasSelector` option:

```javascript
new Palette({    
    ui:SomeSurfaceWidget,
    source:someElement,
    selector:".draggable-child",
    canvasSelector:".someElementMyDecoratorCreated",
      ...
})

```

`canvasSelector` takes any valid CSS3 selector. This identifies the elements that your decorator has created that the Palette should treat as background.

## CSS[​](#css "Direct link to CSS")

| Class                                  | Description                                                                                                                                                                                      |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `vjs-palette-auto-edge-connect-active` | Assigned to the UI's canvas when a drag has started and auto edge connect is active.                                                                                                             |
| `vjs-palette-current-shape-type`       | Assigned to a shape in a ShapePalette that matches the type of the model's currently selected shape.                                                                                             |
| `vjs-palette-drag-active`              | Assigned to possible drop targets when an element is being dragged from the Palette                                                                                                              |
| `vjs-palette-drag-hover`               | Assigned to a drop target when an element that is being dragged from the Palette is hovering over it.                                                                                            |
| `vjs-palette-drag-hover-cannot-drop`   | Assigned to a vertex or the canvas when an element that is being dragged from the palette is hovering over it but drop is not allowed.                                                           |
| `vjs-palette-current`                  | Assigned to an element when it is being dragged from a palette                                                                                                                                   |
| `vjs-palette-selected-element`         | Assigned to the currently selected element in a palette when in tap/draw mode.                                                                                                                   |
| `vjs-palette-tap-mode-active`          | Assigned to the surface canvas when a user has tapped an element in a palette in tap mode. this class can be used to show the user that a vertex can be dropped via click or drawn on the canvas |

In order to use these classes for visual cues in the UI, you'll probably want to define slightly different selectors for each target type. Let's suppose when a drag starts we want to outline our canvas and any nodes/groups with a purple line, and we want to draw any possible target edges with a purple line too:

```css
.vjs-surface.vjs-palette-active, .vjs-node.vjs-palette-active, .vjs-group.vjs-palette-active {
    outline:4px solid purple;
}

svg.vjs-palette-active path {
    stroke:purple;
}

```

Now when something is the current drop target, we'll either outline it green or make its path green:

```css
.vjs-surface.vjs-palette-hover, .vjs-node.vjs-palette-hover, .vjs-group.vjs-palette-hover {
    outline:4px solid green;
}

svg.vjs-palette-hover path {
    stroke:green;
}

```

This is just an example of course. You can do anything with the CSS that you like.

***

## Options[​](#options "Direct link to Options")

PaletteOptions

Options for a Palette

| Name                      | Type                                                                                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------- | -------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowClickToAdd?          | boolean                                                                                                  | When in draw mode, allow addition of new vertices simply by clicking, instead of requiring a shape be drawn. (When this is true, the drag to draw functionality also still works)                                                                                                                                                                                                                                                                                                               |
| allowDropOnCanvas?        | boolean                                                                                                  | Defaults to true. Allows items to be dropped onto whitespace.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| allowDropOnEdge?          | boolean \| CanDropOnEdgeFilter                                                                           | Defaults to false. Allows items to be dropped onto edges in the canvas. A drop on an edge causes that edge to be split, with one edge having the new vertex as a target, and another edge with the new vertex as source.                                                                                                                                                                                                                                                                        |
| allowDropOnGroup?         | boolean                                                                                                  | Defaults to true. Allows items to be dropped onto groups in the canvas.                                                                                                                                                                                                                                                                                                                                                                                                                         |
| allowDropOnNode?          | boolean                                                                                                  | Defaults to false. Allows items to be dropped onto nodes in the canvas. If this is true and an element is dropped onto a node, the result is the same as if the element has been dropped onto whitespace. Note that when this is false and the user has dragged something over a node, the drag item is still not considered to be over the canvas, and releasing the mouse button at that time will not cause a new node to be added. Use `ignoreDropOnNode` if that's the behaviour you want. |
| allowRotation?            | boolean                                                                                                  | Whether or not to allow rotation of elements being dragged. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| autoEdgeConnect?          | boolean \| [AutoEdgeConnectOptions]()                                                                    | Controls whether the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements. You can set this to simply 'true', and use defaults, or you can provide values for various options.                                                                                                                                                              |
| canDrop?                  | (candidate:[Node]() \| [Group](), target:[Node]() \| [Group](), onCanvas:boolean) => boolean             | Optional function that is invoked at the start of a drag, and which identifies allowed drop targets. Each target - the canvas, nodes and groups - is passed in turn to this method; returning false indicates that the given target is not valid for that drag.                                                                                                                                                                                                                                 |
| canvasDropFilter?         | [CanvasDropFilter]()                                                                                     | Optional function that you can use to inform the Palette that drop should be aborted. This method is invoked at the start of a drag (in drag mode) or when an item is tapped (in tap/draw mode) and is passed the candidate drag object's data.                                                                                                                                                                                                                                                 |
| clickToAddOnly?           | boolean                                                                                                  | This flag relates to "draw" mode, and defaults to false. When true, the palette only supports click to draw new vertices, not drag. This flag is forced to true if the associated UI does not have `useModelForSizes` set, since there is no point in allowing a user to drag a vertex to some size if its not going to be honoured. When you set this flag and associated UI does have `useModelForSizes` set, the palette will use default sizes for new nodes/groups.                        |
| contentTemplate?          | string                                                                                                   | Optional template that will be used in conjunction with `data` to generate the HTML content of the palette. The template can return any number of elements (ie. you're not limited to just a single root node)                                                                                                                                                                                                                                                                                  |
| data?                     | [ObjectData]()                                                                                           | Optional data that will be used in conjunction with `contentTemplate` to generate the HTML content of the palette.                                                                                                                                                                                                                                                                                                                                                                              |
| dataGenerator?            | [DataGeneratorFunction]()                                                                                | Optional function to generate an initial payload from an element that has started to be dragged/has been tapped.                                                                                                                                                                                                                                                                                                                                                                                |
| dragActiveClass?          | string                                                                                                   | Class to set on the UI canvas and any other drop targets when a new element is being dragged                                                                                                                                                                                                                                                                                                                                                                                                    |
| dragElementClass?         | string                                                                                                   | Class to set on an element being dragged.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| dragHoverCannotDropClass? | string                                                                                                   | Class to set on the UI canvas and any other drop targets when a drag element is hovering over it but drop is not allowed.s                                                                                                                                                                                                                                                                                                                                                                      |
| dragHoverClass?           | string                                                                                                   | Class to set on the UI canvas and any other drop targets when a drag element is hovering over it.                                                                                                                                                                                                                                                                                                                                                                                               |
| dragSize?                 | [Size]()                                                                                                 | Optional size to use for elements dragged from the palette; used in drag mode only.                                                                                                                                                                                                                                                                                                                                                                                                             |
| dragSizeGenerator?        | (payload:[ObjectData](), el:[BrowserElement]()) => [Size]()                                              | Optional function to generate the size to use for some object that is being dragged.                                                                                                                                                                                                                                                                                                                                                                                                            |
| edgeDropHandler?          | (newVertex:[Vertex](), originalEdge:[Edge]()) => [EdgeDropInfo]()                                        | If `allowDropOnEdge` is true, this function can be provided, to customise the behaviour of the drop. By default, the new vertex is used as the target of the original edge and the source of the new edge. But you might want to connect to ports on the new vertex, and this method allows you to do that: you can return the ID of a port to use for the existing edge's target, a port ID to use for the new edge's source, a source anchor or a target anchor.                              |
| elementGenerator?         | (el:[BrowserElement](), e:MouseEvent) => [BrowserElement]()                                              | Optional function you can provide which will be used to generate an element to use for dragging. The default behaviour is to use a clone of the element the user began dragging, but if you provide this method you can customise that.                                                                                                                                                                                                                                                         |
| enabled?                  | boolean                                                                                                  | Defaults to true. Set to false if you wish to instantiate the Palette in a disabled state                                                                                                                                                                                                                                                                                                                                                                                                       |
| groupIdentifier?          | [GroupIdentifierFunction]()                                                                              | Optional function to use to determine if the element being dragged/has been tapped represents a group. If you do not provide this, the default behaviour is to check for the presence of a `data-vjs-is-group` attribute on the element, with a value of `true`.                                                                                                                                                                                                                                |
| ignoreDropOnNode?         | boolean                                                                                                  | Defaults to false. When true, the palette treats nodes as if they are part of the canvas - a user can drag new items on top of existing nodes and the new item will be added to the canvas. If you want to force your users to drop on canvas whitespace, don't set this. Note that this flag will force `allowDropOnNode` to `false`.                                                                                                                                                          |
| ignoreGrid?               | boolean                                                                                                  | Defaults to false. By default this class will conform to any grid in place in the surface to which it is attached when dragging items around.                                                                                                                                                                                                                                                                                                                                                   |
| ignoreZoom?               | boolean                                                                                                  | By default, the Palette will apply a `scale` transform to elements that are being dragged so that they appear at the same size as the UI they're being dragged to. Setting this flag to true will switch off that behaviour.                                                                                                                                                                                                                                                                    |
| lassoClass?               | string                                                                                                   | When in 'draw' mode, you can optionally provide a class to set on the lasso used by the vertex drawing plugin.                                                                                                                                                                                                                                                                                                                                                                                  |
| mode?                     | PaletteMode                                                                                              | Mode to operate in - 'drag', 'tap' or 'draw'. Defaults to 'drag'.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| onDrag?                   | [DragFunction]()                                                                                         | Optional function to invoke as the user is dragging a new element, or has tapped an element and is moving the mouse over the canvas.                                                                                                                                                                                                                                                                                                                                                            |
| onVertexAdded?            | [OnVertexAddedCallback]()                                                                                | Optional callback that will be invoked after a new vertex has been dropped and added to the dataset.                                                                                                                                                                                                                                                                                                                                                                                            |
| rotationSpeed?            | number                                                                                                   | The number of milliseconds required to complete a full rotation of an element when the trigger key is held down. Defaults to 2000.                                                                                                                                                                                                                                                                                                                                                              |
| selectAfterAdd?           | boolean                                                                                                  | Defaults to false. When true, a newly added vertex is set as the model's current selection.                                                                                                                                                                                                                                                                                                                                                                                                     |
| selector?                 | string                                                                                                   | A CSS selector identifying children of `source` that are draggable/can be tapped. If not provided, the Palette will use `[data-vjs-type]`.                                                                                                                                                                                                                                                                                                                                                      |
| source                    | [BrowserElement]()                                                                                       | The element containing things that will be dragged/tapped.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| typeGenerator?            | [TypeGeneratorFunction]()                                                                                | Optional function to determine the type of the data object from an element that is being dragged (in drag mode) or has been tapped (in draw/tap mode)                                                                                                                                                                                                                                                                                                                                           |
| vertexPreviewGenerator?   | (objectType:string, type:string, data:[ObjectData](), p:[PointXY](), e:MouseEvent) => [BrowserElement]() | When in draw mode, this function can be used to provide the element shown to the user as a new vertex is being drawn.                                                                                                                                                                                                                                                                                                                                                                           |
| vertexPreviewUpdater?     | (el:[BrowserElement](), origin:[PointXY](), size:[Size](), data:[ObjectData]()) => any                   | When in draw mode this function is repeatedly called as the mouse is dragging a new shape. It provides a hook for you to update the element's appearance. This is only called if you provided a vertexPreviewGenerator and it has returned a valid DOM element at the start of a drag.                                                                                                                                                                                                          |

By default, the `Palette` is configured to allow nodes/groups to be dropped onto the canvas or an existing edge, and for nodes to be dropped on groups. You can control this via the appropriate `allowDropOn***` flags.
