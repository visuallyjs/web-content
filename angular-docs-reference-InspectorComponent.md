# Inspector

Provides an object inspector for the nodes/groups/edges in your app. When model objects are added to the model's current selection, the inspector component is informed. You can use any HTML you like in an inspector. VisuallyJs will bind values into inputs on which you have declared a `vjs-att` attribute, for instance:

```html
<input vjs-att="label" type="text"></input>

```

Here, VisuallyJs will populate the given text input with the value of the `label` property in the backing data of whatever is currently selected.

If you have multiple objects selected, VisuallyJs will only populate fields of the inspector where every selected object has the same value for that field. Otherwise the field is initially left blank. Changes are, though, propagated to every selected object.

## Usage[​](#usage "Direct link to Usage")

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

`currentType` and `currentObjectType` are two fields set on the class set by the `refresh` method, whose default implementation is:

```typescript
refresh(obj:Base):void {
  this.currentType = obj.data.type
  this.currentObjectType = obj.objectType
}

```

## Data Binding[​](#data-binding "Direct link to Data Binding")

### Supported elements[​](#supported-elements "Direct link to Supported elements")

Elements on which the inspector will perform data binding are:

* **select** Drop down boxes, including those with `multiple:true`
* **textarea** For long pieces of text
* **input** Various input types are supported.

### Supported input types[​](#supported-input-types "Direct link to Supported input types")

* **checkbox** Note: the inspector will peform a ["truthy" match](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) to determine whether or not a checkbox should be checked
* **radio** Note: As radio buttons are represented with strings in HTML, you can provide a `vjs-datatype` attribute to instruct VisuallyJs that you wish to coerce its value to a number. [Read more here](#radio-button-datatypes)
* **color** Note: your data model must be using rgb or hex to represent colors
* **number**
* **range**
* **text**

### Validation[​](#validation "Direct link to Validation")

As the inspector is represented using standard HTML, you can take advantage of all of the validation attributes that are available in HTML 5 elements.

### Radio Button Datatypes[​](#radio-button-datatypes "Direct link to Radio Button Datatypes")

To tell VisuallyJs to coerce the value a given radio button represents to a number, write out a `vjs-datatype` attribute on it:

```html
<input type="radio" vjs-att="foo" value="5" vjs-datatype="integer"/>

```

Valid values are `"integer"` and `"float"`.

## Setting focus[​](#setting-focus "Direct link to Setting focus")

If you wish to specify a field that should receive the focus whenever the UI is updated, use `vjs-focus`:

```html
<input type="text" vjs-att="label" vjs-focus="true"/>

```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name             | Type                | Description                                                              |
| ---------------- | ------------------- | ------------------------------------------------------------------------ |
| context?         | Record\<string,any> | Optional context for shared data for inspector templates.                |
| cssClass?        | string              | Optional css class(es) to set on the inspector - a space separated list. |
| showCloseButton? | boolean             | Whether or not to show a close button. Defaults to false.                |

### Class Members[​](#class-members "Direct link to Class Members")

| Name              | Type   | Description                                                                                                                 |
| ----------------- | ------ | --------------------------------------------------------------------------------------------------------------------------- |
| currentObj        | T      | The object that is currently being inspected.                                                                               |
| currentObjectType | string | The `objectType` of the current object - `Group`, `Node`, `Edge` or `Port`                                                  |
| currentType       | string | By default, this is the `type` of the current object. You can override `refresh` to implement more sophisticated scenarios. |
| EDGE              | string | Edge.objectType is exposed on the class for reference in the template.                                                      |
| GROUP             | string | Group.objectType is exposed on the class for reference in the template.                                                     |
| NODE              | string | Node.objectType is exposed on the class for reference in the template.                                                      |
| PORT              | string | Port.objectType is exposed on the class for reference in the template.                                                      |
