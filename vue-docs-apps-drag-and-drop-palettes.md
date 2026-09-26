# Palettes

A common use case in the sorts of applications for which VisuallyJs is useful is the requirement to be able to drag and drop new nodes/groups onto the workspace.

## Setup[​](#setup "Direct link to Setup")

To configure your UI to drag and drop HTML elements onto your canvas, you'll use a `PaletteComponent`.

```html
<script setup>
    
    
</script>
<template>
  <SurfaceProvider>
    <SurfaceComponent .../>
    <PaletteComponent>
      <div style="dusplay:flex;dlex-direction:column">
		  <div data-vjs-type="hello" data-vjs-label="new hello">Hello</div>
		  <div data-vjs-type="world" data-vjs-label="new world">World</div>
      </div>
    </PaletteComponent>
  </SurfaceProvider>
    
</template>


```

The basic contract is that you declare a `PaletteComponent` in your template, and then you write out the children that should be draggable however you like - in this case we use a `div` with flex column and an `div` for each draggable type, a pretty common setup. The palette identifies draggable elements, by default, by the fact that they have a `data-vjs-type` attribute set on them. You can override this default behaviour by providing your own `dataGenerator` - see below.

The `PaletteComponent` needs to know which surface it is going to be attached to, and it does this by being context aware - in the code above we have a `SurfaceProvider` wrapping both the surface component and the palette component. When the surface component is instantiated, it populates the surface provider's context, and the palette component is notified of the surface to use.

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

You can supply a `dataGenerator` function if you want to customise the initial dataset for dragged elements:

```html
<script setup>
    
  const dataGenerator = (el) => {
    const type = el.getAttribute("data-vjs-type")
      return {
        type,
        width:120,
        height:80, 
        timestamp:new Date().getTime()
      }
  }
    
</script>
<template>
<SurfaceProvider>
  <SurfaceComponent .../>
  <PaletteComponent :dataGenerator="dataGenerator">
    <div data-vjs-type="hello" data-vjs-label="new hello">Hello</div>
    <div data-vjs-type="world" data-vjs-label="new world">World</div>
  </PaletteComponent>
</SurfaceProvider>
</template>

```

Here, our data generator extracts the `data-vjs-type` to use for the new node's type, then sets a fixed value for width and height, and adds a timestamp.

## Distinguishing between a node and a group[​](#distinguishing-between-a-node-and-a-group "Direct link to Distinguishing between a node and a group")

By default, VisuallyJs will look for a `data-vjs-is-group` attribute on a dragged element. If the value of this attribute is `"true"`, VisuallyJs will assume the element represents a group. You can provide your own `groupIdentifier` if you wish.

## Specifying the size for a new element[​](#specifying-the-size-for-a-new-element "Direct link to Specifying the size for a new element")

```html
<script setup>
    
  const dragSize = {width:100,height:80}
    
</script>
<template>
  <SurfaceProvider>
    <SurfaceComponent .../>
    <PaletteComponent selector="div" :dragSize="dragSize">
      <div data-vjs-type="hello" data-vjs-label="new hello">Hello</div>
      <div data-vjs-type="world" data-vjs-label="new world">World</div>
    </PaletteComponent>
  </SurfaceProvider>
    
</template>


```

## Filtering draggable elements[​](#filtering-draggable-elements "Direct link to Filtering draggable elements")

It is possible, when drag starts, to decide whether or not you want the dragged element to be droppable on the canvas, via the `canvasDropFilter` prop:

```html
<script setup>
    
  const canvasDropFilter = (data) => {
      return data.type === "someDroppableOnCanvasType"
  }
    
</script>
<template>
  <SurfaceProvider>
    <SurfaceComponent .../>
    <PaletteComponent selector="div" :canvasDropFilter="canvasDropFilter">
      <div data-vjs-type="hello" data-vjs-label="new hello">Hello</div>
      <div data-vjs-type="world" data-vjs-label="new world">World</div>
    </PaletteComponent>
  </SurfaceProvider>
    
</template>


```

## Rotating dragged elements[​](#rotating-dragged-elements "Direct link to Rotating dragged elements")

Since:

<!-- -->

1.2.5

You can rotate an element that you are dragging from the palette before dropping it, if you have the `ResizingToolsPlugin` installed on your canvas and you have *not* explicitly set `allowRotation:false` on the palette.

