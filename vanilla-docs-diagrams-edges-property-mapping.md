# Property Mapping

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
