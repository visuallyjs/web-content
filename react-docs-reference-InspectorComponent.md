# \<InspectorComponent/>

Provides an object inspector for the nodes/groups/edges in your app. When model objects are added to the model's current selection, the inspector component is informed. You can use any HTML you like in an inspector. VisuallyJs will bind values into inputs on which you have declared a `vjs-att` attribute, for instance:

```html
<input vjs-att="label" type="text"></input>

```

Here, VisuallyJs will populate the given text input with the value of the `label` property in the backing data of whatever is currently selected.

If you have multiple objects selected, VisuallyJs will only populate fields of the inspector where every selected object has the same value for that field. Otherwise the field is initially left blank. Changes are, though, propagated to every selected object.

## Usage[​](#usage "Direct link to Usage")

Create a React component that renders an `InspectorComponent`, and pass a function to its body that renders content based on the current selected object.

```jsx

import { useState } from "react"
import { InspectorComponent} from "@visuallyjs/browser-ui-react"
import { Node, Edge } from "@visuallyjs/browser-ui"

export default function MyInspectorComponent(props) {

    return <InspectorComponent>

        {(current) => {

            { current.objectType === Node.objectType &&
            <div className="node-inspector">
                <div>Text</div>
                <input type="text" vjs-att="text" vjs-focus="true"/>
                <div>Fill</div>
                <input type="color" vjs-att="fill"/>
            </div>
            }

            { current.objectType === Edge.objectType &&
            <div className="edge-inspector">
                <div>Label</div>
                <input type="text" vjs-att="label"/>
                <div>Color</div>
                <input type="color" vjs-att="color"/>
            </div>
            }
            
        }}

    </InspectorComponent>
}
    

```

## Empty inspector[​](#empty-inspector "Direct link to Empty inspector")

To render something when the inspector has no current selection, pass a function to the `renderEmptyContent` prop:

```jsx

import { useState } from "react"
import { InspectorComponent} from "@visuallyjs/browser-ui-react"
import { Node, Edge } from "@visuallyjs/browser-ui"

export default function MyInspectorComponent(props) {

    function nothingSelected() {
        return <h3>Select a node to inspect its properties</h3>
    }
    
    return <InspectorComponent renderEmptyContent={nothingSelected}>

        {(current) => {
            ...
        }}

    </InspectorComponent>
}
    

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

## Props[​](#props "Direct link to Props")

InspectorComponentProps

Props for the InspectorComponent

| Name                | Type                      | Description                                                                                                                                                                                           |
| ------------------- | ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| afterUpdate?        | (s:[BrowserUI]()) => void | Optional function to invoke after an update.                                                                                                                                                          |
| autoCommit?         | boolean                   | Whether or not to auto commit on enter keypress/blur. Defaults to true.                                                                                                                               |
| className?          | string                    | Optional extra css classes to set on the root element                                                                                                                                                 |
| filter?             | (b:[Base]()) => boolean   | Optional filter you can use to instruct the inspector to ignore certain items.                                                                                                                        |
| multipleSelections? | boolean                   | Whether or not to support multiple selections. Defaults to true.                                                                                                                                      |
| refresh?            | (obj:[Base]()) => void    | Callback invoked when a new object has started to be edited. You need to provide this if the child content you provide to the Inspector is not a function.                                            |
| renderEmptyContent? | () => any                 | Optional function that returns JSX to use when nothing is selected                                                                                                                                    |
| showCloseButton?    | boolean                   | Whether or not to show a close button. Defaults to false.                                                                                                                                             |
| surface?            | [Surface]()               | Surface to attach to. It is not mandatory that you supply this - the component is context aware and can try to resolve a surface from an ancestor SurfaceProvider SurfaceComponent or PaperComponent. |