To configure the palette to allow rotation, set `rotatable` to be true in the `ResizingToolsPlugin` options:

```html
<template>
  <SurfaceProvider>
    <div class="col-9">
      <SurfaceComponent :renderOptions="renderOptions"/>
    </div>
    <div class="col-3">
        <PaletteComponent>
            <div style="display:flex; flex-direction:column">
                <div data-vjs-type="foo" vjs-is-group="true" data-vjs-label="New Foo">FOO</div>
                <div data-vjs-type="bar" data-vjs-label="New Bar">BAR</div>
            </div>
        </PaletteComponent>
    </div>
  </SurfaceProvider>
</template>

<script setup>
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
</script>

```

Hold down the meta key (CMD on mac) to rotate an element as you are dragging it from the palette in this canvas:

FOO

BAR

### Rotation stops[​](#rotation-stops "Direct link to Rotation stops")

If you specify `rotationStops` in your resizing tools options, the palette will honour them:

```html
<template>
  <SurfaceProvider>
    <div class="col-9">
      <SurfaceComponent :renderOptions="renderOptions"/>
    </div>
    <div class="col-3">
        <PaletteComponent>
            <div style="display:flex; flex-direction:column">
                <div data-vjs-type="foo" vjs-is-group="true" data-vjs-label="New Foo">FOO</div>
                <div data-vjs-type="bar" data-vjs-label="New Bar">BAR</div>
            </div>
        </PaletteComponent>
    </div>
  </SurfaceProvider>
</template>

<script setup>
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
</script>

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

To configure the palette to allow dropping a new vertex onto an existing edge, which will then be split, set `allowDropOnEdge` to be true on the palette props:

```html
<template>
  <SurfaceProvider>
    <div class="col-9">
      <SurfaceComponent/>
    </div>
    <div class="col-3">
        <PaletteComponent :allowDropOnEdge="true">
            <div style="display:flex; flex-direction:column">
                <div data-vjs-type="foo" vjs-is-group="true" data-vjs-label="New Foo">FOO</div>
                <div data-vjs-type="bar" data-vjs-label="New Bar">BAR</div>
            </div>
        </PaletteComponent>
    </div>
  </SurfaceProvider>
</template>

<script setup>
    import { PaletteComponent, SurfaceComponent, SurfaceProvider } from '@visuallyjs/browser-ui-vue';
</script>

```

FOO

BAR

This is the simplest configuration, in which we instruct the palette to allow any vertex to be dropped on an edge. If you want more fine-grained control, you can supply a function instead, of this type:

```typescript
export type CanDropOnEdgeFilter = (d: ObjectData) => boolean;

```

The function is invoked with the payload for the item that is currently being dragged.

## Getting notification of a new vertex[​](#getting-notification-of-a-new-vertex "Direct link to Getting notification of a new vertex")

You can supply an `onVertexAdded` callback, which will be invoked whenever a new vertex has been dropped onto the canvas:

```html
<script setup>
    
  const onVertexAdded = (vertex, dropTarget) => {
	  ...
  }
    
</script>
<template>
  <SurfaceProvider>
    <SurfaceComponent .../>
    <PaletteComponent selector="div" :onVertexAdded="onVertexAdded">
      <div data-vjs-type="hello" data-vjs-label="new hello">Hello</div>
      <div data-vjs-type="world" data-vjs-label="new world">World</div>
    </PaletteComponent>
  </SurfaceProvider>
    
</template>


```

`vertex` is the new vertex that was added. In the event that the new vertex was dropped on top of some existing node, `dropTarget` will be provided, containing information about the node onto which the new vertex was dropped, as well as its position and size.

## Working with decorators[​](#working-with-decorators "Direct link to Working with decorators")

If you have any Decorators in your UI, you may wish to inform the drop manager about the elements they have created, because without doing this the drop manager will not be able to recognise them as background. To do this, you use the `canvasSelector` prop:

```html
<script setup>
    
</script>
<template>
  <SurfaceProvider>
    <SurfaceComponent .../>
    <PaletteComponent selector="div" canvasSelector=".someElementMyDecoratorCreated">
      <div data-vjs-type="hello" data-vjs-label="new hello">Hello</div>
      <div data-vjs-type="world" data-vjs-label="new world">World</div>
    </PaletteComponent>
  </SurfaceProvider>
    
</template>


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

