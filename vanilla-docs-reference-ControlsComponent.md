# Controls

This component provides a set of controls for a surface - such operations as zoom to extents, undo/redo, clear, etc. The operations that are available can be specified on the controls element, and you can also add your own buttons.

## Usage[​](#usage "Direct link to Usage")

You need to declare an element to host the controls component:

```html
<!doctype html>
<html>
  <head>
	<link rel="stylesheet" href="node_modules/@visuallyjs/browser-ui/css/visuallyjs.css">
  </head>
  <body>
    <div id="myContainer">
        <div id="controls"></div>
    </div>
  </body>
</html>

```

```typescript
import {createSurface, ControlsComponent} from "@visuallyjs/browser-ui"

const renderOptions = {
   view: {
     nodes: {
       default: {
         template: `<div>{{id}}</div>`
       }
     }
  }
}

const data = {
    nodes: [
        {id: "1", left: 50, top: 50}
    ]
}

const surface = createSurface(document.getElementById("myContainer"), renderOptions)
new ControlsComponent(document.getElementById("controls"), surface, {... })

```

## Class Definition[​](#class-definition "Direct link to Class Definition")

### ControlsComponent

Simple component offering management of pan/zoom, lasso, undo/redo, and a few other features.

constructor [ControlsComponent]()(container:[BrowserElement](), ui:[BrowserUI](), options:[ControlsComponentOptions]())

## Constructor Options[​](#constructor-options "Direct link to Constructor Options")

ControlsComponentOptions

Options for the controls component.

| Name           | Type                         | Description                                                                                                                                                         |
| -------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| buttons?       | [ControlsComponentButtons]() | Optional extra buttons to add to the controls component.                                                                                                            |
| clear?         | boolean                      | Whether or not to show the clear button, defaults to true.                                                                                                          |
| clearMessage?  | string                       | Optional message to show the user when prompting them to confirm they want to clear the dataset                                                                     |
| orientation?   | "row" \| "column"            | Optional orientation for the controls. Defaults to 'row'.                                                                                                           |
| undoRedo?      | boolean                      | Whether or not to show undo/redo buttons, defaults to true                                                                                                          |
| zoom?          | boolean                      | Whether or not to show zoom in/zoom out buttons. Defaults to false when the UI's zoom method is "wheel", and defaults to true when the UI's zoom method is "click". |
| zoomToExtents? | boolean                      | Whether or not to show the zoom to extents button, defaults to true                                                                                                 |
