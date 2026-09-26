# ExportControlsComponent

Provides a set of buttons allowing your users to export a given canvas as SVG, PNG or JPG.

info

This component only works when your surface is using a `ShapeLibrary` to render elements, or if you are using a `Diagram`.

## Usage[​](#usage "Direct link to Usage")

You need to declare an element to host the export controls component:

```html
<!doctype html>
<html>
  <head>
	<link rel="stylesheet" href="node_modules/@visuallyjs/browser-ui/css/visuallyjs.css">
  </head>
  <body>
    <div id="myContainer">
        <div id="exportControls"></div>
    </div>
  </body>
</html>

```

```typescript
import {createSurface, ExportControlsComponent} from "@visuallyjs/browser-ui"

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
new ExportControlsComponent(document.getElementById("exportControls"), surface, {... })

```

## Class Definition[​](#class-definition "Direct link to Class Definition")

Sorry - we could not find this document.

## Constructor Options[​](#constructor-options "Direct link to Constructor Options")

Sorry - we could not find this document.
