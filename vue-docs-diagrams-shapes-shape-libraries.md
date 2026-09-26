# SVG Shapes

Diagrams use SVG to render shapes. These shapes are stored inside `ShapeSets`, and when you create a diagram you instruct VisuallyJs which shape sets you want to use.

## Registering shapes[​](#registering-shapes "Direct link to Registering shapes")

```html
<script setup>
import { FLOWCHART_SHAPES, BASIC_SHAPES } from "@visuallyjs/browser-ui"

const options = {
  shapes: [FLOWCHART_SHAPES, BASIC_SHAPES]
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

## Required data[​](#required-data "Direct link to Required data")

In order for the diagram to be able to pick the appropriate shape for some vertex, the vertex data must contain:

1. A `type` property that maps to the ID of one of the shapes in your library
2. A `category` property that maps to some shape set ID
3. A `width` and `height` value for each node. The SVG shapes use `path` elements internally, which require absolute coordinates, and so they need to know the current size of your vertices.
4. An `x` and `y` value for each node

## Optional data[​](#optional-data "Direct link to Optional data")

The full list of optional data properties depends on the shape libraries you are using, but all of the VisuallyJs libraries support these optional properties:

* `fill` - Color to fill the shape with. Defaults to `#FFFFFF`.
* `outline` - Color to outline the shape with. Defaults to `#000000`.
* `outlineWidth` - Width of the shape's outline. Defaults to 2px.
* `color` - Color to use for the shape's label (if shown). Defaults to `#000000`.

As an example, consider this list of two nodes:

```javascript
[
{
    "id":"1",
    "x":50,
    "y":50,
    "type":"process",
    "category":"flowchart",
    "width":100,
    "height":100,
    "fill":"white",
    "outline":"black"
},
{
    "id":"2",
    "x":150,
    "y":250,
    "type":"terminus",
    "category":"flowchart",
    "width":100,
    "height":100,
    "fill":"white",
    "outline":"black"
}
]

```

This is rendered as:

**********

## Cell Template Events[​](#cell-template-events "Direct link to Cell Template Events")

`DiagramOptions.cells.templateEvents` lets you attach delegated event handlers to elements inside rendered shape templates. Keys are CSS selectors, and each selector maps event names to callbacks.

```typescript
renderDiagram(container, {
    cells: {
        templateEvents: {
            ".delete": {
                tap: ({ cell }) => cell.remove()
            },
            ".label": {
                dbltap: ({ cell }) => startEditing(cell)
            }
        }
    }
})

```

You can bind a listener to anything listed as a **BindableViewEvent**:

BindableViewEvent

Events that can be bound in a view.

`EVENT_CLICK | EVENT_DBLCLICK | EVENT_TAP | EVENT_DBLTAP | EVENT_CONTEXTMENU | EVENT_MOUSEDOWN | EVENT_MOUSEOUT | EVENT_MOUSEUP | EVENT_MOUSEOVER | EVENT_MOUSEMOVE`

## Displaying Labels[​](#displaying-labels "Direct link to Displaying Labels")

By default, a diagram will display a `label` value from each node - if we add `label` to the vertices from before we'll see them:

```javascript
[
{
    "id":"1",
     ...,
    "label":"Node 1"
},
{
    "id":"2",
    ...,
    "label":"Node 2"
}
]

```

**********

### Hiding labels[​](#hiding-labels "Direct link to Hiding labels")

You can hide labels by setting `showLabels:false` in your diagram's `edges` options:

```html
<script setup>
import { FLOWCHART_SHAPES, BASIC_SHAPES } from "@visuallyjs/browser-ui"

const options = {
  shapes: [FLOWCHART_SHAPES, BASIC_SHAPES],
  edges: {
    showLabels: false
  }
}
const data = ...
</script>
<template>
  <div class="my-container">
    <DiagramComponent :data="data" :options="options"></DiagramComponent>
  </div>        
</template>

```

***

## Shape properties[​](#shape-properties "Direct link to Shape properties")

A `ShapeType` can define a `properties` array to describe the values its template uses and make those values available in an inspector. Each property has an `id`, `label`, and `type`. The `id` identifies the value in the shape’s model data. The `label` may be shown to the user.

Supported property types are:

