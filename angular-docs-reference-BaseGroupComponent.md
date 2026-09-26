# BaseGroupComponent

This component is what you must extend in any components you create to render groups. It injects the underlying [VisuallyJsService](/angular/docs/reference/VisuallyJsService.md), and also provides a number of helper methods you can use to manipulate the model object that your component represents.

The vertex this component represents is available on the class as `data` (a plain JS object), and `$data()` (a signal wrapping `data`).

## Usage[​](#usage "Direct link to Usage")

```typescript
import { Component } from "@angular/core"
import { BaseGroupComponent } from "@visuallyjs/browser-ui-angular"

@Component({
   template:`<div>
  <strong>{{data.label}}</strong>
  <div data-vjs-group-content="true"></div>
</div>` 
})
export class MyGroupComponent extends BaseGroupComponent { }  

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
| cloneGroup(options:[SurfaceVertexCloneOptions]())  | void                           | Instructs the model to clone this group - which will result in a new group being added to the UI, whose position will be shifted slightly in X and Y from the cloned group.                      |
| cloneVertex(options:[SurfaceVertexCloneOptions]()) | void                           | Clones this vertex, optionally setting to a given position, or offsetting from the original, and optionally magnetizing the new vertex's position, and flashing it to show the user where it is. |
| flashGroup(duration:number, animName:string)       | void                           | Flash this Group                                                                                                                                                                                 |
| getGroup()                                         | [Group]()                      | Gets the group that this component represents.                                                                                                                                                   |
| getMembers()                                       | Array<[Node]()>                | Gets the child vertices for this group. Group members may be of type Node or Group.                                                                                                              |
| getPort(portId:string)                             | [Port]()                       | Gets the port with the given ID                                                                                                                                                                  |
| getVertex()                                        | [Group]()                      | Gets the vertex that this component represents. Subclasses have getters that return more specific subclasses of Vertex.                                                                          |
| removeFromSelection()                              | void                           | Removes the vertex this component represents from the current selection in the model.                                                                                                            |
| removeGroup()                                      | void                           | Shortcut method to remove the Group (and therefore this whole component)                                                                                                                         |
| removePort(portId:string)                          | void                           | Removes the port with the given id.                                                                                                                                                              |
| removeVertex()                                     | void                           | Removes the vertex this component represents from the data model, which will cause this component to be cleaned up.                                                                              |
| setAsSelection()                                   | void                           | Sets the vertex this component represents as the current selection in the model.                                                                                                                 |
| updateGroup(data:[ObjectData]())                   | void                           | Shortcut method to update the current data backing this Group, for convenience.                                                                                                                  |
| updateVertex(data:[ObjectData]())                  | void                           | Shortcut method to update the current data backing this vertex, for convenience.                                                                                                                 |
