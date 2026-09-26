# Dragging edges

You can setup your app for edge dragging by specifying some part of each vertex's DOM element to act as a connection source and/or target, via a set of `data-vjs-` attributes. VisuallyJs offers very fine-grained control over this setup, and assigns a [variety of CSS classes](#css-classes) during the edge drag lifecycle, to assist you in providing the best experience for your users.

## Configuring Connectivity[​](#configuring-connectivity "Direct link to Configuring Connectivity")

### Source and target attributes[​](#source-and-target-attributes "Direct link to Source and target attributes")

You can specify parts of your UI that should act as connection sources and/or targets using a set of `data-vjs-` attributes inside your vertex components/template:

```html
<div data-vjs-source="true" data-vjs-target="true"></div>

```

This is the most basic setup: a div element that is declared to be both a source and target of connections established by dragging with the mouse. Note, though, that the surface widget will automatically exclude any elements with a `data-vjs-source` attribute from being able to instigate dragging, since once an element can act as a connection source it is not possible to also support element dragging: the user's intent would be ambiguous.

In this canvas, you can drag edges from each node to each other node - but note the nodes themselves are not draggable, because the entire node is declared as a connection source:

**********

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [viewOptions]="viewOptions"></vjs-surface> `
})
export class AppComponent {
  viewOptions = {
  nodes: {
    default: {
      jsx: (ctx) => <div data-vjs-source='true' data-vjs-target='true'/>
    }
  }
};
}

```

So, a more plausible real world scenario would be some element in which only part of it could act as a connection source:

```html
<div data-vjs-target="true">
    <h1>Some Vertex</h1>
    <div data-vjs-source="true" class="dragFromHere"></div>
</div>

```

In this canvas the red circles are our `data-vjs-source` elements - you can drag edges from them, and you can drag each node around. But you cannot drag the nodes around by their red circles:

**********

Note that we still put the `data-vjs-target` attribute on the root element since there is no ambiguity - when the element is behaving as a connection target it is not going to be the element that is currently being dragged.

### Mapping ports to elements[​](#mapping-ports-to-elements "Direct link to Mapping ports to elements")

Ports on a vertex have an ID, which must be unique across the ports on that vertex, and which can be addressed. We use ports in the data model of several of our applications - for instance, in the Schema Builder starter app, we have a `table` node type, which has a set of columns. Each column in a table is mapped to a specific port id. This allows us to define edges between columns on two tables, for instance we may have an edge from `book.book_author_id` to `author.author_id`; here `book` and `author` are table IDs, and `book_author_id` and `author_id` are port IDs.

VisuallyJs offers two attributes to assist in mapping ports from your model into your UI.

#### Physical ports[​](#physical-ports "Direct link to Physical ports")

You can map port IDs to DOM elements - what we refer to as **physical** ports - via the `data-vjs-port` attribute.

Here, we have two nodes that each contain a list of columns, and each column has an `id`, for instance:

```javascript
{ 
    id:"1", 
    left:50, 
    top:50, 
    columns:[
     {id:"one", scope:"cadetblue"}, 
     {id:"two", scope:"darkseagreen"}, 
     {id:"three", scope:"cadetblue" }
    ] 
}

```

We render each node this this template:

```html
<div style="display:flex;flex-direction:column;>
  @for(column of obj.columns;track column) {
    <div [data-vjs-scope]="column.scope" 
           style="background-color:{{column.scope}}" 
           data-vjs-source="true" 
           data-vjs-target="true" 
           [data-vjs-port]="column.id">{{column.id}}</div>
  }    
</div>

```

Each of our column elements declares `data-vjs-source` and `data-vjs-target` to be true, meaning the element is both a source and target for edges dragged with the mouse. But the key piece is the `data-vjs-port` attribute: it indicates to VisuallyJs that that element is the *physical* representation of the given port on that vertex. Any edges connected to the port with that ID on the vertex will be connected to that DOM element.

In the dataset for the canvas below we have two edges:

