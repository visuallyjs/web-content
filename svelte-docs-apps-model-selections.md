# Selections

A `Selection` is a collection of nodes, groups, ports and edges (zero or more of each), upon which operations can be made that affect the entire set at once.

You can work with these in one of two ways - either use the model's [current selection](#currentSelection), or [create an ad-hoc selection](#adhoc-selection).

## Current selection[​](#current-selection "Direct link to Current selection")

Each instance of the VisuallyJs model maintains a `currentSelection` - the currently selected set of objects. Several methods are available for you to manipulate the contents of the current selection. Changes to the selection are propagated to all registered UI components for some model, which take appropriate action as they need to.

Some examples of the current selection in use in the UI are:

* the Surface and Paper components will assign a CSS class to any object that is in the current selection;
* an Inspector will extract data from the object(s) in the current selection and allow users to edit the values;
* the [ResizingToolsPlugin](/svelte/docs/apps/plugins/resizing-tools.md) will attach resize (and possibly rotate) controls to objects in the current selection;
* the [LassoPlugin](/svelte/docs/apps/plugins/lasso.md) adds snagged vertices to the current selection

### setSelection(obj)[​](#setselectionobj "Direct link to setSelection(obj)")

Set the current selection. Here, `obj` can take a number of forms:

* A node, group, port or edge object
* A list of nodes/groups/ports/edges
* Another `Selection`
* A `Path`

### addToSelection(obj)[​](#addtoselectionobj "Direct link to addToSelection(obj)")

Add something to the current selection. Here, `obj` can take a number of forms:

* A node, group, port or edge object
* A list of nodes/groups/ports/edges
* Another selection
* A path

### addPathToSelection(params)[​](#addpathtoselectionparams "Direct link to addPathToSelection(params)")

A helper method to get a path (see [the Paths docs](/svelte/docs/apps/model/paths.md)) and add it to the current selection.

### removeFromSelection(obj)[​](#removefromselectionobj "Direct link to removeFromSelection(obj)")

Remove something from the current selection. Valid values for `obj` are the same as for the `addToSelection` and `setSelection` methods.

### getSelection()[​](#getselection "Direct link to getSelection()")

Get the current selection. This returns a [Selection](), which is a selector-like object that offers a number of methods for performing operations on the selection as a whole.

### clearSelection()[​](#clearselection "Direct link to clearSelection()")

Clears the current selection. This method is analogous to calling `getSelection().clear()`.

***

## AdHoc selections[​](#adhoc-selections "Direct link to AdHoc selections")

In addition to the current selection, you can also select a set of vertices and/or edges on an adhoc basis:

* **select(obj)**

Here, `obj` can be some node/group/port/edge, or the ID of some node, group or port, or an array of a combination of these.

For example, here we create an adhoc selection consisting of 3 nodes, which we nominated by their IDs:

```typescript
const mySelection = model.select(["1", "2", "7"])

```

***

### Filtering objects[​](#filtering-objects "Direct link to Filtering objects")

A more powerful method to use to get a set of objects is `filter`, which, as the name suggests, can filter the contents of some model instance according to a few criteria. There are two ways to call this method.

#### Filtering with a function[​](#filtering-with-a-function "Direct link to Filtering with a function")

You can pass a Function as argument to the `filter` method, which is expected to return true to indicate that a given object should be included:

```javascript
import { Node } from "@visuallyjs/browser-ui"

let selection = model.filter((obj) => {
    return (obj.objectType === Node.objectType) 
})

```

Note here that this function is given *every* object managed by VisuallyJs - meaning all groups, nodes and edges. So you can use `objectType` to test if the object is a node or an edge. In this simple example we have simply returned all the nodes in the model.

Another example of using a function:

```javascript
import { Node } from "@visuallyjs/browser-ui"

let selection = model.filter((obj) => {
    return obj.objType === Node.objectType && obj.data.maxValue < 150
});

```

Here we return only nodes whose `maxValue` is less than 150.

#### Filtering with a match object[​](#filtering-with-a-match-object "Direct link to Filtering with a match object")

Alternatively, you can pass a match object in to the `filter` method:

```javascript
let selection = model.filter({
  maxValue:150
});

```

Here we've told VisuallyJs we are interested only in vertices whose `maxValue` is exactly 150. Note that with a match object only exact matches are supported: we cannot recreate the previous example in which vertices whose `maxValue` was less than 150 are returned.

You can match an arbitrary number of values:

```javascript
let selection = model.filter({
  maxValue:150,
  lorem:"ipsum"
});

```

Here we get vertices with a `maxValue` of 150 and a `lorem` of "ipsum".

#### Partial matches with a match object[​](#partial-matches-with-a-match-object "Direct link to Partial matches with a match object")

You can instruct VisuallyJs that an object that matches at least one entry in the match object should be included in the output (by default, every value must match):

```javascript
let selection = model.filter({
  maxValue:150,
  lorem:"ipsum"
}, true)

```

...by passing in `true` as the second argument to the `filter` function. So in this example we now get vertices that have a `maxValue` of 150 and/or a `lorem` of "ipsum".

***

### Selection mode[​](#selection-mode "Direct link to Selection mode")

This concept allows you to control what can be added to the selection by its type - it's basically a higher level version of the `filter` we just discussed.

There are 5 modes supported by a selection, of which the default is `mixed`:

