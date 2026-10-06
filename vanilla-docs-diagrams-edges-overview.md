# Connecting shapes

Edges in a Diagram represent the relationships between nodes and groups. They are highly configurable, supporting various connector types, overlays (like arrows), and markers.

## Configuration[​](#configuration "Direct link to Configuration")

You configure the default behavior and appearance of edges in a Diagram using the `edges` section of the `DiagramOptions` interface.

```javascript
const diagramOptions = {
  // ... other options
  edges: {
    anchor: "AutoDefault",          // Default anchor for edges
    connector: {                    // Default connector type and options
        type: "Orthogonal",
        options: {
            cornerRadius: 3
        }
    },
    editable: true,                 // Whether edges can be edited via the UI
    avoidVertices: true,            // Whether edges should avoid overlapping vertices
    allowUnattached: true,          // Whether edges can exist without being connected to a target
    propertyMappings: []       // Mappings to drive edge appearance from data
  }
}

```

### Options[​](#options "Direct link to Options")

The `edges` section supports the following options:

| Name               | Type                   | Description                                                                            |
| ------------------ | ---------------------- | -------------------------------------------------------------------------------------- |
| `anchor`           | `AnchorSpec`           | The default anchor(s) to use for edges.                                                |
| `connector`        | `ConnectorSpec`        | The default connector type (e.g., "Orthogonal", "Bezier", "Straight") and its options. |
| `editable`         | `boolean`              | Whether edges are editable by the user. Defaults to `true`.                            |
| `avoidVertices`    | `boolean`              | If `true`, the connector will attempt to route around vertices.                        |
| `allowUnattached`  | `boolean`              | If `true`, users can drag an edge that isn't connected to a target vertex.             |
| `propertyMappings` | `EdgePropertyMappings` | A set of mappings that define how edge data affects its appearance.                    |
| `color`            | `string`               | Default color for the edges.                                                           |
| `outlineWidth`     | `number`               | Default width for the edge lines.                                                      |

## Linking from Diagram tools[​](#linking-from-diagram-tools "Direct link to Linking from Diagram tools")

When a vertex (node or group) is selected in a Diagram, a set of tools appears around it. One of these tools is the **Link** tool (usually represented by a chain icon or a plus icon with an arrow).

Dragging from this tool allows users to create a new edge. You can control whether this tool is available for a specific vertex using the `canLink` method in the [Diagram Mediator](/vanilla/docs/diagrams/controlling-diagram-actions.md).

## Connectors[​](#connectors "Direct link to Connectors")

Connectors define the path that an edge takes between its source and target.

Connectors are the lines that actually join elements of the UI. They are the visual representation of edges. VisuallyJs has four connector types:

* **Bezier** - a Bezier curve with two control points
* **Straight** - One or more straight line segments, optionally smoothed or with rounded corners
* **Orthogonal** - Horizontal/vertical straight line segments, optionally with rounded corners
* **QuadraticBezier** - a Bezier curve with a single control point

info

The default, if you do not provide a value, is to use the `Straight` connector.

## Overlays and Markers[​](#overlays-and-markers "Direct link to Overlays and Markers")

Overlays are UI elements attached to an edge, such as arrows, labels, or custom shapes. Markers are specific types of overlays that appear at the start or end of an edge.

In Diagrams, you typically use `propertyMappings` to define which overlays or markers should be visible based on the edge's data.

## Unattached Edges[​](#unattached-edges "Direct link to Unattached Edges")

By default, edges in a Diagram must be connected to both a source and a target, but unattached edges are supported and can be enabled. You can toggle this behavior using the `allowUnattached` option.

When `allowUnattached` is set to `true`, users can drag either end of an edge off a shape and leave it in whitespace. This is useful for creating diagrams where some connections might be incomplete or for visually indicating flow that doesn't yet have a target.

**********

## Edge Geometry and Editors[​](#edge-geometry-and-editors "Direct link to Edge Geometry and Editors")

When `editable` is set to `true` in the `edges` configuration, users can modify the path of an edge. VisuallyJs automatically selects the appropriate editor based on the connector type.

