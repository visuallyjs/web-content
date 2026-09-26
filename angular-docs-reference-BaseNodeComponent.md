# BaseNodeComponent

This component is what you must extend in any components you create to render nodes. It contains a few internal members that VisuallyJs needs, and also provides a number of helper methods you can use to manipulate the model object that your component represents.

The vertex this component represents is available on the class as `data` (a plain JS object), and `$data()` (a signal wrapping `data`).

## Usage[​](#usage "Direct link to Usage")

```typescript
import { Component } from "@angular/core"
import { BaseNodeComponent } from "@visuallyjs/browser-ui-angular"

@Component({
   template:`<div>
  <strong>{{data.label}}</strong>
</div>` 
})
export class MyNodeComponent extends BaseNodeComponent { }  

```

## Definition[​](#definition "Direct link to Definition")

### Class Members[​](#class-members "Direct link to Class Members")

| Name                                               | Type                           | Description                                                                                                                                                                                      |
| -------------------------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| $data                                              | WritableSignal<[ObjectData]()> | This signal represents the underlying data for the vertex this component represents.                                                                                                             |
| data                                               | [ObjectData]()                 | Data object for the vertex                                                                                                                                                                       |
| zoom                                               | WritableSignal\<number>        | This is a signal that provides the current zoom for the canvas the component is in. You can use this to selectively hide/show content based upon the zoom level.                                 |
| addNewPort(type:string, data:[ObjectData]())       | void                           | Instructs the model to add a new port with the given data to the vertex this component represents. This will call the model's `portFactory`.                                                     |
| addPort(data:[ObjectData]())                       | [Port]()                       | Adds a port with the given data to the vertex this component represents.                                                                                                                         |
| addToSelection()                                   | void                           | Adds the vertex this component represents to the current selection in the model.                                                                                                                 |
| cloneNode(options:[SurfaceVertexCloneOptions]())   | void                           | Instructs the model to clone this node - a new node which is a copy of this one will be added to the UI, with a position shifted slightly in X and Y from the cloned node.                       |
| cloneVertex(options:[SurfaceVertexCloneOptions]()) | void                           | Clones this vertex, optionally setting to a given position, or offsetting from the original, and optionally magnetizing the new vertex's position, and flashing it to show the user where it is. |
| flashNode(duration:number, animName:string)        | void                           | Flash this Node                                                                                                                                                                                  |
| getNode()                                          | [Node]()                       | Gets the node that this component represents.                                                                                                                                                    |
| getPort(portId:string)                             | [Port]()                       | Gets the port with the given ID                                                                                                                                                                  |
| getVertex()                                        | [Node]()                       | Gets the vertex that this component represents. Subclasses have getters that return more specific subclasses of Vertex.                                                                          |
| removeFromSelection()                              | void                           | Removes the vertex this component represents from the current selection in the model.                                                                                                            |
| removeNode()                                       | void                           | Shortcut method to remove the node (and therefore this whole component)                                                                                                                          |
| removePort(portId:string)                          | void                           | Removes the port with the given id.                                                                                                                                                              |
| removeVertex()                                     | void                           | Removes the vertex this component represents from the data model, which will cause this component to be cleaned up.                                                                              |
| setAsSelection()                                   | void                           | Sets the vertex this component represents as the current selection in the model.                                                                                                                 |
| updateNode(data:[ObjectData]())                    | void                           | Shortcut method to update the current data backing this node, for convenience.                                                                                                                   |
| updateVertex(data:[ObjectData]())                  | void                           | Shortcut method to update the current data backing this vertex, for convenience.                                                                                                                 |
