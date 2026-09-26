# \<InspectorComponent/>

Provides an object inspector for the nodes/groups/edges in your app. When model objects are added to the model's current selection, the inspector component is informed. You can use any HTML you like in an inspector. VisuallyJs will bind values into inputs on which you have declared a `vjs-att` attribute, for instance:

```html
<input vjs-att="label" type="text"></input>

```

Here, VisuallyJs will populate the given text input with the value of the `label` property in the backing data of whatever is currently selected.

If you have multiple objects selected, VisuallyJs will only populate fields of the inspector where every selected object has the same value for that field. Otherwise the field is initially left blank. Changes are, though, propagated to every selected object.

## Usage[​](#usage "Direct link to Usage")

Create a Svelte component that renders an `InspectorComponent`, and pass it a state variable that VisuallyJs will populate with the current selected object :

```html

<script lang="ts">

import { InspectorComponent } from "@visuallyjs/browser-ui-svelte"
import {Base} from "@visuallyjs/browser-ui";

let current = $state<Base|null>(null)
    
</script>

<InspectorComponent bind:current={current}>

    {#if current?.objectType === 'Node'}
	<div class="node-inspector">
		<div>Text</div>
		<input type="text" vjs-att="text" vjs-focus="true"/>
		<div>Fill</div>
		<input type="color" vjs-att="fill"/>
	</div>
    {/if}    

    {#if current?.objectType === 'Edge'}
	<div class="edge-inspector">
		<div>Label</div>
		<input type="text" vjs-att="label"/>
		<div>Color</div>
		<input type="color" vjs-att="color"/>
	</div>
    {/if}
    
    {#if current == null}
        <h3>Nothing selected</h3>
    {/if}

</InspectorComponent>


```

In our template here we examine the `objectType` from the selected object, which tells us whether it's a `Node`, `Edge`, `Group` or `Port`. Our UI then paints itself accordingly. At the bottom of the template we write out a message if `current` is null.

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

## Props[​](#props "Direct link to Props")

InspectorComponentProps

| Name                | Type                      | Description                                                                                                                                                                            |
| ------------------- | ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| autoCommit?         | boolean                   | Whether or not to auto commit changes on blur or enter keypress. Defaults to true.                                                                                                     |
| className?          | string                    | Optional class name to set on the component's root element.                                                                                                                            |
| current?            | [Base]() \| null          | A $state ref that the inspector will apply 2-way binding to. Since 1.2.0 this is the preferred way to use an inspector, as it reduces the amount of boilerplate you need to configure. |
| filter?             | (obj:[Base]()) => boolean | Optional filter function that you can supply if you want to ignore certain objects in your dataset.                                                                                    |
| multipleSelections? | boolean                   | Whether or not to allow multiple objects to be selected and edited at once.<br />Defaults to false.                                                                                    |
| refresh?            | (obj:[Base]()) => void    | Callback invoked when a new object has started to be edited.                                                                                                                           |
| style?              | string                    | Optional style to set on the component's root element.                                                                                                                                 |