VisuallyJs supports editing the path of edges for each of the different [connector types](/vanilla/docs/diagrams/edges/connectors.md) that VisuallyJs ships with. The selection of the appropriate editor tool is managed automatically by VisuallyJs.

## Setup[​](#setup "Direct link to Setup")

In a diagram, edge path editing is enabled by default (as long as the diagram is not marked `editable:false`). If you want to disable path editing, without marking the diagram readonly, you need to set the `editable` flag in the `edges` section of your render options:

<!-- -->

Path editing begins when the user taps on an edge, and stays active until they click on whitespace, or perform some other operation such as editing a cell,

Each editor offers a different interface for working with path edits.

## Orthogonal editors[​](#orthogonal-editors "Direct link to Orthogonal editors")

The orthogonal editor draws a handle on each segment of an edge, which can be dragged at 90 degrees to the direction of travel of the segment, ie. for a vertical segment, you can shift it horizontally, and for a horizontal segment you can shift it vertically.

When you are shifting a segment, if you release the mouse at such a point that the segment you just dragged forms a straight line with a previous or subsequent segment, the segments are coalesced into one. If you drag some segment such that an existing segment ceases to be a straight line, the segment is split and new segment is inserted between them.

#### Static anchors[​](#static-anchors "Direct link to Static anchors")

In this example we use an edge editor to edit the path of some edge whose anchors are at fixed points (in this case, `AnchorLocations.Bottom` and `AnchorLocations.Top`). We've also already called `startEditingPath(..)` on the surface for you:

**********

#### Dynamic anchors[​](#dynamic-anchors "Direct link to Dynamic anchors")

