# Selected edge highlighter

This plugin provides a visual indicator for edges when they are selected in a Diagram. It draws a bounding box (highlight) around the selected edge, making it easier for users to identify which edge is currently being interacted with.

<!-- -->

**********

This plugin is **switched on by default** in any `Diagram` instance.

## Features[​](#features "Direct link to Features")

* Automatically draws a highlight when an edge is selected.
* Updates the highlight position and size in real-time if the edge's geometry changes (e.g., when moving connected vertices or editing the edge path).
* Removes the highlight when the edge is deselected or removed from the diagram.

## Configuration[​](#configuration "Direct link to Configuration")

While the plugin is active by default, you can configure its behavior or disable it entirely via the `edges` section of your `DiagramOptions`.

## Disabling the Plugin[​](#disabling-the-plugin "Direct link to Disabling the Plugin")

To disable the edge highlight, set `highlightSelected` to `false`:

```jsx
import { FLOWCHART_SHAPES } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  shapes: FLOWCHART_SHAPES,
  edges: {
    highlightSelected: false
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

## Customizing the Highlight Style[​](#customizing-the-highlight-style "Direct link to Customizing the Highlight Style")

You can customize the appearance of the highlight box using the `highlightStyle` option. This option accepts a [PaintStyle]() object.

**********

```jsx
import { FLOWCHART_SHAPES } from "@visuallyjs/browser-ui"
import { DiagramComponent } from "@visuallyjs/browser-ui-react"
import "@visuallyjs/browser-ui/css/visuallyjs.css";

export default function App() {
    
  const data = ...
    
  const options = {
  shapes: FLOWCHART_SHAPES,
  edges: {
    highlightStyle: {
      stroke: "blue",
      strokeWidth: 3,
      fill: "rgba(0, 0, 255, 0.1)",
      dashArray: "5 5"
    }
  }
}
    
  return <div style={{width:"100%", height:"500px"}}>
    <DiagramComponent data={data} options={options}/>
  </div>    
}

```

The `highlightStyle` supports the following properties:

PaintStyle

Basic style definition for an edge

| Name           | Type                     | Description                                                               |
| -------------- | ------------------------ | ------------------------------------------------------------------------- |
| dashArray?     | string                   | Definition for stroke pattern                                             |
| fill?          | string                   | Fill color for the edge.                                                  |
| gradient?      | Array<\[number, string]> | Definition of a linear gradient to apply. Each entry is \[offset, color]. |
| outlineStroke? | string                   | Color for the outline path                                                |
| outlineWidth?  | number                   | Width of the outline path                                                 |
| stroke?        | string                   | Stroke color for the edge                                                 |
| strokeWidth?   | number                   | Width of the stroke                                                       |

## CSS Customization[​](#css-customization "Direct link to CSS Customization")

The highlight element is an SVG `rect` and is assigned the CSS class `vjs-selected-edge-highlight`. You can also use this class to apply additional styles via CSS, though `highlightStyle` in options is the preferred method for basic styling.
