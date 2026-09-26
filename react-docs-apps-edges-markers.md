# Markers

Markers are overlays that are being used in the specific context of marking the source or target of some edge. `Label` and `Custom` overlays are not supported for markers, but all of the simple shape overlays are.

In this example we show a `Dot` marker as the source and a `PlainArrow` as the target.

```javascript
edges:{
    sourceMarker:"Dot",
    targetMarker:"PlainArrow"
}

```

**********

info

## Location[​](#location "Direct link to Location")

Although markers are just overlays, you do not supply a location when specifying a marker - or rather, you do, but implicitly, by the fact that you have identified a marker as a `sourceMarker` (location:0) or a `targetMarker` (location:1). VisuallyJs will automatically set this location and also set `direction:-1` for a target marker.

## Differences to overlays[​](#differences-to-overlays "Direct link to Differences to overlays")

Markers are specified with the same syntax as overlays, so what is the difference? There are two:

### Syntax[​](#syntax "Direct link to Syntax")

The `sourceMarker` / `targetMarker` syntax is a useful shortcut to having to declare a set of `overlays` and configuring the properties required to set an overlay at the source/target of an edge. It is the difference, for instance, of typing this:

```javascript
markers:{
    sourceMarker:"Dot",
    targetMarker:"PlainArrow"
}

```

versus typing this:

```javascript
overlays:[
    { type:"Dot", options:{location:0}},
    { type:"PlainArrow", options:{location:1}}
]

```

### Edge overlap[​](#edge-overlap "Direct link to Edge overlap")

When an overlay is used as a marker, the path of the edge is adjusted so that it stops at the edge of the marker. An exaggerated example is given below - in this canvas, the edges have a stroke width of 8 pixels, and you can see in the top edge how the edge path intersects the overlays whereas in the bottom edge it does not.

**********
