# Data model

The core data model in VisuallyJs is that of a graph, as discussed [here on Wikipedia](https://en.wikipedia.org/wiki/Graph_\(discrete_mathematics\)).

A graph is a collection of nodes, groups, edges and ports.

* **Nodes** map to entities in your data model.
* **Groups** are collections of nodes/groups. They map to entities in your data model.
* **Ports** are logical and/or physical locations on nodes/groups that are the terminus for an edge. Not all apps use ports in their data model. The simplest example of the usage of ports is perhaps a database schema: you'd represent your tables as nodes, and then the columns on each table would be represented as ports. Another good analogy is ports in TCP/IP.
* **Edges** are relationships between nodes, groups or ports.

tip

In the VisuallyJs documentation you'll see references to `Vertex` and `vertices` - this is a node, port or group. We often use "vertex" to refer to the source and target terminus for an edge throughout the documentation as it's easier than typing "Node/Group/Port"...and also, conceptually, its correct!

## What do I need the model for?[​](#what-do-i-need-the-model-for "Direct link to What do I need the model for?")

A brief list of the sorts of things you can do with the model:

* add/remove/update nodes, groups and edges
* undo/redo operations
* impose constraints on connectivity between objects
* specify object factories for the creation of new objects
* import/export the dataset
* execute multiple operations within a transaction
* select specific contents via filtering
* check for the existence of and retrieve paths between vertices

Changes to the model are automatically reflected in the UI.

## Accessing the model[​](#accessing-the-model "Direct link to Accessing the model")

You'll need to access the model from inside your code in order to use the programmatic model API. Expand the section below for instructions on how to do that.

How to access the model

### From your app component[​](#from-your-app-component "Direct link to From your app component")

To access the model from inside a component that uses a `SurfaceComponent`, declare a `ref` of type [SurfaceComponent]() and assign it in the template.

You can then access the model through the ref's value, which is of type [SurfaceComponent]()

```html
<script setup lang="ts">
import { ref } from "vue"
import { SurfaceComponent} from "@visuallyjs/browser-ui-vue"

const surfaceRef = ref<SurfaceComponent>(null)
    
function addANode() {
    surfaceRef.value.surface.model.addNode({id:"1", left:50, top:50})
}
</script>
<template>
  <SurfaceComponent ref={surfaceRef}/>
  <button onClick={() => addANode()}>Add a node!</button>
</template>

```

### From a different component[​](#from-a-different-component "Direct link to From a different component")

If you have a component somewhere in your tree from which you wish to interact with the model, you can use the `useSurface()` hook in conjunction with a `SurfaceProvider` to access the surface. Your app component should look something like this:

```html
<script setup lang="ts">
</script>
<template>
  <SurfaceProvider>
    <SurfaceComponent/>
    <MyOtherComponent/>
  </SurfaceProvider>
</template>

```

Then the implementation of `MyOtherComponent` can use the `useSurface` hook:

```html
<script setup lang="ts">

  import { useSurface } from "@visuallyjs/browser-ui-vue"
  import { Surface } from "@visuallyjs/browser-ui"
    
  const surface:Surface = useSurface() // this is reactive state

  function addANode() {
    surface.model.addNode({id:"1", left:50, top:50})
  }
    
</script>
<template>
  <div><button onClick={() => addANode()}>Add a node!</button></div>
</template>

```

## Data Format[​](#data-format "Direct link to Data Format")

The various parts of your data model can be represented as any valid Javascript type. As an example, here is the backing data for the `Book` table in the Schema Builder starter app:

```json
{
  "id":"book",
  "name":"Book",
  "type":"table",
  "columns":[
    { "id":"123", "name":"id", "datatype":"integer", "primaryKey":true },
    { "id":"456", "name":"isbn", "datatype":"varchar" },
    { "id":"789", "name":"title", "datatype":"varchar" }
  ]
}

```

## Object IDs[​](#object-ids "Direct link to Object IDs")

Every vertex is required to have a unique ID. VisuallyJs attempts to derive this automatically from your data, by looking for an `id` member, which should be a **string**.

tip

For the vast majority of applications this setup will work fine. Should you wish to implement a different strategy, though, you can supply your own `idFunction` in your model options:

```html
<script setup>

import { ObjectData } from "@visuallyjs/browser-ui"

function modelOptions() {
  return {
  idFunction: (data:ObjectData):string {
    return SomeCustomComputing(data);
  }
})
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

Remember to pass back the ID as a string. This method will be used to attempt to derive an ID for any model object.

Again note this is optional - you do not need to supply this function, but if you do not then VisuallyJs will expect an `id` member in your data.

### Group IDs[​](#group-ids "Direct link to Group IDs")

IDs for groups are derived using whatever method VisuallyJs is using to derive IDs for nodes - either by looking for an `id` value in your data, or by using a supplied `idFunction`. group IDs must be unique across all groups *and nodes* in the dataset: you cannot have a group that has the same ID as some node.

### Edge IDs[​](#edge-ids "Direct link to Edge IDs")

You are not required to supply an ID for every edge, and if you do not, VisuallyJs will assign one automatically.

### Port IDs[​](#port-ids "Direct link to Port IDs")

Port IDs are required to be unique on the node/group on which the port exists, but may be the same as the ID of a port on some other node (and in fact this is quite common).

#### Referencing ports by ID[​](#referencing-ports-by-id "Direct link to Referencing ports by ID")

When adding an edge to a VisuallyJs instance, you can reference a port on some node using, by default, dotted notation. In the data given above there were three ports. We could connect one of them to a column on another table like this:

```javascript
model.connect({
  source:"book.id", 
  target:"book_author.book_id"
})

```

`book_author` is another table in the schema from the SchemaBuilderDemoLink title="Schema Builder"/> starter app.

#### Custom port ID Separator[​](#custom-port-id-separator "Direct link to Custom port ID Separator")

If you find that using a period as the separator in a port ID does not work for your data model, you can override what VisuallyJs will use by doing this:

```html
<script setup>

function modelOptions() {
  return {
  portSeparator: "#"
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

## Object type[​](#object-type "Direct link to Object type")

Every object has an associated `type`. This is an important concept in VisuallyJs, as it is the basic means by which the data model is bound to any renderers, via views.

The `type` of a model object is, by default, mapped by the object's `type` in its backing data. It is used by the view in the UI to determine the appearance and behaviour of the object.

To change the type of some object after it has been initially created, use the `setType` method on a model instance. For a discussion, see [this page](/vue/docs/apps/model/add-remove-update.md#setting-object-types)

tip

As with ID, you can provide your own function to retrieve the type for some object, should you need to.

```html
<script setup>

import { ObjectData } from "@visuallyjs/browser-ui"

function modelOptions() {
  return {
  typeFunction: (data:ObjectData):string => {
  return SomeOtherComputing(data);
}
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

## Constraining connectivity[​](#constraining-connectivity "Direct link to Constraining connectivity")

Connectivity can be controlled at runtime by **interceptors** - callbacks that can be used to cancel some proposed activity, and that are bound on an instance of the VisuallyJs model by supplying a specific function in the model constructor options.

#### beforeConnect[​](#beforeconnect "Direct link to beforeConnect")

A function to run before an edge with the given data can be established between the given source and target. Returning false from this method aborts the connection. Note that this method fires regardless of the source of the new edge, meaning it will be called when loading data programmatically.

##### Method signature[​](#method-signature "Direct link to Method signature")

`beforeConnect(source: Vertex, target: Vertex): any`

##### Parameters[​](#parameters "Direct link to Parameters")

* *source* The source vertex for the new edge
* *target* The target vertex for the new edge

##### Return value[​](#return-value "Direct link to Return value")

* `false` - aborts the connection
* all other values are ignored and will allow the edge to be established

##### Example[​](#example "Direct link to Example")

Here, we reject connections from any vertex to itself.

```html
<script setup>

function modelOptions() {
  return {
  beforeConnect: (source: Vertex, target: Vertex) => {
      return (source !== target)
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

#### beforeMoveConnection[​](#beforemoveconnection "Direct link to beforeMoveConnection")

A function to run before an edge of the given type is relocated from its current source or target to a new source or target. Returning false from this method will abort the move.

##### Method signature[​](#method-signature-1 "Direct link to Method signature")

`beforeMoveConnection(source: Vertex, target: Vertex, edge: Edge): any`

##### Parameters[​](#parameters-1 "Direct link to Parameters")

* *source* Candidate source. May be the edge's current source, or may be a new source.
* *target* Candidate target. May be the edge's current target, or may be a new target.
* *edge* The edge that is being moved.

The parameters `source` and `target` reflect the source and target of the edge if the move were to be accepted. So if, for example, your user drags a connection by its target and drops it elsewhere, `target` will be the drop target, not the edge's current target, but `source` will be the edge's current source. You can access the current source/target via the `source` and `target` properties of `edge`.

##### Return value[​](#return-value-1 "Direct link to Return value")

* `false` - aborts the move
* all other values are ignored and will allow the move to occur

##### Example[​](#example-1 "Direct link to Example")

Here, we reject moving any edge that has `fixed:true` in it backing data:

```html
<script setup>

function modelOptions() {
  return {
  beforeMoveConnection: (source: Vertex, target: Vertex, edge:Edge) => {
      return (edge.data.fixed !== true)
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

#### beforeStartConnect[​](#beforestartconnect "Direct link to beforeStartConnect")

A function to run before an edge of the given type is dragged from the given source (ie. before the mouse starts moving). This interceptor is slightly different to the others in that it's not just a yes/no question: as with the other interceptors, returning false from this method will reject the action, that is in this case it will not allow a connection drag to begin. But you can also return an object from this method, and when you do that, the connection start is allowed, and the object you returned becomes the payload for the new edge.

##### Method signature[​](#method-signature-2 "Direct link to Method signature")

`beforeStartConnect(source: Vertex, type: string): any`

##### Parameters[​](#parameters-2 "Direct link to Parameters")

* *source* The vertex that is the source for the new edge
* *type* The computed type for this new edge.

##### Return value[​](#return-value-2 "Direct link to Return value")

* `false` - aborts the connection
* `Object` - An object returned from this method will be used as the initial payload for the new edge
* all other values are ignored and will allow the connection start to continue

##### Example - reject a connection start[​](#example---reject-a-connection-start "Direct link to Example - reject a connection start")

```html
<script setup>

function modelOptions() {
  return {
  beforeStartConnect: (source: Vertex, type:string) => {
      return type !== 'not-connectable'
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

##### Example - provide an initial payload[​](#example---provide-an-initial-payload "Direct link to Example - provide an initial payload")

```html
<script setup>

function modelOptions() {
  return {
  beforeStartConnect: (source: Vertex, type:string) => {
      return {
          type,
          message:`initial payload for vertex ${source.id}`
      }
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

#### beforeDetach[​](#beforedetach "Direct link to beforeDetach")

A function to run before the given edge is detached from the given source vertex. If this method returns false, the detach will be aborted.

##### Method signature[​](#method-signature-3 "Direct link to Method signature")

`beforeDetach(source: Vertex, target: Vertex, edge: Edge, isDiscard?: boolean): any`

##### Parameters[​](#parameters-3 "Direct link to Parameters")

* *source* The source vertex for the edge that is to be detached.
* *target* The candidate target for the edge - may be null, if the edge is being discarded
* *edge* The edge that is being detached.
* *isDiscard* True if the edge is not now connected to a target.

##### Return value[​](#return-value-3 "Direct link to Return value")

* `false` Returning false will abort the edge detach
* all other values are ignored and will allow the detach to occur

##### Example[​](#example-2 "Direct link to Example")

Here, we reject the detach if the target is null, ie. the user is trying to discard the edge, not relocate it.

```html
<script setup>

function modelOptions() {
  return {
  beforeDetach: (source: Vertex, target: Vertex, edge: Edge, isDiscard?: boolean) => {
      return target != null
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

#### beforeStartDetach[​](#beforestartdetach "Direct link to beforeStartDetach")

##### Method signature[​](#method-signature-4 "Direct link to Method signature")

`beforeStartDetach(source: Vertex, edge: Edge): any`

A function to run before the given edge is detached from the given source vertex. If this method returns false, the detach will be aborted. The difference between this and `beforeDetach` is that this method is fired as soon as a user tries to detach an edge from an anchor in the UI, whereas `beforeDetach` allows a user to detach the edge in the UI.

##### Parameters[​](#parameters-4 "Direct link to Parameters")

* *source* The source vertex for the edge that the user has started to detach
* *edge* The edge that the user has started to detach

##### Return value[​](#return-value-4 "Direct link to Return value")

* `false` Returning false will abort the edge detach
* all other values are ignored and will allow the user to begin the detach

##### Example[​](#example-3 "Direct link to Example")

Here, we reject the detach if the source vertex has `doNotDetachEdges:true` in its backing data.

```html
<script setup>

function modelOptions() {
  return {
  beforeDetach: (source: Vertex, edge: Edge) => {
      return source.data.doNotDetachEdges !== true
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

##### Multiple interceptors[​](#multiple-interceptors "Direct link to Multiple interceptors")

You can provide multiple interceptors - in this example we provide a `beforeStartConnect` and `beforeDetach` interceptor to the model. The `beforeStartConnect` interceptor prevents the user from dragging connections from any vertex whose ID is not an even number. The `beforeDetach` interceptor reattaches detached connections whose source ID is not an event number

```html
<script setup>

function modelOptions() {
  return {
  beforeStartConnect: (source, type) => {
      // only allow connections from nodes whose 
      // ID is an even number
      return parseInt(source.id, 10) % 2 === 0
  },
  beforeDetach: (source, target, edge, isDiscard) => {
      // only allow connections to be detached whose 
      // source ID is an even number
      return parseInt(edge.source.id, 10) % 2 === 0
  }
}
    }

</script>
<template>
  <SurfaceComponent :viewOptions="modelOptions()" />
</template>

```

**********

## Next Steps[​](#next-steps "Direct link to Next Steps")

[Add, remove and update](/vue/apps/model/add-remove-update)

[Read about how to add, remove and update data](/vue/apps/model/add-remove-update)

[Undo/redo and transactions](/vue/apps/model/undo-redo)

[Read about how to undo/redo operations, and work with transactions](/vue/apps/model/undo-redo)

[Selections](/vue/apps/model/selections)

[Read about how to generate and work with selections](/vue/apps/model/selections)
