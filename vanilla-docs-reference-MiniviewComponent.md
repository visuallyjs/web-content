# Miniview

Provides a miniaturized view of a surface, showing the nodes/groups in the surface canvas. Users can pan/zoom the surface via pointer/touch events on the miniview, and click on specific vertices to have the surface center itself on the clicked vertex.

## Usage[​](#usage "Direct link to Usage")

The miniview is a surface plugin:

```html
<!doctype html>
<html>
  <head>
	<link rel="stylesheet" href="node_modules/@visuallyjs/browser-ui/css/visuallyjs.css">
  </head>
  <body>
    <div id="myContainer">
        <div id="miniview"></div>
    </div>
  </body>
</html>

```

```typescript
import {createSurface, MiniviewPlugin} from "@visuallyjs/browser-ui"

const renderOptions = {
  plugins: [
    {
      type: MiniviewPlugin.type,
       options:{
         container:document.getElementById("miniview")
       }
    }
  ],
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


```

## Lasso[​](#lasso "Direct link to Lasso")

By default, as a user drags the lasso on the main canvas to select elements, a corresponding lasso will appear in the miniview, showing the selection area in context of the overall diagram.

We've selected the lasso tool in this canvas - drag it around and you'll see the miniview displaying the lasso also.

**********

To disable this feature and prevent the lasso from being shown in the miniview, you can set `showLasso` to `false` in the miniview plugins options:

```javascript
plugins: [
    {
        type: MiniviewPlugin.type,
        options:{
            container:document.getElementById("miniview"),
            showLasso:false
        }
    }
]

```

## Selected vertices[​](#selected-vertices "Direct link to Selected vertices")

The miniview highlights vertices that are part of the current selection on the main canvas, by assigning the CSS class `.vjs-miniview-selected` to the elements representing these vertices in the miniview.

In this canvas, two nodes are initially selected, and are shown as highlighted in the miniview. Tap a node to set it as the current selection.

Being able to see the selected elements inside the miniview is particularly useful with large datasets, where one or more selected vertices may not currently be in the viewport. When someone lassos a large area and the canvas has been panned, it's helpful for them to be able to see everything that is currently selected.

This option defaults to `true`, meaning selection tracking is active by default. However, you can explicitly set `trackSelection` to `false` in the miniview's options if you wish to disable this behavior.

```javascript
plugins: [
    {
        type: MiniviewPlugin.type,
        options:{
            container:document.getElementById("miniview"),
            trackSelection:false
        }
    }
]

```

## Props[​](#props "Direct link to Props")

MiniviewPluginOptions

Options for the MiniviewPlugin

| Name              | Type                                | Description                                                                                                                                                                                                   |
| ----------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| activeTracking?   | boolean                             | Defaults to true, meaning the miniview actively updates as nodes/groups are dragged on the related surface. If this is set to false, the miniview only updates after mouseup.                                 |
| clickToCenter?    | boolean                             | Defaults to true, meaning a click on a node/group in the miniview will cause that node/group to be centered in the related surface.                                                                           |
| collapsible?      | boolean                             | Defaults to true, determines whether or not the miniview can be collapsed.                                                                                                                                    |
| container         | [BrowserElement]()                  | Element to render into. When using a library integration you do not provide this.                                                                                                                             |
| elementFilter?    | (v:[Vertex]()) => boolean           | Optional filter for elements to display. Defaults to undefined - all elements displayed.                                                                                                                      |
| enableWheelZoom?  | boolean                             | Defauts to true, Whether or not to enable the wheel zoom.                                                                                                                                                     |
| showLasso?        | boolean                             | Defaults to true - the miniview will display a lasso as the user is using the lasso in the canvas                                                                                                             |
| suspended?        | boolean                             | Defaults to false. Whether or not to suspend rendering after load.                                                                                                                                            |
| trackSelection?   | boolean                             | Defaults to true - the miniview will add a CSS class to elements whose model object is in the current selection.                                                                                              |
| typeFunction?     | (v:[Node]() \| [Group]()) => string | Optional function to use to derive a type for each rendered node/group. This is written onto the corresponding element as the value of the `data-vjs-miniview-type` attribute, and can be useful for styling. |
| visible?          | boolean                             | Defaults to true. Whether or not the miniview is initially visible.                                                                                                                                           |
| wheelReverse?     | boolean                             | Defaults to false. Whether or not to reverse the zoom direction in response to a wheel event.                                                                                                                 |
| wheelSensitivity? | number                              | Optional override for how sensitive the wheel zoom should be.                                                                                                                                                 |