* `string` — a single-line text value.
* `text` — a multi-line text value.
* `number` — a numeric value. You can also set `min` and `max`.
* `boolean` — a true or false value.
* `color` — a color value.

Properties can also include a `defaultValue` and a `description`. The default is used when the property has no value in the model; the description can help explain the setting in the inspector.

### Value lists[​](#value-lists "Direct link to Value lists")

`string`, `text` and `number` properties can be declared with a list of possible `values`, for example:

```javascript
{
    id:"pump",
    label:"Pump",
    properties:[
        { 
            id: "pumpType", 
            label: "Type", 
            type: "string",
            template:"....",
            values: ["Centrifugal", "Positive Displacement"], 
            defaultValue: "Centrifugal" 
        }
    ]
}

```

The items in `values` may be strings, as shown above, or they can be a Javascript object containing a label and value, for those use cases where your internal values are not very useful as human readable text:

```javascript
{
    id:"pump",
    label:"Pump",
    properties:[
        { 
            id: "pumpType", 
            label: "Type", 
            type: "string",
            template:"....",
            values: [
                { label:"Centrifugal", value:"c" },
                { label:"Positive Displacement", value:"d" }
            ], 
            defaultValue: "c" 
        }
    ]
}

```

### Default values[​](#default-values "Direct link to Default values")

Any property can declare a `defaultValue`:

```javascript
{
    id:"pump",
    label:"Pump",
    properties:[
        { 
            id: "pumpType", 
            label: "Type", 
            type: "string", 
            template:"....",
            values: ["Centrifugal", "Positive Displacement"], 
            defaultValue: "Centrifugal" 
        }
    ]
}

```

This will be used in the initial payload for an item of this type when it is added to the dataset.

### Read-only properties[​](#read-only-properties "Direct link to Read-only properties")

Set `readOnly: true` to display a property's value without an editable control in the inspector. This only affects the inspector UI: it does not make the model value read-only. Application code and other model operations can still write to that property, and the inspector will display the updated value.

### Choosing controls with `editor`[​](#choosing-controls-with-editor "Direct link to choosing-controls-with-editor")

For `string` and `number` properties, supply a `values` array to present a fixed set of choices instead of a free-form input. Values can be plain strings, or objects with separate `label` and `value` fields when the text shown to the user should differ from the stored value.

Use `editor` to choose how those options are presented:

* `radio` displays radio buttons.
* `select` displays a dropdown.
* If omitted, the integration chooses a control based on the number of options. The framework inspectors show radio buttons for up to seven choices by default, and a dropdown for larger lists. Their `maxRadios` setting can change that threshold.

For a boolean property, `editor: "radio"` or `editor: "select"` replaces the default checkbox with radio buttons or a dropdown. To set the displayed boolean labels, provide a two-item `booleanLabels` tuple. The first label is used for `true`, and the second for `false`; for example:

```javascript
  {
    id: "enabled",
    label: "Enabled",
    type: "boolean",
    editor: "select",
    booleanLabels: ["On", "Off"]
}

```

Without booleanLabels, the framework inspectors use “True” and “False” for boolean radio buttons and dropdowns. With the default checkbox, the property's label is shown beside the control.

## Shape property inspectors[​](#shape-property-inspectors "Direct link to Shape property inspectors")

Each framework integration provides a ShapePropertiesInspector component for rendering the selected shape’s properties. Add it within the integration’s inspector component and pass it the vertex being inspected. The component reads the shape definition from the active shape library and renders the property controls described above.

### React[​](#react "Direct link to React")

Use the ShapePropertiesInspector component exported by the React integration. It accepts a vertex and an optional maxRadios value, which sets how many choices are shown as radio buttons before the inspector switches to a dropdown.

### Vue[​](#vue "Direct link to Vue")

Use the registered ShapePropertiesInspectorComponent within the Vue inspector. It accepts the vertex and an optional maxRadios value, with the same radio- button threshold behavior.

### Svelte[​](#svelte "Direct link to Svelte")

Use the ShapePropertiesInspector component within the Svelte inspector and pass it the vertex. Its optional maxRadios setting controls when a list of choices is rendered as a dropdown instead of radio buttons.

### Angular[​](#angular "Direct link to Angular")

