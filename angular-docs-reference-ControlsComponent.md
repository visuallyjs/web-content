# Controls

HTML Tag

**vjs-controls**

This component provides a set of controls for a surface - such operations as zoom to extents, undo/redo, clear, etc. The operations that are available can be specified on the controls element, and you can also add your own buttons.

## Usage[​](#usage "Direct link to Usage")

```typescript

import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div>
        <vjs-surface [renderOptions]="renderOptions" [data]="data"/>
        <vjs-controls />
        </div>`
})
export class MyApp {
    renderOptions = { ... }
    data = { ... }
}


```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name           | Type                         | Description                                                             |
| -------------- | ---------------------------- | ----------------------------------------------------------------------- |
| buttons?       | [ControlsComponentButtons]() | Optional extra buttons to display in the component.                     |
| clear?         | boolean                      | Whether or not to show the clear model button. Defaults to true.        |
| clearMessage?  | string                       | Message to show when the user clicks the clear model button.            |
| orientation?   | string                       | Orientation of the component - `"row"` or `"column"`                    |
| undoRedo?      | boolean                      | Whether or not to show undo/redo buttons. Defaults to true.             |
| zoomButtons?   | boolean                      | Whether or not to show the zoom in/zoom out buttons. Defaults to false. |
| zoomToExtents? | boolean                      | Whether or not to show the zoom to extents button. Defaults to true.    |