```javascript
[
    { "source":"1.three", "target":"2.two" },
    { "source":"1.two", "target":"2.five" }
]

```

These edges are from a port on some vertex to a port on some other vertex, and it is the `data-vjs-port` attribute in our template that helps VisuallyJs figure out which DOM elements to connect.

**********

We call this a **physical** port mapping: for some port ID, there is a specific DOM element mapped to it.

#### Logical ports[​](#logical-ports "Direct link to Logical ports")

What we call **logical** ports are slightly different - with this setup, there is no specific DOM element mapped to a given port, and edges connected to a logical port are shown in the UI as being connected to the port's vertex.

caution

If you wish to use logical ports, you need to tell VisuallyJs in the render options. VisuallyJs assumes, by default, that you're not using logical ports.

Here, we have two nodes that each contain a list of columns, and each column has an `id`, for instance:

```javascript
{ 
    id:"1", 
    left:50, 
    top:50, 
    columns:[
     {id:"one", scope:"cadetblue"}, 
     {id:"two", scope:"darkseagreen"}, 
     {id:"three", scope:"cadetblue" }
    ] 
}

```

We render each node this way:

```html

<div style="display:flex;flex-direction:column;>
@for(column of obj.columns;track column) {
  <div [data-vjs-scope]="column.scope" 
         style="background-color:{{column.scope}}" 
         data-vjs-source="true" 
         data-vjs-target="true" 
         [data-vjs-port-id]="column.id">{{column.id}}</div>
}    
</div>

```

In this example the key piece is the `data-vjs-port-id` attribute: it indicates to VisuallyJs that that element is the *logical* representation of the given port on that vertex, meaning that any edges dragged from that element will be assigned a source port ID corresponding to the `data-vjs-port-id` attribute's value, but the actual DOM element used for the edge will be the vertex's DOM element.

In the dataset for the canvas below we have two edges:

```javascript
[
    { "source":"1.three", "target":"2.two" },
    { "source":"1.two", "target":"2.five" }
]

```

These edges are from a port on some vertex to a port on some other vertex, and it is the `data-vjs-port-id` attribute in our template that helps VisuallyJs figure out which DOM elements to connect.

**********

We call this a **logical** port mapping: for some port ID, there is no specific DOM element mapped to it; VisuallyJs uses the DOM element for the port's vertex.

***

### Specifying anchors[​](#specifying-anchors "Direct link to Specifying anchors")

Since:

<!-- -->

1.2.5

Anchors define the position on some element at which one end of an edge is located. There are several different types of anchors available (a full discussion of which can be found [here](/angular/docs/apps/edges/anchors.md)), and there are a few different ways to configure what anchors will be used by some edge - setting them for the whole UI, for example, or mapping to a specific edge type.

In this section we'll discuss a more granular approach to declaring anchors, by writing out the anchors you want directly in your templates, via `data-vjs-anchor`, `data-vjs-source-anchor` or `data-vjs-target-anchor` attributes. For example, in this canvas, each node tells you what anchor will be used when you drag an edge from the red circle. In the code below the canvas, look for the `data-vjs-anchor` attribute - it tells VisuallyJs what the anchor should be.

**********

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [viewOptions]="viewOptions"></vjs-surface> `
})
export class AppComponent {
  viewOptions = {
  nodes: {
    default: {
      jsx: (ctx) => <div data-vjs-target='true'><div data-vjs-source='true'/>ANY ANCHOR</div>
    },
    right: {
      jsx: "(ctx) => <div data-vjs-target='true'><div data-vjs-anchor='Right' data-vjs-source='true'/>RIGHT SOURCE ANCHOR</div>"
    },
    left: {
      jsx: (ctx) => <div data-vjs-target='true'><div data-vjs-anchor='Left' data-vjs-source='true'/>LEFT SOURCE ANCHOR</div>
    }
  }
};
}

```

#### Source vs Target[​](#source-vs-target "Direct link to Source vs Target")