PaletteComponentProps

Props for the `PaletteComponent`

| Name               | Type                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------ | ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowClickToAdd?   | boolean                               | When in draw mode, allow addition of new vertices simply by clicking, instead of requiring a shape be drawn. (When this is true, the drawing method also still works)                                                                                                                                                                                                                                                                                                                           |
| allowDropOnCanvas? | boolean                               | Whether or not to allow drop on whitespace in the canvas. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| allowDropOnEdge?   | boolean                               | Whether or not to allow drop on edge. Defaults to false.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| allowDropOnGroup?  | boolean                               | Whether or not to allow drop on existing vertices. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| allowDropOnNode?   | boolean                               | Defaults to false. Allows items to be dropped onto nodes in the canvas. If this is true and an element is dropped onto a node, the result is the same as if the element has been dropped onto whitespace. Note that when this is false and the user has dragged something over a node, the drag item is still not considered to be over the canvas, and releasing the mouse button at that time will not cause a new node to be added. Use `ignoreDropOnNode` if that's the behaviour you want. |
| allowRotation?     | boolean                               | Whether or not to allow rotation of elements being dragged. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| autoEdgeConnect?   | boolean \| [AutoEdgeConnectOptions]() | If true, the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements.                                                                                                                                                                                                                                                                          |
| canvasDropFilter?  | [CanvasDropFilter]()                  | Optional filter to test if objects may be dropped on the canvas.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| className?         | string                                | Optional extra css classes to set on the element                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| clickToAddOnly?    | boolean                               | This flag relates to "draw" mode, and defaults to false. When true, the palette only supports click to draw new vertices, not drag. This flag is forced to true if the associated UI does not have `useModelForSizes` set, since there is no point in allowing a user to drag a vertex to some size if its not going to be honoured. When you set this flag and associated UI does have `useModelForSizes` set, the palette will use default sizes for new nodes/groups.                        |
| dataGenerator?     | [DataGeneratorFunction]()             | Function to use to get a dataset for an item that is being dragged/has been tapped. If omitted, Visually JS will use a default data generator that extracts data values from any `data-vjs-***` attribute on the element being dragged.                                                                                                                                                                                                                                                         |
| dragSize?          | [Size]()                              | Optional size to use for elements dragged from the palette; used in drag mode only.                                                                                                                                                                                                                                                                                                                                                                                                             |
| groupIdentifier?   | [GroupIdentifierFunction]()           | Function to use to determine whether an item that is being dragged/has been tapped represents a group.                                                                                                                                                                                                                                                                                                                                                                                          |
| ignoreDropOnNode?  | boolean                               | Defaults to false. When true, the palette treats nodes as if they are part of the canvas - a user can drag new items on top of existing nodes and the new item will be added to the canvas. If you want to force your users to drop on canvas whitespace, don't set this. Note that this flag will force `allowDropOnNode` to `false`.                                                                                                                                                          |
| mode?              | PaletteMode                           | Mode to operate in - 'drag', 'tap' or 'draw'. Defaults to 'drag'.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| onVertexAdded?     | [OnVertexAddedCallback]()             | Optional callback that will be invoked after a new vertex has been dropped and added to the dataset.                                                                                                                                                                                                                                                                                                                                                                                            |
| rotationSpeed?     | number                                | The number of milliseconds required to complete a full rotation of an element when the trigger key is held down. Defaults to 2000.                                                                                                                                                                                                                                                                                                                                                              |
| selectAfterAdd?    | boolean                               | Defaults to false. When true, a newly added vertex is set as the model's current selection.                                                                                                                                                                                                                                                                                                                                                                                                     |
| selector?          | string                                | CSS 3 selector identifying what child elements of `container` are draggable/can be tapped. Optional. If omitted, a default of `[data-vjs-type]` will be used.                                                                                                                                                                                                                                                                                                                                   |
| showGroups?        | boolean                               | Whether or not to show groups in the palette. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| surface?           | [Surface]()                           | The surface to attach to. Optional: this component can derive a surface from a SurfaceProvider or SurfaceComponent. You'll only need this in certain advanced scenarios.                                                                                                                                                                                                                                                                                                                        |
| typeGenerator?     | [TypeGeneratorFunction]()             | Function to use to get the type of an item that is being dragged/has been tapped.                                                                                                                                                                                                                                                                                                                                                                                                               |
