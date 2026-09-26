# ShapePropertiesInspector

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/angular/docs/reference/InspectorComponent.md) we'd recommend it.

This component renders the properties defined by the selected shape in the active shape library. Use it inside an inspector and pass it the vertex being inspected. The Angular selector is `<vjs-shape-properties-inspector>`.

note

If you're using standalone components you'll need to include the `VisuallyJsModule` in your component's imports, as shown here, in order to bring the component into scope.

```typescript
import { Component } from "@angular/core"
import { Node, Group } from "@visuallyjs/browser-ui"
import { InspectorComponent, VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
  imports: [VisuallyJsModule],
  template: `@if (currentObjectType === 'Node') {
    <vjs-shape-properties-inspector [vertex]="asNode(currentObj)" />
  }`,
  selector: "app-my-inspector"
})
export class MyInspector extends InspectorComponent<Node | Group> {
  asNode(obj: any): Node {
    return obj as Node
  }
}

```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name       | Type       | Description                                                                                                        |
| ---------- | ---------- | ------------------------------------------------------------------------------------------------------------------ |
| maxRadios? | number     | The maximum number of radio buttons to show for a value list before switching to a select dropdown. Defaults to 7. |
| vertex     | [Vertex]() | vertex to inspector                                                                                                |

`maxRadios` controls how many choices are displayed as radio buttons before the inspector uses a dropdown.
