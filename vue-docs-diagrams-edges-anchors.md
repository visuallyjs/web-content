# Anchors

An anchor models the notion of where on an element an edge should connect. There are three main types:

* **static** - These are fixed to some point on an element and do not move. They can be specified using a string to identify one of the defaults that VisuallyJs ships with, or an object describing the location and orientation of edges connected to it.

* **dynamic** - These are lists of static anchors from which VisuallyJs selects the most appropriate one each time a connection is painted. The algorithm used to determine the most appropriate anchor picks the one that is closest to the center of the other element in the connection. A future version of VisuallyJs might support a pluggable algorithm to make this decision.

* **continuous** - These anchors are not fixed to any specific location; they are assigned to one of the four faces of an element depending on that element's orientation to the other element in the associated connection. These are the default anchors used by VisuallyJs.

## Static Anchors[​](#static-anchors "Direct link to Static Anchors")

VisuallyJs has nine default anchor locations you can use to specify where the connectors connect to elements: these are the four corners of an element, the center of the element, and the midpoint of each edge of the element:

TopLeft

TopRight

Top

BottomLeft

BottomRight

Bottom

Center

Left

Right

Each of these string representations is just a wrapper around the underlying object-based syntax `{x, y, ox, oy}`, where `x` and `y `are coordinates in the interval `[0,1]` specifying the position of the anchor, and `ox` and `oy`, which specify the orientation of the curve incident to the anchor, can have a value of 0, 1 or -1. For example, `{x:0, y:0.5, ox:-1, oy:0}` defines a `Left` anchor with a connector curve that emanates leftward from the anchor. Similarly, `{x:0.5, y:0, ox:0, oy:-1}` defines a `Top` anchor with a connector curve emanating upwards.

```javascript
anchor:"Bottom"

```

is identical to:

```javascript
anchor:{ x:0.5, y:1, ox:0, oy:1 }

```

### Anchor Offsets[​](#anchor-offsets "Direct link to Anchor Offsets")

In addition to supplying the location and orientation of an anchor, you can optionally supply two more parameters that define an offset in pixels from the given location. Here's the anchor specified above, but with a 50 pixel offset below the element in the y axis:

```javascript
anchor:{ x:0.5, y:1, ox:0, oy:1, offsetX:0, offsetY:50 } 

```

## Dynamic Anchors[​](#dynamic-anchors "Direct link to Dynamic Anchors")

These are anchors that can be positioned in one of a number of locations, choosing the one that is most appropriate each time something moves or is painted in the UI.

There is no special syntax for creating a dynamic anchor; you just provide an array of individual static anchor specifications, eg:

```javascript

anchor:[
    {x:0.2, y:0, ox:0, oy:-1 },
    {x:1, y:0.2, ox:1, oy:0 },
    {x:0.8, y:1, ox:0, oy:1 },
    {x:0, y:0.8, ox:-1, oy:0 } 
]

```

Note that you can mix the types of these individual static anchor specifications:

```javascript
anchor:[
    {x:0.2, y:0, ox:0, oy:-1 },
    {x:1, y:0.2, ox:1, oy:0 },
    "Top",
    "Bottom"
]


```

### Default[​](#default "Direct link to Default")

VisuallyJs provides a dynamic anchor called `AutoDefault` that chooses from `Top`, `Right`, `Bottom` and `Left`:

```javascript
anchor:"AutoDefault"

```

These two nodes have an endpoint with an `AutoDefault` anchor - drag them around and see how they choose from `Top`, `Left`, `Bottom` and `Right` depending on their orientation.

**********

### Location selection[​](#location-selection "Direct link to Location selection")

The algorithm that decides which location to choose just calculates which location is closest to the center of the other element in the edge. It is possible that future versions of VisuallyJs could support more sophisticated choice algorithms, if the need arose.

## Continuous Anchors[​](#continuous-anchors "Direct link to Continuous Anchors")

As discussed above, these are anchors whose positions are calculated by VisuallyJs according to the orientation between elements in a connection, and also how many other continuous anchors happen to be sharing the element. You specify that you want to use continuous anchors using the string syntax you would use to specify one of the default static anchors, for example:

```javascript
anchor:"Continuous"

```

Note in this example we specified only "anchor", rather than "anchors" - VisuallyJs will use the same spec for both anchors. But we could have said this:

```javascript
anchors:["Bottom", "Continuous"]

```

...which would have resulted in the source element having a static anchor at `Bottom`. In practise, though, it seems the continuous anchors work best if both elements in a connection are using them.

Try dragging these nodes around and see how the anchors adapt their positions:

**********

### Face selection[​](#face-selection "Direct link to Face selection")

By default, a continuous anchor will choose points from all four faces of the element on which it resides. You can control this behaviour, though, with the `faces` parameter on the anchor spec:

```javascript
anchor:{ type:"Continuous", options:{ faces:[ "top", "left" ] } }

```

Allowed values are:

* `top`
* `left`
* `right`
* `bottom`

If you provide an empty array for the `faces` parameter, VisuallyJs will default to using all four faces.