In the above example we specified the anchor we wanted to use for the source, but not for the target - because the `data-vjs-source` element is a different element to `data-vjs-target`. We can update that code to also include a `data-vjs-anchor` attribute on the targets (we'll set them all to 'Top'):

**********

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [viewOptions]="viewOptions"></vjs-surface> `
})
export class AppComponent {
  viewOptions = {
  nodes: {
    default: {
      jsx: (ctx) => <div data-vjs-target='true' data-vjs-anchor='Top'><div data-vjs-source='true'/>ANY ANCHOR</div>
    },
    right: {
      jsx: "(ctx) => <div data-vjs-target='true' data-vjs-anchor='Top'><div data-vjs-anchor='Right' data-vjs-source='true'/>RIGHT SOURCE ANCHOR</div>"
    },
    left: {
      jsx: (ctx) => <div data-vjs-target='true' data-vjs-anchor='Top'><div data-vjs-anchor='Left' data-vjs-source='true'/>LEFT SOURCE ANCHOR</div>
    }
  }
};
}

```

#### Anchor syntax[​](#anchor-syntax "Direct link to Anchor syntax")

Anchors in VisuallyJs all boil down to 4 essential pieces of information:

* `x` Where, as a proportion of width, the anchor is located on the x-axis
* `y` Where, as a proportion of height, the anchor is located on the y-axis
* `ox` In which x direction should a connection naturally travel from this anchor. Valid values are 1 (to the right), 0 (dont care) or -1 (to the left)
* `oy` In which y direction should a connection naturally travel from this anchor. Valid values are 1 (downwards), 0 (dont care) or -1 (upwards)

You can use [any named anchor](/angular/docs/apps/edges/anchors.md), but you can also specify custom values for `x`, `y`, `ox` and `oy`, via a comma-delimited string:

```html
<div data-vjs-anchor="0,0.5,-1,0" data-vjs-source="true"/>

```

In this example, we have indicated our anchor is on the left edge, halfway down, and points to the left. This is in fact the same as saying `Left`. But with this syntax you can do things that aren't covered by one of the named anchors, for instance an anchor that sits in the center of some element but points to the left:

```html
<div data-vjs-anchor="0.5,0.5,-1,0" data-vjs-source="true"/>

```

***

### Available attributes[​](#available-attributes "Direct link to Available attributes")

This is the list of supported connectivity attributes:

| Attribute                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `data-vjs-allow-loopback` | Indicates the it should be possible to drag loopback connections from this element to itself.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `data-vjs-anchor`         | Specifies the anchor to use for both source and target of an edge connected to some element, when an edge is dragged from that element as the source.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `data-vjs-edge-type`      | Optional attribute used to tell VisuallyJs what `type` to use from some element that has `data-vjs-source="true"` set.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `data-vjs-enabled`        | Specifies whether or not some drag source/target is enabled.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `data-vjs-magnet`         | Indicates the element acts as a magnet, when edge snapping is turned on.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `data-vjs-port`           | This attribute indicates that the given element is the specific DOM element to which connections for the given port should be attached. It is distinct from `data-vjs-port-id` in that this attribute is a "physical" presence of a port. Connections to/from the associated port are attached to this DOM element, and not to the element representing the vertex to which the port belongs.                                                                                                                                                                                                          |
| `data-vjs-port-id`        | This attribute indicates the ID of the logical port that the element represents. A logical port is one which exists in the data model, but connections to/from the port in the UI are shown as being attached to the vertex to which the port belongs. Don't confuse this with the `data-vjs-port` attribute. When you drag a connection to/from some DOM element with this attribute set, you are instructing VisuallyJs to associate the source/target of the new edge with a port with the specified ID, but that the edge should be connected visually to the DOM element representing the vertex. |
| `data-vjs-port-type`      | Optional attribute used to tell VisuallyJs the type of the port represented by the given element. Maps to a port type defined in your view.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `data-vjs-scope`          | Specifies the value for 'scope' for an edge dragged from some element. Edges will only be able to be dragged to target elements that have the same value for `data-vjs-scope`.                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `data-vjs-source`         | Indicates the given DOM element acts as a source for edges dragged with the mouse/touch events. Any element with this attribute set will automatically be excluded from instigating a drag of the vertex on which the element resides                                                                                                                                                                                                                                                                                                                                                                  |
| `data-vjs-source-anchor`  | Specifies the anchor to use for the source of an edge connected to some element, when an edge is dragged from that element.                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `data-vjs-target`         | Indicates the given DOM element acts as a target for edges dragged with the mouse/touch events. Elements with this attribute set are not excluded from instigating a drag of the vertex on which the element resides.                                                                                                                                                                                                                                                                                                                                                                                  |
| `data-vjs-target-anchor`  | Specifies the anchor to use for the target of an edge connected to some element, when an edge is dragged from that element.                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `data-vjs-target-port`    | Indicates the ID of the physical port represented by this element when the element is acting as the target of some edge. See discussion at `data-vjs-port` to read about how this differs from `data-vjs-target-port-id`                                                                                                                                                                                                                                                                                                                                                                               |

***

## Visual cues[​](#visual-cues "Direct link to Visual cues")

### While dragging[​](#while-dragging "Direct link to While dragging")

There are two main CSS classes you can use to provide visual cues to your users about the state of an edge drag:

* `vjs-drag-active` When an edge is being dragged, this class is assigned to all elements onto which the edge could be dropped

* `vjs-drag-hover` When an edge is being dragged and the mouse is hovering over a possible target, this class is assigned to that element

In the canvas below we have these style rules:

```css
.vjs-node {
    outline:1px solid;
}
  
.vjs-drag-active {
    outline:2px solid forestgreen;
}

.vjs-drag-hover {
  outline:4px solid orangered;
}

```

Try dragging an edge - you'll see the `.vjs-drag-active` class applied to each of the nodes initially. When you drag the edge over one of the nodes you'll see the `.vjs-drag-hover` class applied:

**********

### Connected elements[​](#connected-elements "Direct link to Connected elements")

When some element has one or more edges attached to it, VisuallyJs adds the CSS class `vjs-connected` to the element in the DOM. In the canvas below we have this style rule declared:

```css
.vjs-connected {
    background-color: #0a58ca;
    color:white;
}

```

Nodes 1 and 2 are connected in our initial dataset and are, accordingly, painted with a blue background, via the CSS rule. If you drag a new edge (from one of the red circles) to node 3 you'll see it update to have a blue background, as the `vjs-connected` class will be assigned when the edge is established.

**********

***

## Snapping to drag targets[​](#snapping-to-drag-targets "Direct link to Snapping to drag targets")

You can instruct VisuallyJs to snap to drag targets when dragging edges. The simplest setup is:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  edgeSnap: {
    enabled: true
  }
};
}

