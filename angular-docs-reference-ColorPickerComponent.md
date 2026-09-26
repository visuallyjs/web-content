# ColorPicker

A helper component that offers the ability to manage a color and keep a history of selected colors, for use with an [InspectorComponent](/angular/docs/reference/InspectorComponent.md).

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/angular/docs/reference/InspectorComponent.md) we'd recommend it.

This component is used in the template for an inspector. You need to pass in the name of the property to manage.

note

If you're using standalone components you'll need to include the `VisuallyJsModule` in your component's imports, as shown here, in order to bring the color picker component into scope.

```typescript

import {Component} from "@angular/core"
import { VisuallyJsModule, InspectorComponent } from "@visuallyjs/browser-ui-angular"

@Component({
    imports:[VisuallyJsModule],
    template:`<div>
    <vjs-color propertyName="backgroundColor"/>
</div>`,
    selector:"app-my-inspector"
})
export class MyInspector extends InspectorComponent {}

```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name         | Type   | Description                                             |
| ------------ | ------ | ------------------------------------------------------- |
| maxColors?   | number | Maximum number of colors in history. Defaults to 10.    |
| propertyName | string | The name of the property that maps the color. Required. |

### Outputs[​](#outputs "Direct link to Outputs")

| Name        | Type                  | Description                                                       |
| ----------- | --------------------- | ----------------------------------------------------------------- |
| changeEvent | EventEmitter\<string> | Fires an event when the user selects a new style via mouse click. |
