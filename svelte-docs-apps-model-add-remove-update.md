# Adding, removing and updating data

There is a full API available for you to manage your data model programmatically. Broadly, the operations on the data model can be broken up into three main categories:

* [Adding model objects](#adding-model-objects)
* [Deleting model objects](#deleting)
* [Updating model objects](#updating)

There are also some additional operations available on groups - the addition/removal of child vertices.

Whenever an operation occurs on the model, VisuallyJs advises all of its attached renders to update themselves accordingly.

info

The methods discussed on this page are on the model - which is an instance of the class [BrowserUIReactModel](). To read about how to access the model, [see the model overview](/svelte/docs/apps/model/overview.md#accessing-the-model).

## Adding model objects[​](#adding-model-objects "Direct link to Adding model objects")

### Nodes[​](#nodes "Direct link to Nodes")

There are two ways to add a node, either directly via the `addNode` method, whose signature is:

```typescript
addNode(data: ObjectData, eventInfo?: any): Node

```

for example:

```javascript
model.addNode({id:"1", foo:"a value", type:"someType"})

```

or, if you have a [node factory](/svelte/docs/apps/model/overview.md#node-factory) setup on your instance, you can add a node by invoking the factory, via the `addFactoryNode` method, whose signature is:

```javascript
addFactoryNode(type: string, data?: ObjectData, continueCallback?: Function): void

```

Consider that you have a node factory that does a fetch to some endpoint, providing the type for the new node, and the endpoint responds with the data for your new node:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const modelOptions = {
  nodeFactory: (type, data, callback, evt, native) =>{
      fetch({type:'post', body:{type}}).then(v => callback(v))
  }
}
</script>

<SurfaceComponent {modelOptions}/>

```

You can invoke the factory in a few ways. Firstly you can invoke the factory without supplying any data of your own:

```javascript
model.addFactoryNode("someType");

```

It is possible to also provide some seed data for the new node, which will be passed in to the node factory as `data`:

```javascript
model.addFactoryNode("someType", { foo:"bar" });

```

And also you can provide a callback which will be run after the node factory has finished adding the new node:

```typescript
model.addFactoryNode("someType", { foo:"bar" }, (newNode:Node) => {
    // newNode is your new node.
});

```

### Groups[​](#groups "Direct link to Groups")

As with nodes, you can add a group directly using `addGroup`, whose signature is:

```typescript
addGroup(data: ObjectData, eventInfo?: any): Group

```

for example:

```javascript
model.addGroup({id:"1", foo:"a value", type:"someType"})

```

or you can setup a [group factory](/svelte/docs/apps/model/overview.md#group-factory) and use the `addFactoryGroup` method, whose signature is:

```typescript
addFactoryGroup(type: string, data?: ObjectData, continueCallback?: Function): void

```

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const modelOptions = {
  groupFactory: (type, data, callback, evt, native) {
      fetch({type:'post', body:{type}}).then(v => callback(v))
  }
}
</script>

<SurfaceComponent {modelOptions}/>

```

You can call `addFactoryGroup` just by supplying the desired type for your new group:

```javascript
model.addFactoryGroup("someType");

```

Or by supplying type and initial data:

```javascript
model.addFactoryGroup("someType", { foo:"bar" })

```

Or by supplying type, data and a callback:

```javascript
model.addFactoryGroup("someType", { foo:"bar" }, (newGroup:Group) => {
    // newGroup is your new group
});

```

### Ports[​](#ports "Direct link to Ports")

Ports reside on nodes or groups, and so to add a port you have to supply the vertex you wish to add the port to. To add a port directly to a node or group you use `addPort`:

```javascript
addPort(vertex: string | Node | Group, data: ObjectData): Port

```

So, for instance:

```javascript
const node = model.addNode({id:"one", type:"someType"})
const port = model.addPort(node, {id:"p1", type:"somePortType"})

```

The equivalent to the `addFactoryNode` and `addFactoryGroup` method for ports is:

```javascript
addNewPort(obj: string | Node | Group, type: string, portData?: ObjectData)

```

`addNewPort` will invoke VisuallyJs's [port factory](/svelte/docs/apps/model/overview.md#port-factory) and then call `addPort` with the port factory's result.

As an example, this is the port factory from an early version of our Schema Builder starter app, in which table columns are represented as ports on table nodes:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  const modelOptions = {
  portFactory: (node, type, data, callback) => {
      let column = {
          id:data.columnName,
          name:data.columnName[0].toUpperCase() + data.columnName.slice(1),  
          datatype:\varchar\",
          type:\"column\"
      };
  
      // handoff the new column.
      callback(column);   
  }"
}
</script>

<SurfaceComponent {modelOptions}/>

```

note

The `addPort` and `addNewPort` methods discussed here will add ports to model objects, but they will not necessarily update the underlying JSON dataset. It is important to be across the concepts discussed [regarding the synchronization of port data](/svelte/docs/apps/model/overview.md#extracting-and-synchronizing-port-data)

### Edges[​](#edges "Direct link to Edges")

You can add an edge programmatically to the dataset via the `addEdge` method, which takes an argument of type [AddEdgeOptions]():

```typescript

addEdge(params: AddEdgeOptions): Edge

```

Adding an edge is slightly different to adding vertices, in that the backing data for an edge should be provided in a `data` object inside the payload you pass to this method. With nodes, groups and ports the backing data is at the top level.

The `source` and `target` you pass to this method can be one of three things:

* an object of type `Vertex` (`Node`, `Group` or `Port`);
* the ID of some vertex, in the case of ports this being a fully qualified port id in dotted notation;
* a [PointXY](), defining a location on the canvas, for when you want to add an edge that is initially not connected to a source and/or target vertex.

Some examples:

Here we add an edge from some `Node` to a port which we specify by id. We also supply some data for the edge - in this case, a label. The resulting edge has an ID that the model assigns:

```javascript
const edge = model.addEdge({
    source:someNode, 
    target:"someOtherNode.somePortId", 
    data:{label:"My Edge Label"}
})

```

Here we add an edge between two vertices specified by id. We also supply some data for the edge - in this case, the edge's ID, and also a label:

```javascript
const edge = model.addEdge({
    source:"node1", 
    target:"node2", 
    data:{
        label:"Label",
        id:"edgeId"
    }
})

```

## Removing model objects[​](#removing-model-objects "Direct link to Removing model objects")

### Nodes[​](#nodes-1 "Direct link to Nodes")

Nodes can be removed with the `removeNode` method, whose signature is:

<!-- -->

```typescript
removeNode(node: string | Node):void

```

for example:

```javascript
model.removeNode("someNodeId")

```

### Groups[​](#groups-1 "Direct link to Groups")

Groups can be removed with the `removeGroup` method:

```typescript
removeGroup(group: string | Group, removeChildren?: boolean):void

```

Note the `removeChildren` option to this method. By default when you remove a group its child vertices are orphaned, or if the group is itself a child of some other groups its child vertices are added to the group's parent.

This will remove a group and leave its child vertices in the dataset:

```javascript
model.removeGroup("someNodeId")

```

This will remove a group and its child vertices (and if any of those child vertices is a group, its children will be removed etc):

```javascript
model.removeGroup("someNodeId", true)

```

### Ports[​](#ports-1 "Direct link to Ports")

Use the `removePort` method to remove a port from the dataset:

```typescript
removePort(vertexOrId: string | Node | Group | Port, portId?: string): boolean

```

This method can be called in a few ways.

#### With full port id[​](#with-full-port-id "Direct link to With full port id")

You can provide the full port id in dotted notation, from which VisuallyJs will resolve the node/group and the port:

```javascript
model.removePort("someNode.somePortId")

```

#### With a port object[​](#with-a-port-object "Direct link to With a port object")

You can provide a `Port` model object:

```javascript
const port = model.addPort(someNode, { id:"portId", foo:"foo"})

...

model.removePort(port)

```

#### With a node/group and port id[​](#with-a-nodegroup-and-port-id "Direct link to With a node/group and port id")

Lastly, you can provide the node/group that is the port's parent, and the port id:

```javascript
model.removePort(someNode, "portId")

```

note

We again refer you to the documentation [regarding the synchronization of port data](/svelte/docs/apps/model/overview.md#extracting-and-synchronizing-port-data). Removing ports using these methods will remove the ports from the model, but to ensure the data is removed from the dataset you will need to have configured the model to recognize where your port data is stored on your nodes/groups.

### Edges[​](#edges-1 "Direct link to Edges")

You can remove an edge via `removeEdge`, whose signature is:

```typescript
removeEdge(edge: string | Edge):void

```

Edges can be removed by supplying the edge ID (see the example above for how to set an edge id):

```javascript
model.removeEdge("edgeId")

```

or by supplying an `Edge` model object:

```javascript

const edge = model.addEdge({source:someNode, target:"someOtherNode.somePortId", data:{label:"My Edge Label"}})

...

model.removeEdge(edge)

```

***

## Updating model objects[​](#updating-model-objects "Direct link to Updating model objects")

### Nodes[​](#nodes-2 "Direct link to Nodes")

To update a node, use `updateNode` or `updateVertex`:

```typescript
updateNode(node: string | Node | ObjectData, updates?: ObjectData): void

updateVertex(vertex: string | Node | Group | Port | ObjectData, updates?: ObjectData): void

```

```javascript
model.updateNode("someNodeId", { foo:"new value"})

```

### Groups[​](#groups-2 "Direct link to Groups")

To update a group, use `updateGroup` (or `updateVertex` as shown above for Nodes)

```javascript
model.updateGroup("someNodeId", { foo:"new value"})

```

### Ports[​](#ports-2 "Direct link to Ports")

To update a port, use the `updatePort` method, whose signature is:

```typescript
updatePort(port: Port | string, updates?: ObjectData): void

```

You can call this method with either a full port id:

```javascript
model.updatePort("someNode.somePortId", {field:"updatedValue"})

```

or with a `Port` model object:

```javascript
const port = model.addPort(someNode, { id:"portId", field:"originalValue"})
model.updatePort(port, {field:"updatedValue"})

```

### Edges[​](#edges-2 "Direct link to Edges")

Edges can be updated with the `updateEdge` method, whose signature is:

```typescript
updateEdge(obj: Edge | string, updates?: ObjectData): void

```

As with `removeEdge`, the edge in question can be identified by its id or by an `Edge` object. Here we update our edge from before via its id with a new label:

```javascript
model.updateEdge("edgeId", {label:"New Label"})

```

***

tip

## Transactions[​](#transactions "Direct link to Transactions")

All of the methods discussed on this page are connected to the underlying [undo/redo stack](/svelte/docs/apps/model/undo-redo.md), and run inside a transaction.

Certain methods can cause a cascade of other operations on the data model:

* removal of a vertex causes the removal of all edges to that vertex and to any ports on the vertex
* removal of a group with `removeChildren:true` will cause the removal of any child vertices, and edges connected to them

Since each method runs inside a transaction, calling `undo()` on a model instance will result in the rollback of every operation executed on the data model in response to some specific method call. Calling `redo()` will result in the re-application of every operation executed by the original method call.

***

## Events[​](#events "Direct link to Events")

The various add, update and remove methods discussed on this page will each cause a corresponding event to be fired:

| Method        | Event                 | Payload                |
| ------------- | --------------------- | ---------------------- |
| `addNode`     | `EVENT_NODE_ADDED`    | [NodeAddedParams]()    |
| `updateNode`  | `EVENT_NODE_UPDATED`  | [NodeUpdatedParams]()  |
| `removeNode`  | `EVENT_NODE_REMOVED`  | [NodeRemovedParams]()  |
| `addGroup`    | `EVENT_GROUP_ADDED`   | [GroupAddedParams]()   |
| `updateGroup` | `EVENT_GROUP_UPDATED` | [GroupUpdatedParams]() |
| `removeGroup` | `EVENT_GROUP_REMOVED` | [GroupRemovedParams]() |
| `addPort`     | `EVENT_PORT_ADDED`    | [PortAddedParams]()    |
| `updatePort`  | `EVENT_PORT_UPDATED`  | [PortUpdatedParams]()  |
| `removePort`  | `EVENT_PORT_REMOVED`  | [PortRemovedParams]()  |
