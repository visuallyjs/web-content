# Controlling actions

Various actions and capabilities of a Diagram can be controlled by a [DiagramActionMediator](). This is an interface from which you can implement one or more methods that allow you to decide at runtime whether a given shape should offer various actions in its shape editing tools, whether it can be dragged, or whether it can be dropped onto some other vertex or the diagram canvas.

Each method in the mediator is optional. If a method is not provided, the diagram-wide settings for that operation are used. The mediator is only invoked if the diagram is in an editable state.

```html
<script>

import { DiagramComponent } from "@visuallyjs/browser-ui-svelte"
    
const data = ...
    
const options = {
  mediator: {
    canResize: (vertex, shape, el) => vertex.data.resizable === true,
    canLink: (vertex, shape, el) => vertex.data.linkable === true
  }
}
    
</script>    

<div class="my-container">
    <DiagramComponent data={data} options={options}/>
</div>

```

## Actions[​](#actions "Direct link to Actions")

info

The example implementations on this page come from our <!-- -->[BPMN](/demonstrations/bpmn.md) starter application.

### canResize[​](#canresize "Direct link to canResize")

Returns whether or not the given vertex should be resizable in the UI. Defaults to true, meaning the resize handles will be present in the diagram tools when the vertex is selected.

```typescript
canResize:(vertex: Vertex, shape: Shape, el: HTMLElement) => {
    return vertex.type === "pool" || vertex.type === "lane" || vertex.type === "group"
}

```

### canClone[​](#canclone "Direct link to canClone")

By default, Diagrams will display a clone icon - - on a selected shape. You can manage that on a per-shape basis by providing a `canClone` function:

```typescript
canClone:(vertex: Vertex, shape: Shape, el: HTMLElement) => {
    return vertex.type !== "pool" && vertex.type !== "lane"
}

```

Returning false will mean the icon is not shown.

### canLink[​](#canlink "Direct link to canLink")

Returns whether or not the given vertex should be linkable via edge drag in the UI. Defaults to true, meaning the link icon will be present in the diagram tools when the vertex is selected.

```typescript
canLink:(vertex: Vertex, shape: Shape, el: HTMLElement) => {
    return vertex.type !== "pool" && vertex.type !== "lane"
}

```

### canRotate[​](#canrotate "Direct link to canRotate")

Returns whether or not the given vertex should be resizable in the UI. Defaults to true, meaning the rotate handle and leader will be present in the diagram tools when the vertex is selected.

```typescript
canRotate:(vertex: Vertex, shape: Shape, el: HTMLElement) => {
    return false
}

```

### canDrag[​](#candrag "Direct link to canDrag")

The `canDrag` method is invoked when the user begins to drag a shape. It is passed the underlying vertex that is being dragged, the definition for the shape representing that vertex, and the SVG element from the DOM. Return `false` from this method if you wish to prevent drag.

```typescript
canDrag:(vertex: Vertex, shape: Shape, el: HTMLElement) => {
    return vertex.type !== "lane"
}

```

### canDrop[​](#candrop "Direct link to canDrop")

Returns whether or not the given vertex should be droppable on the given target, which may either be another vertex (if `targetVertex` is set), or the diagram canvas (if `isOnCanvas` is set). This method will never be called with both `targetVertex` set an `isOnCanvas` true - it's one or the other.

```typescript
canDrop:(candidate: Vertex, target: Vertex | null, onCanvas: boolean) => {
    // only allow lanes to be dropped into pools
    if (candidate.type === "lane") {
        return target != null && target.type === "pool"
    }

    // pools can only be dropped on the canvas
    if (candidate.type === "pool") {
        return onCanvas === true
    }

    // other types can be dropped on the canvas or into groups/lanes
    if (onCanvas) {
        return true
    }

    return target.type === "lane" || target.type === "group"
}

```

This action is invoked both when dragging shapes in the diagram and when dragging a shape onto the diagram from a palette.

***

## Interface definition[​](#interface-definition "Direct link to Interface definition")

The full definition for the `DiagramActionMediator` is:

DiagramActionMediator

Defines an object that can decide at runtime whether a given shape should offer various actions in its shape editing tools. Each method in this interface is optional, and does not override any diagram-wide settings for the specific operation. Also, the mediator will not be invoked if a diagram is not editable.

| Name         | Type                                                                                              | Description                                                                                                                                                                                                                                                                                                 |
| ------------ | ------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| canClone?    | (v:[Node]() \| [Group](), shape:[ShapeType](), el:[BrowserElement]()) => boolean                  | Returns whether or not the given vertex should be clonable in the UI. Defaults to true, meaning the clone icon will be present in the diagram tools.                                                                                                                                                        |
| canCollapse? | (group:[Group](), currentSize:[Size]()) => boolean \| [ObjectData]()                              | Returns whether or not the given group can be collapsed                                                                                                                                                                                                                                                     |
| canDelete?   | (v:[Node]() \| [Group](), shape:[ShapeType](), el:[BrowserElement]()) => boolean                  | Returns whether or not the given vertex should be deletable in the UI. Defaults to true, meaning the delete icon will be present in the diagram tools when the vertex is selected.                                                                                                                          |
| canDrag?     | (v:[Node]() \| [Group](), shape:[ShapeType](), el:[BrowserElement]()) => boolean                  | Returns whether or not the given vertex should be draggable in the UI. Defaults to true.                                                                                                                                                                                                                    |
| canDrop?     | (vertex:[Node]() \| [Group](), targetVertex:[Node]() \| [Group](), isOnCanvas:boolean) => boolean | Returns whether or not the given vertex should be droppable on the given target, which may either be another vertex (if `targetVertex` is set), or the diagram canvas (if `isOnCanvas` is set). This method will never be called with both `targetVertex` set an `isOnCanvas` true - it's one or the other. |
| canExpand?   | (group:[Group](), currentSize:[Size]()) => boolean \| [ObjectData]()                              | Returns whether or not the given group can be expanded                                                                                                                                                                                                                                                      |
| canLink?     | (v:[Node]() \| [Group](), shape:[ShapeType](), el:[BrowserElement]()) => boolean                  | Returns whether or not the given vertex should be linkable via edge drag in the UI. Defaults to true, meaning the link icon will be present in the diagram tools when the vertex is selected.                                                                                                               |
| canResize?   | (v:[Node]() \| [Group](), shape:[ShapeType](), el:[BrowserElement]()) => boolean                  | Returns whether or not the given vertex should be resizable in the UI. Defaults to true, meaning the resize handles will be present in the diagram tools when the vertex is selected.                                                                                                                       |
| canRotate?   | (v:[Node]() \| [Group](), shape:[ShapeType](), el:[BrowserElement]()) => boolean                  | Returns whether or not the given vertex should be resizable in the UI. Defaults to true, meaning the rotate handle and leader will be present in the diagram tools when the vertex is selected.                                                                                                             |
