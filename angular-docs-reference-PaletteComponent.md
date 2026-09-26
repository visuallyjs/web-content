# Palette

HTML Attribute

**vjs-palette**

Provides a palette from which your users can select nodes or groups to add to a canvas. Two modes are supported - the default is to allow users to drag nodes or groups from the palette element onto a canvas using touch/pointer events; it is also possible to run the palette in `tap` mode, in which a user first selects a node/group in the palette by clicking it, and then subsequently clicks on the canvas where they would like to place a new object of that type.

## Usage[​](#usage "Direct link to Usage")

Technically, this component is an Angular `Directive`: it does not declare its own template - instead, you use an attribute to instruct Angular to instantiate one.

```typescript
import { Component } from "@angular/core"

@Component({
   template:`<div>
   
  <vjs-surface data={...}/>
  
  <div style="display:flex;flex-direction:column" 
        vjs-palette selector="div">
    <h1>Item Type 1</h1>
    <div data-vjs-type="type11">Type 1</div>
    <div data-vjs-type="groupType1" data-vjs-is-group="true">Group Type 1</div>
    <h1>Item Type 2</h1>
    <div data-vjs-type="type21">Type 21</div> 
  </div>
</div>` 
})
export class MyApp {
    data = { ... }
}  

```

* The `vjs-palette` attribute declared on the `div` is the hook Angular uses to know it should instantiate a `PaletteComponent` on that element.
* The `selector="div"` attribute tells VisuallyJs what CSS3 selector it should use to determine which child elements of the palette represent draggable items. This selector is simple, but any valid selector will do. In this case VisuallyJs will ignore the `<h1>` elements.
* The `data-vjs-type` attribute on the draggable elements tells VisuallyJs what type of data object each element represents.
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

## Definition[​](#definition "Direct link to Definition")

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
