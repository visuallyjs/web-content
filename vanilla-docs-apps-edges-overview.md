# Edges

Edges map relationships between the vertices in your UI. In the data model, an edge consists of a source vertex (node, group or port) or canvas location, a target vertex or canvas location, and some optional backing data, such as ID, type, label etc.

In the UI, an edge is represented by a few concepts that work in tandem:

* **Anchor** The location of each end of an edge on a vertex is determined by its source and target [anchors](#anchors)
* **Connector** The path inscribed by the edge is determined by its [connector type](/vanilla/docs/apps/edges/connectors.md), and also by any [path edits made by the user](/vanilla/docs/apps/edges/path-editing.md)
* **Overlays** An edge may have zero or more [overlays](/vanilla/docs/apps/edges/overlays.md), which are adornments that can be placed at any point along the path inscribed by the edge.
* **Markers** A [marker](/vanilla/docs/apps/edges/markers.md) is an overlay that is placed at the start or end of an edge (equivalent to location 0 or location 1). When a marker is located at the start or end of an edge, the path is automatically trimmed so that it terminates at the marker.

Edges may also be detached from the source and/or target and terminate in whitespace, if you [configure this behaviour](/vanilla/docs/apps/edges/unattached-edges.md).

```javascript
import { newInstance } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  edges: {
    sourceMarker: "Dot",
    targetMarker: "PlainArrow",
    connector: "QuadraticBezier",
    overlays: [
      {
        type: "Label",
        options: {
          label: "{{label}}"
        }
      }
    ]
  }
})

```

**********

<!-- -->

## Anchors[​](#anchors "Direct link to Anchors")

The location of each end of an edge is specified by an `Anchor`, of which there are several different types in VisuallyJs: you can choose to anchor an edge at some specific location and not let it move, or you can choose from a few different approaches for dynamic selection of the anchor location. Take a look at the [Anchors reference](/vanilla/docs/apps/edges/anchors.md) for a thorough discussion.

## Adding edges[​](#adding-edges "Direct link to Adding edges")

Edges can be added to your app in a few different ways:

* Via [drag and drop](/vanilla/docs/apps/edges/dragging-edges.md) with the mouse or touch events
* Via [click to add](/vanilla/docs/apps/edges/click-to-add-edges.md) with the mouse or touch events
* By a [data load](/vanilla/docs/apps/model/io/loading-and-saving-data.md)
* By programmatically [adding an edge to the model](/vanilla/docs/apps/model/edges.md#add)

## Defining appearance and behaviour[​](#defining-appearance-and-behaviour "Direct link to Defining appearance and behaviour")

VisuallyJs will use a `Straight` connector and a `Continuous` anchor by default for all edges, but for most use cases you'll almost certainly want to modify this behaviour, which you can do in one of two ways:

* For basic settings that will apply to all edges, you can set [defaults](#defaults)
* For fine-grained control of edges on a per-type basis, you can map edge types in a [view](#view)
