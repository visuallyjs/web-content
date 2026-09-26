# Inspector

Provides an object inspector for the nodes/groups/edges in your app. When model objects are added to the model's current selection, the inspector component is informed. You can use any HTML you like in an inspector. VisuallyJs will bind values into inputs on which you have declared a `vjs-att` attribute, for instance:

```html
<input vjs-att="label" type="text"></input>

```

Here, VisuallyJs will populate the given text input with the value of the `label` property in the backing data of whatever is currently selected.

If you have multiple objects selected, VisuallyJs will only populate fields of the inspector where every selected object has the same value for that field. Otherwise the field is initially left blank. Changes are, though, propagated to every selected object.

## Usage[​](#usage "Direct link to Usage")

Declare an element to host the inspector component:

```html
<!doctype html>
<html>
  <head>
    <link rel="stylesheet" href="node_modules/@visuallyjs/browser-ui/css/visuallyjs.css">
  </head>
  <body>
    <div id="myContainer"></div>
    <div id="myInspector"></div>
  </body>
</html>

```

<!-- -->

<!-- -->

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

## Creating a VanillaInspector[​](#creating-a-vanillainspector "Direct link to Creating a VanillaInspector")

The `VanillaInspector`'s constructor is:

```typescript
constructor(someDomElement:HTMLElement, options:VanillaInspectorOptions)

```

These are the available options:

VanillaInspectorOptions

Options for the VanillaInspector, an instance of Inspector that uses VisuallyJs's default templating mechanism to render elements.

| Name                      | Type                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| afterUpdate?              | () => any                             | Optional callback to invoke after an update has occurred.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| autoCommit?               | boolean                               | Whether or not to auto commit changes on blur/change events. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| cacheTemplates?           | boolean                               | By default the inspector will cache found templates, keyed by the type of the object and its category (there is a separate cache for nodes, groups, edges and ports, and in each cache the key is the object's `type`). In some situations you may not want to cache the template, for instance if your template has dynamic data that depends on the object that is being inspected. If that's the case you can set this to false.                                                                                                                                                                                                                 |
| container                 | HTMLElement                           | The element into which the inspector is drawn.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| context?                  | Record\<string,any>                   | Optional context to also provide to the templates when rendering. This can be accessed via the `$context` prefix, for<br />instance `{{$context.myValue}}`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| cssClass?                 | string                                | Optional css class(es) to set on the inspector - a space separated list.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| doNotWriteBlankNewValues? | boolean                               | Defaults to true. With this setting, if an update is made that has one or more blank strings, the strings will only be written to objects that already had some value for the corresponding key. If some object has, say, no value stored against the key `foo`, then the inspector will not write a value of "" for that key into the vertex. The reasoning for this flag is that you cannot get a null value from a text field, so if some text field has no value written in it and then gets a blur event, the UI reports a value of "", ie an empty string. But this is likely not the user's intention, if the field was blank to begin with. |
| emptyTemplate?            | string                                | Template to use in the inspector when there is nothing selected. By default an empty `div` element is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| filter?                   | (b:[Base]()) => boolean               | Optional filter you can use to instruct the inspector to ignore certain items.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| getDefaultValue?          | (d:[ObjectData](), key:string) => any | Optional callback used to retrieve a value for a specific property when it's not present in the object's data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| multipleSelections?       | boolean                               | Whether or not to support multiple selections. Defaults to true.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| showCloseButton?          | boolean                               | Defaults to false. When true, the inspector will have a close button in the top right corner, which, when pressed, will<br />clear the Toolkit's selection.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| templateResolver          | (obj:[Base]()) => string              | Resolves templates for a given object.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ui                        | [BrowserUI]()                         | The UI to attach to.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