If the edge you are editing has [dynamic anchors](/vanilla/docs/diagrams/edges/anchors.md#dynamic), the edge editor will draw a placeholder at each end of the edge, which you can drag around to any supported position for the given anchor - here we use the `AutoDefault` dynamic anchor, which is an anchor that has one position on each of the four sides of the element on which it resides:

**********

When you start to drag an anchor placeholder, you'll see VisuallyJs adds an element indicating an allowed position to which that anchor can be moved.

#### Continuous anchors[​](#continuous-anchors "Direct link to Continuous anchors")

If your edge is using anchor of type `AnchorLocations.Continuous` (which is the default), when you drag an anchor placeholder VisuallyJs will highlight the candidate face for the anchor relocation:

**********

### Avoiding vertices[​](#avoiding-vertices "Direct link to Avoiding vertices")

By default, the orthogonal connector editor will avoid getting into a situation where either end of the connector intersects the source or target vertex. This is best illustrated with a picture:

![Orthogonal connector avoiding vertices - When you've reached the limits with SvelteFlow, VisuallyJs has what you need](/assets/images/orthogonal-vertex-avoid-9fcefb5d55b5b5adae49eab8cea35f12.gif)

info

This functionality is only applied to the segments at either end of a connector. If you have some connector path that intersects the source or target vertex somewhere in the middle of the path, the path will not be re-routed to avoid the vertex.

If you want to switch this behaviour off, you can do so in the connector spec:

```javascript
connector:{
    type:"Orthogonal",
    options:{
        vertexAvoidance:false
    }
}

```

This will be the resulting behaviour:

![Orthogonal connector intersecting vertices - VisuallyJs - flowcharts, AI Agent builders, chatbots, bar charts, decision trees, mindmaps, org charts and more](/assets/images/orthogonal-vertex-overlap-f3e8fb219b8294131ab7fbd8194b790f.gif)

Your users can still route the connector around in this setup but they'll have to move a lot more segments.

***

## Straight editors[​](#straight-editors "Direct link to Straight editors")

The straight editor draws a handle at the end of each segment of an edge, which can be dragged in any direction to alter its location. You can split a segment by clicking and holding the mouse at the location you wish to split the segment, and then dragging the new handle.

To delete a handle, click on it.

#### Static anchors[​](#static-anchors-1 "Direct link to Static anchors")

In this example we use an edge editor to edit the path of some edge whose anchors are at fixed points (in this case, `AnchorLocations.Right` and `AnchorLocations.Top`). We've also already called `startEditingPath(..)` for you:

**********

#### Dynamic anchors[​](#dynamic-anchors-1 "Direct link to Dynamic anchors")

If the edge you are editing has [dynamic anchors](/vanilla/docs/diagrams/edges/anchors.md#dynamic), the edge editor will draw a placeholder at each end of the edge, which you can drag around to any supported position for the given anchor - here we use the `AutoDefault` dynamic anchor, which is an anchor that has one position on each of the four sides of the element on which it resides:

**********

When you start to drag an anchor placeholder, you'll see VisuallyJs adds an element indicating an allowed position to which that anchor can be moved.

#### Continuous anchors[​](#continuous-anchors-1 "Direct link to Continuous anchors")

If your edge is using anchor of type `AnchorLocations.Continuous`, when you drag an anchor placeholder VisuallyJs will highlight the candidate face for the anchor relocation:

**********

### Smoothed connectors[​](#smoothed-connectors "Direct link to Smoothed connectors")

When you have `smooth:true` set on your connector, the editor functions slightly differently - the drag handles now represent the location of the control points for the splines that make up the Bezier curve, and when you drag them, the control points are moved accordingly. Also when `smooth` is set, the editor draws a guideline for each segment.

<!-- -->

**********

***

## Bezier editors[​](#bezier-editors "Direct link to Bezier editors")

The bezier editor draws two handles - one for each control point in the connector. They are placed where the control point is, and as you drag them around the control points are updated accordingly.

#### Static anchors[​](#static-anchors-2 "Direct link to Static anchors")

In this example we use an edge editor to edit the path of some edge whose anchors are at fixed points (in this case, `AnchorLocations.Bottom` and `AnchorLocations.Top`). We've also already called `startEditingPath(..)` on the surface for you:

**********

***

## QuadraticBezier editors[​](#quadraticbezier-editors "Direct link to QuadraticBezier editors")

The QuadraticBezier editor draws one handle, located at the connector's control point. As you drag the handle around, the connector's control point is updated.

**********

***

## Overlays[​](#overlays "Direct link to Overlays")

You can supply a set of overlays to render on an edge for the duration of the edit, for example:

```javascript

diagram.startEditingPath(someEdge, {
  overlays:[
    {
      type:LabelOverlay.type,
      options:{
        label:"editing...",
        location:0.1
      }
    }    
  ]
})

```

With this call we get a label overlay at location 0.1:

**********

## Delete button[​](#delete-button "Direct link to Delete button")

The edge path editor offers a shortcut method to attach a delete button:

```javascript
diagram.startEditingPath(someEdge, {
  deleteButton:true
})

```

This results in:

**********

This will delete the edge without prompting the user. If you'd like to hook into the edge deletion, you can provide an `onMaybeDelete` function.

```javascript
diagram.selectEdge(someEdge, {
  deleteButton:true,
  onMaybeDelete:(edge, connection, doDelete) => {
      if (confirm(`Delete edge ${edge.id}`)) {
          doDelete()
      }
  }
})

```

**********

Note that the operation is asynchronous - in the example above we use the windows `prompt` method, but you can invoke the `doDelete` callback at any stage.

## Clearing path edits[​](#clearing-path-edits "Direct link to Clearing path edits")

Edits made to a path can be cleared via `clearPathEdits` method on the `Diagram` object.

```javascript
clearPathEdits (edgeOrLink:Edge|DiagramLink):boolean


```

### Edge Geometry[​](#edge-geometry "Direct link to Edge Geometry")

The `geometry` of an edge is stored in its backing data when it has been edited or when vertex avoidance is active. This geometry consists of the anchor positions and any intermediate segments or control points.

## Edge Mappings[​](#edge-mappings "Direct link to Edge Mappings")

Edge mappings are a powerful way to drive the visual representation of an edge (its style, overlays, and markers) from the properties in its backing data.

Property mappings allow you to match specific values for a given property/properties to a set of config options - it's related to the concept of UI States, but it's a "pull" rather than "push": when you update the model, the UI figures out what config to apply for a given object, rather than you having to tell it.

info

This functionality is available only for edges. We are investigating options for how this could be usefully extended to nodes, groups and ports.

```javascript
import { ArrowOverlay } from "@visuallyjs/browser-ui"

const arrowWidth = 15
const arrowLength = 10

const edgeMappings = [
{
  property:lineStyleProperty,
  name:"Line Style",
  mappings:{
    "plain:{ },
    dashed:{
      dashArray:"2"
    }
  }
},
{
  property:"markers",
  name:"Markers",
  mappings:{
    noArrows:{
      sourceMarker:null,
      targetMarker:null
    },
    sourceArrow:{
      sourceMarker:{
        type:ArrowOverlay.type, 
        options:{
          width:arrowWidth, 
          length:arrowLength
        }
      }
    },
    targetArrow:{
        targetMarker:{ 
          type:ArrowOverlay.type, 
          options:{
            width:arrowWidth, 
            length:arrowLength
          } 
        }
    },
    "bothArrows":{
        sourceMarker:{
            type:ArrowOverlay.type,
            options:{
                width:arrowWidth,
                length:arrowLength
            }
        },
        targetMarker:{
            type:ArrowOverlay.type,
            options:{
                width:arrowWidth,
                length:arrowLength
            }
        }
    }
  }
}]

```

With the mappings shown above, if you had an edge with this definition:

```javascript
{
  source: "1",
  target: "2",
  data:{
      lineStyle:"sourceArrow"
  }
}

```

Then the corresponding connection would have an `Arrow` overlay as its source marker.

## Mapping types[​](#mapping-types "Direct link to Mapping types")

Each mapping consists of a property name (or list of names - see below) and a map of values to configs - the specific type of these configs is defined by the `EdgeMapping` interface:

EdgeMapping

The mapping for the definition of an edge inside a view.

| Name                    | Type                               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ----------------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| allowUnattached?        | boolean                            | Whether or not to allow this type of edge to have a source and/or target in whitespace rather than connected to a vertex. Defaults to false. When this is set to true, a user may drag a new edge of this type and drop it into whitespace, and they may also - subject to whether or not the edge is detachable - detach an edge of this type via the mouse/pointer events, and drop into whitespace. If you do not need this level of control you can also use the `allowUnattached` flag in the `edges` section of the UI render options. If you have this set on an edge type, it will override `allowUnattached` from the edges UI options. |
| anchor?                 | [AnchorSpec]()                     | Spec for the anchor to use for both source and target for edges of this type.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| anchors?                | \[[AnchorSpec](), [AnchorSpec]()]  | \[source, target] anchor specs edges of this type.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| avoidVertices?          | boolean                            | If true, the edge will be routed to avoid any vertices. Note that if your edge has any user edits, or was loaded with a path specified, the edge will not be routed to avoid vertices.                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| color?                  | string                             | Color to paint the edge's path                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| connector?              | [ConnectorSpec]()                  | Name/definition of the connector to use. If you omit this, the default connector will be used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| cssClass?               | string                             | CSS class to add to edges of the type in the UI                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| dashArray?              | string                             | Definition of dash pattern to use to draw the edge path                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| deleteButton?           | boolean \| [OverlayVisibility]()   | Optional delete button.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| deleteButtonClass?      | string                             | Optional class name to set on the delete button. Defaults to "vjs-edge-delete".                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| deleteButtonLocation?   | number \| Array\<number>           | Location for an edge's delete button, if applicable. Defaults to 0.1. You can supply an array of locations if you want multiple buttons.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| deleteConfirm?          | [EdgeDeleteConfirmationFunction]() | An optional function to invoke if the user presses the delete button on some edge. When this is present and the user clicks an edge delete button, instead of just deleting the edge, this function is invoked. It is passed the edge that is a candidate for deletion, and a function which you must invoke if you wish to proceed.                                                                                                                                                                                                                                                                                                             |
| detachable?             | boolean                            | Whether or not edges of this type should be detachable with the mouse. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| events?                 | [EdgeEventOptions]()               | Optional map of event bindings.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| gradient?               | Array<\[number, string]>           | An array of color stops to use as a linear gradient for the edge path. When this is set, `color` is ignored.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| hoverPaintStyle?        | [PaintStyle]()                     | Paint style to use for the edge when the pointer is hovering over it.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ignore?                 | boolean                            | Whether or not to ignore (ie. exclude from the display) edges of this type.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| label?                  | string                             | Optional label to use for the edge. If this is set, a label overlay will be created and the value of `label` will be used as the overlay's label. This value can be parameterised, in order to extract a value from the edge's backing data, eg. if you set `label:"{{name}}"` then VisuallyJs would attempt to extract a property with key `name` from the edge's backing data, and use that property's value as the label.                                                                                                                                                                                                                     |
| labelBackgroundStyle?   | [LabelBackgroundStyle]()           | Optional style for the label's background. This is ignored if `useHTMLLabel` is set to true.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| labelClass?             | string                             | Optional css class to set on the label overlay created if `label` is set. This is a static string and does not support parameterisation like `label` does.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| labelFont?              | [FontSpec]()                       | Optional spec for label font. Will use browser defaults if not specified (or CSS, but remember that CSS is not taken into account when you export an SVG from a diagram or an app using an SVG container)                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| labelLocation?          | number                             | Optional location for the label. If not provided this defaults to 0.5, but the label location can be controlled via the `labelLocationAttribute`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| labelLocationAttribute? | string                             | This defaults to `labelLocation`, and indicates the name of a property whose value can be expected to hold the location at which the label overlay should be located. The default value for this is `labelLocation`, but the key here is that VisuallyJs looks in the edge data for `labelLocation`, so the location is dynamic, and can be changed by updating `labelLocation`. This parameter allows you to change the name of the property that VisuallyJs will look for in the edge data.                                                                                                                                                    |
| labelsRotatable?        | boolean \| "strict" \| "legible"   | Sets whether the label can be rotated to match the gradient of the connector at that location at which it is positioned. If you supply boolean true here, the label will be made rotatable in "legible" mode, in which VisuallyJs ensures that the label is always easy to read, by avoiding rotating the text so that it is upside down or other awkward to read. You can set "strict" mode, which will rotate the label to the appropriate angle regardless of whether or not it will make the label difficult to read.                                                                                                                        |
| lineWidth?              | number                             | Width of the edge path                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| mergeStrategy?          | string                             | When merging a type description into its parent(s), values in the child for `connector`, `anchor` and `anchors` will always overwrite any such values in the parent. But other values, such as `overlays`, will be merged with their parent's entry for that key. You can force a child's type to override *every* corresponding value in its parent by setting `mergeStrategy:'override'`.                                                                                                                                                                                                                                                      |
| outlineColor?           | string                             | Color to paint the edge's outline path                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| outlineWidth?           | number                             | Width to draw the edge's outline path                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| overlays?               | Array<[OverlaySpec]()>             | Array of overlays to add to edges of this type.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| paintStyle?             | [PaintStyle]()                     | Paint style to use for the edge.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| parent?                 | string \| Array\<string>           | Optional ID of one or more edge definitions to include in this definition. The child definition is merged on top of the parent definition(s). Circular references are not allowed and will throw an error.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| reattach?               | boolean                            | Whether or not when a user detaches a edge of this type it should be automatically reattached. Defaults to false.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| sourceMarker?           | [OverlaySpec]()                    | Optional overlay to place at the source of an edge of this type. Location will be set to 0 and direction will be set to -1. This is a shorthand for declaring an overlay at location 0 in the overlays array.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| targetMarker?           | [OverlaySpec]()                    | Optional overlay to place at the target of an edge of this type. Location will be set to 1 and direction will be set to 1. This is a shorthand for declaring an overlay at location 1 in the overlays array.                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| useHTMLLabel?           | boolean                            | By default, an SVG element will be used for an edge's label overlay. This is good because the label can be exported as part of an SVG export of your canvas. If you wish to use an HTML element instead, set this flag.                                                                                                                                                                                                                                                                                                                                                                                                                          |

## Updating data[​](#updating-data "Direct link to Updating data")

When an edge is updated, the property mappings are inspected. Any that are no longer valid are removed, and any that are now valid are added:

```javascript
model.updateEdge(someEdge, {
  lineStyle:EDGE_TYPE_DASHED
})

```

This would result in the arrow overlay being removed, and `"some-css-class"` being added to the connection's class list, because there is a mapping for `EDGE_TYPE_DASHED`:

```javascript
mappings:{
  ...
  [EDGE_TYPE_DASHED]:{
    cssClass:CLASS_DASHED_EDGE
  }
}

```

## Wildcard mappings[​](#wildcard-mappings "Direct link to Wildcard mappings")

You can use "\*" or `WILDCARD` from `@visuallyjs/browser-ui` as the value for some property, which will instruct the UI that the given config should be applied regardless of the value of the mapped property (as long as it is present, not null):

```javascript
import { WILDCARD } from "@visuallyjs/browser-ui"

{
  property:"label",
  mappings:{
    [WILDCARD]:{
      overlays:[{
        type:LabelOverlay.type,
        options:{
          label:"{{label}}",
          location:0.5,
          cssClass:"some-label"
        }
      }]
    }
  }
}

```

Here, we have instructed VisuallyJs to show a label whenever an edge's backing data has a `label` property. Incidentally, this specific requirement can actually be neatly handled by [Edge labels](/vanilla/docs/diagrams/edges/edge-labels.md).

## Multiple properties[​](#multiple-properties "Direct link to Multiple properties")

You can map multiple properties instead of just a single property if you need the extra flexibility. For example, these are property mappings for an edge in a conceptual ERD, in which edges between entities and relationships show cardinality, but only at one end. We can model that with two properties:

```javascript
propertyMappings: [
{
  property: ["cardinality", "terminus"],
  mappings:{
    "one source": {
      sourceMarker: OneOverlay.type
    },
    "one target": {
      targetMarker: OneOverlay.type
    }
  }
}]

```

Then in our dataset we might have edges like this:

```javascript
[
    { source:"1", target:"2", data:{ cardinality:"one", terminus:"source" }},
    { source:"2", target:"3", data:{ cardinality:"many", terminus:"target" }}
]

```

The important point to note in the example mapping above is that the order of the keys must be reflected in the mapping keys: we declare `["cardinality", "terminus"]` as our properties, and our mapping keys are `"one source"` and `"one target"`, ie. the values to match are in the same order as the property keys.

### Examples[​](#examples "Direct link to Examples")

#### Flowchart Starter App[​](#flowchart-starter-app "Direct link to Flowchart Starter App")

In the Flowchart starter app, edge mappings are used to switch between different arrow configurations and line styles (plain or dashed).

```typescript
export default function edgeMappings(): EdgePropertyMappings {
    return [
        {
            property: "lineStyle",
            mappings: {
                "plain": { },
                "dashed": {
                    dashArray: "2"
                }
            }
        },
        {
            property: "markers",
            mappings: {
                "source": {
                    overlays: [
                        { type: ArrowOverlay.type, options: { location: 0, direction: -1 } }
                    ]
                },
                "target": {
                    overlays: [
                        { type: ArrowOverlay.type, options: { location: 1 } }
                    ]
                }
            }
        }
    ]
}

```

#### BPMN Starter App[​](#bpmn-starter-app "Direct link to BPMN Starter App")

The BPMN starter app uses edge mappings to distinguish between sequence flows and message flows, applying different markers and dash patterns.

```javascript
export default function getFlowTypes() {
    return [
        {
            property: "type",
            mappings: {
                "sequence": {
                    targetMarker: {
                        type: "PlainArrow",
                        options: { location: 1 }
                    }
                },
                "message": {
                    dashArray: "3",
                    targetMarker: {
                        type: "PlainArrow",
                        options: { hollow: true }
                    },
                    sourceMarker: {
                        type: "Dot",
                        options: { radius: 6, hollow: true }
                    }
                }
            }
        }
    ]
}

```
