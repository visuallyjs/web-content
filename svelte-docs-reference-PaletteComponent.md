# \<PaletteComponent/>

Provides a palette from which your users can select nodes or groups to add to a canvas. Two modes are supported - the default is to allow users to drag nodes or groups from the palette element onto a canvas using touch/pointer events; it is also possible to run the palette in `tap` mode, in which a user first selects a node/group in the palette by clicking it, and then subsequently clicks on the canvas where they would like to place a new object of that type.

## Usage[​](#usage "Direct link to Usage")

```html
<script>
	import {SurfaceComponent, SurfaceProvider, PaletteComponent} from "@visuallyjs/browser-ui-svelte"
    
    const data = {
        nodes:[ ... ],
        edges:[ ... ]
    }
    
</script>
<SurfaceProvider>
  <SurfaceComponent data={data}/>
  <PaletteComponent>
    <div style="display:flex;flex-direction:column">
      <h1>Item Type 1</h1>
      <div data-vjs-type="type11">Type 1</div>
      <div data-vjs-type="groupType1" data-vjs-is-group="true">Group Type 1</div>    
      <h1>Item Type 2</h1>
      <div data-vjs-type="type21">Type 21</div>
    </div>
  </PaletteComponent>
</SurfaceProvider>    


```

* The `data-vjs-type` attribute on the draggable elements tells VisuallyJs what type of data object each element represents. This can be changed by providing a `selector` prop on the palette component.
* The `data-vjs-is-group="true"` attribute tells VisuallyJs that the item maps a Group, not a node

## Payloads[​](#payloads "Direct link to Payloads")

When a user adds a node/group to a canvas from a Palette, VisuallyJs will prepare an initial payload for the new object in one of two ways:

### Default extractor[​](#default-extractor "Direct link to Default extractor")

By default, any `data-vjs-***` attribute on the element in the Palette will have its value read and inserted into the payload. For instance, the attribute `data-vjs-label="hello"` will result in `{label:"hello"}`.

### Custom extractor[​](#custom-extractor "Direct link to Custom extractor")

If you provide a `dataGenerator`, you can control on a fine-grained level what the payload for new objects will be. This is a [DataGeneratorFunction]() whose type definition is:

`(el:BrowserElement) => ObjectData`

### Marking groups[​](#marking-groups "Direct link to Marking groups")

To inform VisuallyJs that a certain element represents a Group and not a Node, set `data-vjs-is-group="true"` on it:

```html
<div>
  <div data-vjs-type="foo">Foo NODE</div>
  <div data-vjs-type="bar" data-vjs-is-group="true">Bar GROUP</div>
</div>

```

## Props[​](#props "Direct link to Props")

PaletteComponentProps

| Name               | Type                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------ | ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowClickToAdd?   | boolean                               | When in draw mode, allow addition of new vertices simply by clicking, instead of requiring a shape be drawn. (When this is true, the drag to draw functionality also still works)                                                                                                                                                                                                                                                                                                               |
| allowDropOnCanvas? | boolean                               | Whether or not to allow drop on whitespace in the canvas. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| allowDropOnEdge?   | boolean \| CanDropOnEdgeFilter        | Whether or not to allow drop on edge. Defaults to false.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| allowDropOnGroup?  | boolean                               | Whether or not to allow drop on existing vertices. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| allowDropOnNode?   | boolean                               | Defaults to false. Allows items to be dropped onto nodes in the canvas. If this is true and an element is dropped onto a node, the result is the same as if the element has been dropped onto whitespace. Note that when this is false and the user has dragged something over a node, the drag item is still not considered to be over the canvas, and releasing the mouse button at that time will not cause a new node to be added. Use `ignoreDropOnNode` if that's the behaviour you want. |
| allowRotation?     | boolean                               | Whether or not to allow rotation of elements being dragged. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| autoEdgeConnect?   | boolean \| [AutoEdgeConnectOptions]() | Controls whether the palette will automatically connect a new vertex being dragged onto the canvas to existing vertices, if the shape definitions for the new vertex and/or the existing vertices have source/target elements. You can set this to simply 'true', and use defaults, or you can provide values for various options.                                                                                                                                                              |
| canvasDropFilter?  | [CanvasDropFilter]()                  | Optional filter to use to decide at run time which elements may be dragged/dropped                                                                                                                                                                                                                                                                                                                                                                                                              |
| className?         | string                                | Optional class name to set on the component's root element.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| clickToAddOnly?    | boolean                               | This flag relates to "draw" mode, and defaults to false. When true, the palette only supports click to draw new vertices, not drag. This flag is forced to true if the associated UI does not have `useModelForSizes` set, since there is no point in allowing a user to drag a vertex to some size if its not going to be honoured. When you set this flag and associated UI does have `useModelForSizes` set, the palette will use default sizes for new nodes/groups.                        |
| dataGenerator?     | [DataGeneratorFunction]()             | Function to invoke to get a payload for an element that is being dragged/has been tapped. Defaults to a function that extracts `type` from the element via its `data-vjs-type` attribute.                                                                                                                                                                                                                                                                                                       |
| dragSize?          | [Size]()                              | Optional size for elements dragged from the palette; used in drag mode only.                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ignoreDropOnNode?  | boolean                               | Defaults to false. When true, the palette treats nodes as if they are part of the canvas - a user can drag new items on top of existing nodes and the new item will be added to the canvas. If you want to force your users to drop on canvas whitespace, don't set this. Note that this flag will force `allowDropOnNode` to `false`.                                                                                                                                                          |
| mode?              | PaletteMode                           | Mode to operate in - 'drag', 'tap' or 'draw'. Defaults to 'drag'.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| onVertexAdded?     | [OnVertexAddedCallback]()             | Optional function to invoke after a vertex has been added                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| rotationSpeed?     | number                                | The number of milliseconds required to complete a full rotation of an element when the trigger key is held down. Defaults to 2000.                                                                                                                                                                                                                                                                                                                                                              |
| selectAfterAdd?    | boolean                               | Defaults to false. When true, a newly added vertex is set as the model's current selection.                                                                                                                                                                                                                                                                                                                                                                                                     |
| selector?          | string                                | CSS selector identifying draggable elements. Defaults to '\[data-vjs-type]'                                                                                                                                                                                                                                                                                                                                                                                                                     |
| showGroups?        | boolean                               | Whether or not to show groups in the palette. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
