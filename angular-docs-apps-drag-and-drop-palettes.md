# Palettes

A common use case in the sorts of applications for which VisuallyJs is useful is the requirement to be able to drag and drop new nodes/groups onto the workspace.

## Setup[​](#setup "Direct link to Setup")

To configure your UI to drag and drop HTML elements onto your canvas, you'll use a `PaletteComponent`, which is a `directive` you declare via the inclusion of a specific attribute on some element in your template:

```html
<div class="sidebar node-palette" 
     vjs-palette >
  <div *ngFor="let nodeType of nodeTypes" 
            [attr.data-vjs-type]="nodeType.type"
            [attr.data-vjs-label="nodeType.label"
            [attr.data-vjs-width]="nodeType.w" 
            [attr.data-vjs-height]="nodeType.h">{{nodeType.label}}</div>
</div>

```

The basic contract is that you declare the **vjs-palette** attribute on some element, identifying it as a `PaletteComponent`. You then write out the child elements using whatever markup you like, and VisuallyJs will locate them via the fact that they have a `data-vjs-type` attribute declared. You can override this default behaviour by providing your own `dataGenerator` - see below.

The `PaletteComponent` also needs to know which surface to attach to. You can provide a `surfaceId` input to identify your surface, but if you do not, VisuallyJs will use the default ID. For the vast majority of apps - having only a single surface - you can safely omit the `surfaceId` and use the default.

The `PaletteComponent` will automatically prepare a dataset for a newly dragged node/group by reading any `data-vjs-***` attributes from the element the user dragged. You can override this behaviour by providing a `dataGenerator` - see below.

FOO

BAR

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

If you want to override the default dataset generation, you can provide your own `dataGenerator` function:

```javascript
export class AppComponent {
    
    dataGenerator(el:Element) {
        return {
            type:el.getAttribute("data-vjs-type"),
            width:80,
            height:60,
            timestamp:new Date().getTime()
        }
    } 
    
}

```

```html
<div class="sidebar node-palette" 
     vjs-palette>
    @for(nodeType of nodeTypes;track nodeType) {
      <div [attr.data-vjs-type]="nodeType.type" 
            [attr.data-vjs-width]="nodeType.width" 
            [attr.data-vjs-height]="nodeType.height">{{nodeType.label}}</div>
    }
</div>

```

Here, our data generator extracts the `data-vjs-type` to use for the new node's type, then sets a fixed value for width and height, and adds a timestamp.

## Distinguishing between a node and a group[​](#distinguishing-between-a-node-and-a-group "Direct link to Distinguishing between a node and a group")

By default, VisuallyJs will look for a `data-vjs-is-group` attribute on a dragged element. If the value of this attribute is `"true"`, VisuallyJs will assume the element represents a group. You can provide your own `groupIdentifier` if you wish.

## Specifying the size for a new element[​](#specifying-the-size-for-a-new-element "Direct link to Specifying the size for a new element")

By default, the `PaletteComponent` clones the DOM element on which the user started a drag and then sets the size of the element that is being dragged to match the bounding client rectangle of the element that was cloned.

In some situations, for instance when you have a grid in your surface, you may wish to mandate the size for any new elements that are being dragged on to the surface, which you can do by providing a `dragSize` input:

```javascript
export class AppComponent {
    dragSize = { width:100,height:80 }
}

```

```html
<div class="sidebar node-palette" 
     vjs-palette 
     selector="div" 
     [dragSize]="dragSize">
    
    @for(nodeType of nodeTypes;track nodeType) {
        <div [attr.data-vjs-type]="nodeType.type" 
            [attr.data-vjs-width]="nodeType.w" 
            [attr.data-vjs-height]="nodeType.h">{{nodeType.label}}</div>
    }
            
</div>

```

## Filtering draggable elements[​](#filtering-draggable-elements "Direct link to Filtering draggable elements")

It is possible, when drag starts, to decide whether or not you want the dragged element to be droppable on the canvas, via the `canvasDropFilter` input:

```javascript
export class AppComponent {
    canvasDropFilter(data: ObjectData): boolean {
        return data.type === "someDroppableOnCanvasType"
    }
}

```

```html
<div class="sidebar node-palette" 
     vjs-palette 
     selector="div" 
     [canvasDropFilter]="canvasDropFilter">
    
  @for(nodeType of nodeTypes;track nodeType) {    
    <div [attr.data-vjs-type]="nodeType.type" 
            [attr.data-vjs-width]="nodeType.width" 
            [attr.data-vjs-height]="nodeType.height">{{nodeType.label}}</div>
  }  
            
</div>

```

## Rotating dragged elements[​](#rotating-dragged-elements "Direct link to Rotating dragged elements")

Since:

<!-- -->

1.2.5

You can rotate an element that you are dragging from the palette before dropping it, if you have the `ResizingToolsPlugin` installed on your canvas and you have *not* explicitly set `allowRotation:false` on the palette.

To configure the palette to allow rotation, set `rotatable` to be true in the `ResizingToolsPlugin` options:

```typescript
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

```

```html
<vjs-surface [renderOptions]="renderOptions">

```

Hold down the meta key (CMD on mac) to rotate an element as you are dragging it from the palette in this canvas:

FOO

BAR

### Rotation stops[​](#rotation-stops "Direct link to Rotation stops")

If you specify `rotationStops` in your resizing tools options, the palette will honour them:

```typescript
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

```