```

Which you can see in operation here - try dragging an edge from one of the red circles. As it gets within proximity of one of the other nodes, the edge is snapped:

**********

The canvas above configures each element as a target, and the default behaviour is to snap to any target.

### Limiting snap targets[​](#limiting-snap-targets "Direct link to Limiting snap targets")

If you wish to only snap to certain elements, you can use the `requireMagnets` option:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  edgeSnap: {
    enabled: true,
    requireMagnets: true
  }
};
}

```

Here, we have instructed VisuallyJs to only snap to elements that have declared themselves to be "magnets" - which you configure via the `data-vjs-magnet` attribute in your HTML:

```html
<div data-vjs-target="true" data-vjs-magnet="true">
    ...
</div>

```

In this canvas the node with the red outline is declared as a magnet, because it has `data-vjs-magnet="true"` declared. Try dragging an edge from one of the other nodes. It won't snap to any node except the one with the red border:

**********

### Child elements as target[​](#child-elements-as-target "Direct link to Child elements as target")

Snapping works when something other than the entire element is the target. In this next example we use this markup for our nodes:

```html
<div>
  <div data-vjs-target="true" class="dragToHere"/>
  <div data-vjs-source="true" class="dragFromHere"/>
</div>

```

Our drag targets are the blue circles in the top left corner - and it is to these that edges will snap. But the snapping is activated in proximity to the vertex:

