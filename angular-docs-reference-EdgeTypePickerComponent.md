# EdgeTypePicker

This component provides the means for a user to pick an edge type from a visual rendering of the available options. It reads the current list of edge property mappings from the surface its inspector is attached to, and draws a sample of each one in a list for the user to select from. It is designed for use inside of an Inspector.

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/angular/docs/reference/InspectorComponent.md) we'd recommend it.

This component is used in the template for an inspector. You need to input the name of the property to manage.

note

If you're using standalone components you'll need to include the `VisuallyJsModule` in your component's imports, as shown here, in order to bring the color picker component into scope.

```typescript

import {Component} from "@angular/core"
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
    imports:[VisuallyJsModule],
    template:`<div>
    <vjs-edge-type propertyName="edgeType"/>
</div>`,
    selector:"app-my-inspector"
})
export class MyInspector extends InspectorComponent {}

```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name          | Type                     | Description                                                                                                                                             |
| ------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| edgeMappings? | [EdgePropertyMappings]() | Set of edge property mappings to render and allow the user to select from.<br />Optional. By default the component will retrieve these from the surface |
| propertyName  | string                   | The name of the property that maps the edge type. Required.                                                                                             |

### Outputs[​](#outputs "Direct link to Outputs")

| Name        | Type                  | Description                                                       |
| ----------- | --------------------- | ----------------------------------------------------------------- |
| changeEvent | EventEmitter\<string> | Fires an event when the user selects a new style via mouse click. |

## Edge Mappings[​](#edge-mappings "Direct link to Edge Mappings")

This component expects that you have some edge mappings declared on your surface - it is these that the component displays for the user to select from.

Edge mappings allows you to match specific values for a given property to a set of config options for an edge.

An edge mapping declares a `property`, which is the name of some property an edge's backing data that VisuallyJs will attempt to match. In the code snippet below we're matching the property `lineStyle`. Then there is a `mappings` section, which is an object whose keys are the values we're matching.

In this example we see four possible matches - `"source"`, `"target"`, `"plain"` and `"dashed"`. Each match then declares a set of zero or more configuration options for the edge.

The `name` property is optional; it is used in the edge property mapper inspector as the default label to show for the section pertaining to the property mapping. If omitted, the value of `property` will be used as the section label.

```json
{
    "property": "lineStyle",
    "name": "Line Style",
    "mappings": {
      "source": {
        "overlays": [
          {
            "type": "Arrow",
            "options": {
              "location": 0,
              "direction": -1,
              "width": 5,
              "length": 10
            }
          }
        ]
      },
      "target": {
        "overlays": [
          {
            "type": "Arrow",
            "options": {
              "location": 1,
              "width": 5,
              "length": 10
            }
          }
        ]
      },
      "plain": {},
      "dashed": {
        "cssClass": "some-css-class"
      }
    }
}

```
