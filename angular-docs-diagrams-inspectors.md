# Inspectors

An inspector is a form that can be used to edit the properties of some object, or set of objects, in the VisuallyJs dataset. Inspectors listen to selection events from the underlying model and then draw a suitable UI for editing the selected object(s) based upon the configuration you provide.

In the canvas below we've setup a simple inspector and selected a vertex to begin with. You can edit the various fields in the form on the left. Note that with the text input, changes are persisted on blur and when the enter key is pressed, but for the textarea changes are only persisted on blur.

<!-- -->

**********

## Setup[​](#setup "Direct link to Setup")

Create a class that extends `InspectorComponent` and provide a template with your inspector controls:

```typescript

import {Component} from "@angular/core"
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div>
  @if(currentType === 'type1') {
    <input vjs-att="name" type="text"></input>
  }
    
  @if(currentType === 'type2') {
    <input vjs-att="title" type="text"></input>
  }
</div>`,
    selector:"app-my-inspector"
})
export class MyInspector extends InspectorComponent {}

```

<!-- -->

<!-- -->

We can then use this inspector like this:

```html

<app-main>
<vjs-diagram [options]="options"/>
<app-my-inspector/>
</app-main>

```

`currentType` and `currentObjectType` are two fields set on the class set by the `refresh` method, whose default implementation is:

```typescript
refresh(obj:Base):void {
  this.currentType = obj.data.type
  this.currentObjectType = obj.objectType
}

```

The InspectorComponent is discussed in detail in the reference docs [on this page](/angular/docs/reference/InspectorComponent.md).

## Binding data[​](#binding-data "Direct link to Binding data")

Fields in your data objects are bound to HTML elements via an `vjs-att` attribute. For instance, here's the form we use in the example canvas above:

```html
<input type="text" vjs-att="label">
<textarea vjs-att="description" rows="10" cols="10"></textarea>
<select vjs-att="someNumber">
    <option value="1">1</option>
    <option value="5">5</option>
    <option value="10">10</option>
</select>

```

Each of the `vjs-att` attributes in the HTML above maps to a property in the backing data of the object(s) being inspected:

```javascript
{
  label:"My Object",
  description:"This is my object, with a label and a description and some number",
  someNumber:5
}

```

## Supported input types[​](#supported-input-types "Direct link to Supported input types")

This is the list of supported input types. We show a simple example for each type, but keep in mind you can use all the available attributes on these in your markup - for instance, for a `number` field, perhaps you want to limit the allowed values. Or you could supply a regular expression to a `text` input, etc.

### Text Input[​](#text-input "Direct link to Text Input")

```html
<input type='text' vjs-att="someProperty">

```

### Radio Button[​](#radio-button "Direct link to Radio Button")

```html
<input type='radio' vjs-att="someProperty" value="radioValue" name="someProperty">

```

### Checkbox(es)[​](#checkboxes "Direct link to Checkbox(es)")

```html
<input type='checkbox' vjs-att="someProperty">

```

The inspector supports rendering multiple checkboxes with the same `vjs-att`, for example:

```html
<div class="my-inspector">
  <input type='checkbox' vjs-att="someProperty" value="type1">
  <input type='checkbox' vjs-att="someProperty" value="type2">
</div>

```

You need to be using an array in your data to support this:

```javascript
{
  id:"my-vertex",
  someProperty:["type1", "type2"]
}

```

### Number Input[​](#number-input "Direct link to Number Input")

```html
<input type='number' vjs-att="someProperty">

```

### Textarea[​](#textarea "Direct link to Textarea")

```html
<textarea vjs-att="someProperty" rows="10" cols="5">

```

### Select[​](#select "Direct link to Select")

```html
<select vjs-att="someProperty">
    <option value="someValue">Some Value</option>
    <option value="someOtherValue">Some Other Value</option>
</select>

```

### Color Input[​](#color-input "Direct link to Color Input")

```html
<input type='color' vjs-att="someProperty">

```

### Hidden Input[​](#hidden-input "Direct link to Hidden Input")

```html
<input type='hidden' vjs-att="someProperty" value="someValue">

```

## Non-string datatypes[​](#non-string-datatypes "Direct link to Non-string datatypes")

By default, HTML element values are strings, which may not be ideal for your data model. You can instruct VisuallyJs to cast the value of certain elements to a number, by declaring a `vjs-datatype` attribute in your inspector template:

```html
<div>
    <select vjs-att="threshold" vjs-datatype="integer">
        <option value="5">5</option>
        <option value="10">10</option>
        <option value="15">15</option>
    </select>
</div>

```

In this example, VisuallyJs will attempt to cast the value to an integer. Currently, supported values for `vjs-datatype` are:

* **integer** Cast the value to an integer
* **float** Cast the value to a float, eg 1.5, 2.0, etc.

The `vjs-datatype` attribute is supported on:

* `<select.../>`
* `<input type="radio" .../>`
* `<input type="text" .../>`

note

If you're using an input of type `text` and you want a number, it's probably better to use an input of type `number` - see MDN's discussion [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/number).

## Edge Property Mappings[​](#edge-property-mappings "Direct link to Edge Property Mappings")

[Edge Property Mappings](/angular/docs/diagrams/edges/property-mapping.md) are a means for you to group several pieces of information about an edge's appearance and link them to a named property. If you want to provide your users with a graphical picker to assist them in choosing edge type, include `EdgePropertyMappingsInspector` in your inspector and show it when an edge is selected. It builds its form from the edge property mappings declared on the UI.

```typescript
import { Component } from "@angular/core"
import { InspectorComponent, VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
  imports: [VisuallyJsModule],
  template: `@if (currentObjectType === 'Edge') {
    <vjs-edge-property-mappings />
  }`,
  selector: "app-my-inspector"
})
export class MyInspector extends InspectorComponent {}

```

For a full discussion, see the [Angular reference](/angular/docs/reference/EdgePropertyMappingsInspector.md).

## Shape Properties[​](#shape-properties "Direct link to Shape Properties")

To let users edit a node's shape properties, include `ShapePropertiesInspector` in your inspector and show it when a node is selected. It renders the properties defined by that shape in the active shape library, so pass it the selected vertex.

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

For a full discussion, see the [Angular reference](/angular/docs/reference/ShapePropertiesInspector.md).

## Multiple selections[​](#multiple-selections "Direct link to Multiple selections")

By default, an inspector supports selections containing multiple objects. When multiple objects are being edited, the inspector calculates a set of "common data", ie. the set of keys for which every object in the inspector has a value. For text inputs and text areas, if every value for some given key is the same across all the managed objects, that value is shown and can be edited, resulting in a change to all the managed objects. Otherwise, if not every value is the same, the text input or text area will display a blank value. If the user types in the input field then that change will be propagated to all the managed objects.

To switch off multiple selections you can do this:

```typescript

import {Component} from "@angular/core"
import { VisuallyJsModule } from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div>
  ...
</div>`,
    selector:"app-my-inspector"
})
export class MyInspector extends InspectorComponent {
    constructor() {
        super()
        this.multipleSelections = true
    }
}

```

<!-- -->

note

Diagrams are configured to use a selection mode of \`isolated\` - meaning that although multiple objects can be edited at once, they must all be of the same type. See the [documentation on selections](/angular/docs/apps/model/selections.md) for a discussion of selections.