**********

Using nested elements as targets with snapping turned on also, of course, works with `requireMagnets:true` set.

### Adjusting sensitivity[​](#adjusting-sensitivity "Direct link to Adjusting sensitivity")

By default the snapping mechanism will kick in at a distance of 50 pixels from the target. You can change this:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  edgeSnap: {
    enabled: true,
    threshold: 20
  }
};
}

```

**********

***

## Constraining connectivity[​](#constraining-connectivity "Direct link to Constraining connectivity")

There are a couple of different approaches to control connectivity.

### Edge scope[​](#edge-scope "Direct link to Edge scope")

A high level approach to controlling connectivity is offered by the `data-vjs-scope` attribute. Edges dragged from some source element with a `data-vjs-scope` attribute can only be attached to target elements that have a matching `data-vjs-scope`. We use this approach in our Schema builder starter app.

Here, we have two nodes that each contain a list of columns, and each column has a `scope` in its backing data - this is the data object for the node on the left:

```javascript
{ 
    id:"1", 
    left:50, 
    top:50, 
    columns:[
     {id:"one", scope:"cadetblue"}, 
     {id:"two", scope:"darkseagreen"}, 
     {id:"three", scope:"cadetblue" }
    ] 
}

```

We're using HTML colours for our `scope` so that we can style the elements easily, but scope is just an arbitrary string. We render each node this this template:

<!-- -->

Each of our column elements declares `data-vjs-source` and `data-vjs-target` to be true, meaning the element is both a source and target for edges dragged with the mouse. But the key piece is the `data-vjs-scope` attribute: try dragging an edge from a green to blue or vice verse below - you can't, due to a scope mismatch. But you can drag between elements having the same colour.

**********

***

### Interceptors[​](#interceptors "Direct link to Interceptors")

If edge scope is too high level for your needs, you can use `interceptors`, which provide a fine-grained means of controlling connectivity, at the model level.

info

The interceptors discussed here are passed as arguments to the underlying model - they operate at the model level, ie. both on programmatic calls to connect vertices and when the user is connecting vertices via the mouse/touch events.

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

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [modelOptions]="modelOptions"></vjs-surface> `
})
export class AppComponent {
  modelOptions = {
  beforeConnect: (source: Vertex, target: Vertex) => {
      return (source !== target)
  }
};
}

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

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [modelOptions]="modelOptions"></vjs-surface> `
})
export class AppComponent {
  modelOptions = {
  beforeMoveConnection: (source: Vertex, target: Vertex, edge:Edge) => {
      return (edge.data.fixed !== true)
  }
};
}

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

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [modelOptions]="modelOptions"></vjs-surface> `
})
export class AppComponent {
  modelOptions = {
  beforeStartConnect: (source: Vertex, type:string) => {
      return type !== 'not-connectable'
  }
};
}

```

##### Example - provide an initial payload[​](#example---provide-an-initial-payload "Direct link to Example - provide an initial payload")

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [modelOptions]="modelOptions"></vjs-surface> `
})
export class AppComponent {
  modelOptions = {
  beforeStartConnect: (source: Vertex, type:string) => {
      return {
          type,
          message:`initial payload for vertex ${source.id}`
      }
  }
};
}

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

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [modelOptions]="modelOptions"></vjs-surface> `
})
export class AppComponent {
  modelOptions = {
  beforeDetach: (source: Vertex, target: Vertex, edge: Edge, isDiscard?: boolean) => {
      return target != null
  }
};
}

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

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [modelOptions]="modelOptions"></vjs-surface> `
})
export class AppComponent {
  modelOptions = {
  beforeDetach: (source: Vertex, edge: Edge) => {
      return source.data.doNotDetachEdges !== true
  }
};
}