* **SelectionModes.mixed** Any combination of nodes, edges and groups is supported
* **SelectionModes.isolated** Only a set of nodes/groups, OR a set of edges, but not a mix. Conceptually this means the selection works in a "vertices only" or "edges only" mode, where the selection object decides which of these is appropriate when a new addition is made. For instance, if you have a selection in isolated mode that already has one node, then no new edges may be added. If you subsequently remove that node, making the selection empty, you could then add an edge.
* **SelectionModes.nodesOnly** Only nodes. No groups or edges.
* **SelectionModes.groupsOnly** Only groups. No nodes or edges.
* **SelectionModes.edgesOnly** Only nodes. No groups or nodes.

The mode for a selection can be set in its constructor:

```javascript
const sel = new Selection(modelInstance, {
    mode: SelectionModes.edgesOnly
})

```

or it can be set on an existing selection object:

```javascript
mySelection.setMode(SelectionModes.isolated)

```

If you want to change the mode for the current selection of some model instance, you can do that programmatically:

```javascript
model.getSelection().setMode(SelectionModes.mixed)

```

***

## Selecting Descendants[​](#selecting-descendants "Direct link to Selecting Descendants")

If you are working with hierarchical data, you can use VisuallyJs to get a list of descendants of some vertex (and, optionally, the edges to and from each vertex):

```javascript
const descendants = model.selectDescendants(someVertex)

```

The return value is a [Selection](), with all of the methods discussed above available. By default this selection does not include the focus node or any edges, but there are a number of options you can provide to modify the behaviour:

#### selectDescendants[​](#selectdescendants "Direct link to selectDescendants")

Selects all descendants of some Node or Group, and, optionally, the Node/Group itself.

Signature

selectDescendants(obj:string | [Node]() | [Group](), includeFocus:boolean, includeEdges:boolean)

Parameters

|              |                                 |                                                                                            |
| ------------ | ------------------------------- | ------------------------------------------------------------------------------------------ |
| obj          | string \| [Node]() \| [Group]() | Node/Group, or ID of Node/Group, to select                                                 |
| includeFocus | boolean                         | Whether or not to include the focus node/group in the returned dataset. Defaults to false. |
| includeEdges | boolean                         | Whether or not to include edges in the returned dataset. Defaults to false.                |

Return value

[VisuallyJsSelection]()

So this call would return all of a vertex's descendants plus the vertex itself:

```javascript
var descendants = model.selectDescendants(someNode, true);

```

And this would get the descendants, the node itself, and any edges connecting the nodes in the set:

```javascript
var descendants = model.selectDescendants(someNode, true, true);

```

***

## Removing everything in a selection[​](#removing-everything-in-a-selection "Direct link to Removing everything in a selection")

This is a fairly common use case when working with a selection:

```javascript
let selection = model.selectDescendants(someNode)
model.remove(selection)

```

Here we used the `selectDescendants` method, but we could have used any method that returns a selection or path - `select`, `selectDescendants`, `filter` or `getPath`.

***

## Appending to selections[​](#appending-to-selections "Direct link to Appending to selections")

You can append individual objects, other selections and also paths to a selection:

```javascript
// get a selection containing nodes 1, 2 and 3
let selection1 = model.select(["1", "2", "3"]);

// get a path from node 1 to node 17
let path = model.getPath({source:"1", target:"17"});

// append the path
selection1.append(path);

// append node 34
selection1.append("34")

// get another selection
let selection2 = model.select(["36", "25"]);

// append it
selection1.append(selection2)


```

***

## Limiting selection size[​](#limiting-selection-size "Direct link to Limiting selection size")

You can limit the number of group, nodes and/or edges in a selection or model's `currentSelection`. This can be useful in a few ways: maybe your app wants to enforce that only one node is selected at any point in time, for instance. Or maybe you want to maintain a selection queue of fixed size for some purpose.

#### Limiting the model's current selection[​](#limiting-the-models-current-selection "Direct link to Limiting the model's current selection")

You can provide constructor parameters to control this behaviour:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { Selection } from "@visuallyjs/browser-ui"
  const modelOptions = {
  maxSelectedNodes: 1,
  maxSelectedGroups: 1,
  maxSelectedEdges: 1,
  selectionCapacityPolicy: "discardNew"
}
</script>

<SurfaceComponent {modelOptions}/>

```

Here we have specified that at most 1 node, 1 group and 1 edge may be selected, and that when the user tries to add a new node or edge to the current selection, it should be discarded. The other option - the default option - for `selectionCapacityPolicy` is `Selection.DISCARD_EXISTING`, which takes the 0th element from the underlying list.

You can also control these values with setter methods:

```javascript
tk.setMaxSelectedNodes(4)
tk.setMaxSelectedGroups(3)
tk.setMaxSelectedEdges(3)
tk.setSelectionCapacityPolicy(Selection.DISCARD_EXISTING)

```

### Limiting an AdHoc selection[​](#limiting-an-adhoc-selection "Direct link to Limiting an AdHoc selection")

To set limits and control the capacity policy of an ad-hoc selection, these methods are available:

```javascript
var sel = model.select() // create an empty selection
sel.setMaxNodes(4)
sel.setMaxEdges(3)
sel.setCapacityPolicy(Selection.DISCARD_EXISTING);

```