Use the vjs-shape-properties-inspector component within the Angular inspector and bind its vertex input. The optional maxRadios input controls when a list of choices is rendered as a dropdown instead of radio buttons.

### Vanilla JavaScript[​](#vanilla-javascript "Direct link to Vanilla JavaScript")

The vanilla ShapeTypeInspector generates inspector controls from the resolved property definitions. It renders strings, text, numbers, booleans, and colors as standard inputs, and displays readOnly values without editable controls. For font properties, it provides inputs for the font size, family, weight, and style.

The vanilla inspector’s built-in template does not use values, editor, or booleanLabels to render choice controls. If you need those controls in vanilla JavaScript, provide a custom inspector template.

***

## Available sets[​](#available-sets "Direct link to Available sets")

VisuallyJs ships with two shape sets in the `browser-ui` package and a set of BPMN shapes:

### Flowchart[​](#flowchart "Direct link to Flowchart")

```javascript
import { FLOWCHART_SHAPES } from "@visuallyjs/browser-ui"

```

***

### Basic[​](#basic "Direct link to Basic")

```javascript
import { BASIC_SHAPES } from "@visuallyjs/browser-ui"

```

### BPMN[​](#bpmn "Direct link to BPMN")

```javascript
import { BPMN2_SHAPES } from "@visuallyjs/bpmn"

```

info

These shapes are shipped in the `@visuallyjs/bpmn` library - you'll need to import it.

***

## Custom shape sets[​](#custom-shape-sets "Direct link to Custom shape sets")

It's straightforward to make your own shape set - they consist of an id and then a list of shapes, for each of which you provide SVG.

Here we have made a set of faces:

**********

```javascript
const shapes = {
    id:"faces",
    shapes:[
        {
            type:"impassive",
            template:`<g>
<circle cx="{{width/2}}" cy="{{height/2}}" r="{{(width/2)}}"/>
    <path d="M {{width/4}} {{height*3/4}} L {{width*3/4}} {{height*3/4}}"/>
    <circle cx="{{width/4}}" cy="{{height/4}}" r="10"/>
    <circle cx="{{width*3/4}}" cy="{{height/4}}" r="10"/>
    <circle cx="{{width/2}}" cy="{{height/2}}" r="10"/>
    </g>`,
        label:"Impassive"
    },
    {
        type:"pleased",
        template:`<g>
            <circle cx="{{width/2}}" cy="{{height/2}}" r="{{(width/2)}}"/>            
            <circle cx="{{width/4}}" cy="{{height/4}}" r="10"/>
            <circle cx="{{width*3/4}}" cy="{{height/4}}" r="10"/>
            <circle cx="{{width/2}}" cy="{{height/2}}" r="10"/>
            <path d="M {{width/4}} {{height*3/4}} C {{width/4}} {{height*7/8}}, {{width*3/4}} {{height*7/8}} {{width*3/4}} {{height*3/4}}"/>
            </g>`,
        label:"Pleased"
    },
    {
        type:"notpleased",
        template:`<g>
              <circle cx="{{width/2}}" cy="{{height/2}}" r="{{(width/2)}}"/>            
              <circle cx="{{width/4}}" cy="{{height/4}}" r="10"/>
              <circle cx="{{width*3/4}}" cy="{{height/4}}" r="10"/>
              <circle cx="{{width/2}}" cy="{{height/2}}" r="10"/>
              <path d="M {{width/4}} {{height*3/4}} C {{width/4}} {{height*5/8}}, {{width*3/4}} {{height*5/8}} {{width * 0.75}} {{height * 0.75}}"/>
              </g>`,
        label:"Not Pleased"
    }
    ]
}

```

***

## Nested Shape sets[​](#nested-shape-sets "Direct link to Nested Shape sets")

It is possible to nest shape sets, via the `children` property of a shape set. For instance, say we want to split our set of faces into two subsets:

```javascript
const shapes = {
  id:"faces",
  children:[
  {
    id:"expressionless",
    name:"Expressionless",
    shapes:[
      {
        id:"impassive",
        template:`...`
      }
    ]
  },  
  {
    id:"expressions",
    name:"Expressions",
    shapes:[
      {
        id:"pleased",
        template:`...`
      },
      {
        id:"notpleased",
        template:`...`
      }
    ]
  }
  ]
}

```