```

##### Multiple interceptors[​](#multiple-interceptors "Direct link to Multiple interceptors")

You can provide multiple interceptors - in this example we provide a `beforeStartConnect` and `beforeDetach` interceptor to the model. The `beforeStartConnect` interceptor prevents the user from dragging connections from any vertex whose ID is not an even number. The `beforeDetach` interceptor reattaches detached connections whose source ID is not an event number

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [modelOptions]="modelOptions"></vjs-surface> `
})
export class AppComponent {
  modelOptions = {
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
};
}

```

**********

## Active filtering[​](#active-filtering "Direct link to Active filtering")

You can use a `beforeConnect` interceptor to implement a scheme where unavailable targets are disabled when the user starts to drag a new connection.

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';

@Component({
  selector: 'app-root',
  template: ` <vjs-surface [modelOptions]="modelOptions"></vjs-surface> `
})
export class AppComponent {
  modelOptions = {
  beforeConnect: (source:Vertex, target:Vertex) => {
      return source.data.scope === target.data.scope
  }
};
}

```

**********

Disabled vertices are assigned the DOM attribute `data-vjs-enabled="false"`, which you can target via css. For example, in this page, we have this rule:

```css
[data-vjs-enabled='false'] {
    filter: grayscale(0.4);
    opacity: 0.5;
}

```

***

## CSS Classes[​](#css-classes "Direct link to CSS Classes")

There are a number of CSS classes assigned to various parts of the UI during an edge drag. These can be used to easily add visual cues for your users, and also to manage z-index for the best user experience.

| Class                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `vjs-connector-source-drag`    | The class assigned to the SVG element with which a user can drag to reposition the source of some edge.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `vjs-connector-target-drag`    | The class assigned to the SVG element with which a user can drag to reposition the target of some edge.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `vjs-connector-transient-drag` | Assigned to the temporary DOM element used when relocating an existing edge via the mouse/touch events.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `vjs-edge-relocating`          | Assigned by the Surface to the DOM element representing an edge that is being dragged to relocate its source or target. This class is only added when the edge input handler is in drag mode. It is assigned to the connector element once the mouse starts to move, and removed on mouseup.                                                                                                                                                                                                                                                                                                |
| `vjs-edge-will-relocate`       | Assigned by the Surface to the DOM element representing an edge that is about to be relocated. When the edge input mode is dragging, this class is assigned on mousedown on one of the drag handles, before the mouse moves, and removed when the mouse begins to move (or on mouseup if the user does not move the mouse). When the edge input mode is tap, this class is assigned when the user has tapped on one of the relocate handles, and is removed either when the user clicks on whitespace, cancelling the relocation, or clicks on an active target and effects the relocation. |
| `vjs-surface-edge-dragging`    | Assigned by the Surface to its root element when an edge is being dragged. This is not assigned to the edge element itself.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

***

## Advanced Markup Configuration[​](#advanced-markup-configuration "Direct link to Advanced Markup Configuration")

Above, we listed the most commonly used attributes to configure connectivity, but there are several more that can be used in more advanced configurations, specifically when you want to use a different physical or logical port mapping depending on whether the connection is to an edge or target.

| Attribute                   | Description                                                                                                                                                                                                                                                                                                                                |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `data-vjs-source-port`      | Indicates the ID of the physical port that the element represents when it is acting as an edge source. In some situations you might want to use the same element as a source and target, but have the data model use different ports ids. See discussion for `data-vjs-port` to read about how this differs from `data-vjs-source-port-id` |
| `data-vjs-source-port-id`   | Indicates the ID of the logical port that the element represents when it is acting as an edge source. In some situations you might want to use the same element as a source and target, but have the data model use different logical ports.                                                                                               |
| `data-vjs-source-port-type` | Indicates the type of the port represented by this element when the element is acting as the source of some edge. Maps to a port type defined in your view. In some situations you might want to use the same element as a source and target, but have the data model use different ports types.                                           |
| `data-vjs-target-port-id`   | Indicates the ID of the logical port that the element represents when it is acting as an edge target.                                                                                                                                                                                                                                      |
| `data-vjs-target-port-type` | Indicates the type of the port represented by this element when the element is acting as the target of some edge. Maps to a port type defined in your view.                                                                                                                                                                                |