```html
<vjs-surface [renderOptions]="renderOptions">

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

To configure the palette to allow dropping a new vertex onto an existing edge, which will then be split, set `allowDropOnEdge` to be true on the element that has the `vjs-palette` directive:

```html
<div class="row">
    <div class="col-9">
      <vjs-surface/>
    </div>
    <div class="col-3">
        <div vjs-palette [allowDropOnEdge]="true">
            <div style="display:flex; flex-direction:column">
                <div data-vjs-type="foo" vjs-is-group="true" data-vjs-label="New Foo">FOO</div>
                <div data-vjs-type="bar" data-vjs-label="New Bar">BAR</div>
            </div>
        </div>
    </div>
</div>

```

FOO

BAR

This is the simplest configuration, in which we instruct the palette to allow any vertex to be dropped on an edge. If you want more fine-grained control, you can supply a function instead, of this type:

```typescript
export type CanDropOnEdgeFilter = (d: ObjectData) => boolean;

```

The function is invoked with the payload for the item that is currently being dragged.

## Getting notification of a new vertex[​](#getting-notification-of-a-new-vertex "Direct link to Getting notification of a new vertex")

You can create a `PaletteComponent` with an `onVertexAdded` callback, which will be invoked whenever a new vertex has been dropped onto the canvas:

```javascript
export class AppComponent {
    onVertexAdded(v:Vertex, dropTarget?:{pos:PointXY, vertex:Node|Group, size:Size}):any {
        ...
    }
}

```

```html
<div class="sidebar node-palette" 
     vjs-palette
     selector="div" 
     [onVertexAdded]="onVertexAdded">
     
  @for(nodeType of nodeTypes;track nodeType) {
    <div [attr.data-vjs-type]="nodeType.type" 
            [attr.data-vjs-width]="nodeType.width" 
            [attr.data-vjs-height]="nodeType.height">{{nodeType.label}}</div>
  }  
            
</div>

```

## Working with decorators[​](#working-with-decorators "Direct link to Working with decorators")

If you have any Decorators in your UI, you may wish to inform the drop manager about the elements they have created, because without doing this the drop manager will not be able to recognise them as background. To do this, you use the `canvasSelector` input:

```html
<div class="sidebar node-palette" 
     vjs-palette
     selector="div" 
     canvasSelector=".someElementMyDecoratorCreated">
     
  @for(nodeType of nodeTypes;track nodeType) {  
    <div [attr.data-vjs-type]="nodeType.type" 
            [attr.data-vjs-width]="nodeType.w" 
            [attr.data-vjs-height]="nodeType.h">{{nodeType.label}}</div>
  }  
            
</div>

```

`canvasSelector` takes any valid CSS3 selector. This identifies the elements that your decorator has created that the drop manager should treat as background.

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

### Inputs[​](#inputs "Direct link to Inputs")

| Name               | Type                                  | Description                                                                                                                                                                                                                                                                                                                        |
| ------------------ | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowDropOnCanvas? | boolean                               | Defaults to true. Allows items to be dropped onto whitespace.                                                                                                                                                                                                                                                                      |
| allowDropOnEdge?   | boolean \| CanDropOnEdgeFilter        | Defaults to true. Allows items to be dropped onto edges in the canvas.                                                                                                                                                                                                                                                             |
| allowDropOnGroup?  | boolean                               | Defaults to true. Allows items to be dropped onto groups in the canvas.                                                                                                                                                                                                                                                            |
| allowDropOnNode?   | boolean                               | Defaults to false. Allows items to be dropped onto nodes in the canvas. If this is true and an element is dropped onto a node, the result is the same as if the element has been dropped onto whitespace.                                                                                                                          |
| autoEdgeConnect?   | boolean \| [AutoEdgeConnectOptions]() | Controls whether the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements. You can set this to simply 'true', and use defaults, or you can provide values for various options. |
| canvasDropFilter?  | [CanvasDropFilter]()                  | Optional filter to test if objects may be dropped on the canvas. This method is invoked at the start of a drag and is passed the candidate drag object's data.                                                                                                                                                                     |
| dataGenerator?     | [DataGeneratorFunction]()             | Function to use to generate an initial payload when the user starts to drag something from this component, or taps on an item in tap/draw mode. Optional, and if omitted Visually JS will use a default data generator that extracts data values from any `data-vjs-***` attributes on the element being dragged.                  |
| dragSize?          | [Size]()                              | Optional size to use for dragged elements.                                                                                                                                                                                                                                                                                         |
| groupIdentifier?   | [GroupIdentifierFunction]()           | Optional function to use to determine if the object that is being dragged represents a group. If this function is present, and returns true, then the drag object is considered to be a group. In all other cases the drag object is considered to be a node.                                                                      |
| mode?              | PaletteMode                           | Mode to use - drag or tap. Defaults to drag.                                                                                                                                                                                                                                                                                       |
| onVertexAdded?     | [OnVertexAddedCallback]()             | Optional callback for when a new vertex has been added via this component.                                                                                                                                                                                                                                                         |
| selectAfterAdd?    | boolean                               | Defaults to false. When true, a newly added vertex is set as the model's current selection.                                                                                                                                                                                                                                        |
| selector?          | string                                | CSS3 selector identifying the child elements of the the element on which this directive was declared that act as drag sources. Optional; if omitted Visually JS will use `[data-vjs-type]`.                                                                                                                                        |
| typeGenerator?     | [TypeGeneratorFunction]()             | Optional function to use to determine the type of object that a user has just started dragging or tapped on                                                                                                                                                                                                                        |
