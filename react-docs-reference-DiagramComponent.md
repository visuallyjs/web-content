# \<DiagramComponent/>

Provides an SVG diagram component. This is a wrapper around a Surface or Paper, with a few flags set:

* We use an SVG container element
* Every cell is drawn as an SVG element from a ShapeLibrary
* Cell sizes and positions are stored inside the model

A Diagram is a pure SVG UI.

## Usage[​](#usage "Direct link to Usage")

```jsx
import {DiagramComponent} from "@visuallyjs/browser-ui-react";
import {FLOWCHART_SHAPES} from "@visuallyjs/browser-ui";

export default function MyApp() {
    const options = {
        shapes: [FLOWCHART_SHAPES]
    }
    
    const data = {
        nodes:[
            { id:"1", x:50, top:50, width:150, height:100, type:"process" },
            { id:"2", x:250, top:250, width:150, height:100, type:"terminus" }
        ]
    }

    return <DiagramComponent options={options} data={data}/>
}


```

## Props[​](#props "Direct link to Props")

DiagramComponentProps

Props for the DiagramComponent

| Name          | Type                   | Description                                              |
| ------------- | ---------------------- | -------------------------------------------------------- |
| className?    | string                 | Optional class name to set on the container              |
| data?         | any                    | Optional initial data                                    |
| modelOptions? | [ModelOptions]()       | Options for the underlying model                         |
| options?      | [DiagramOptions]()     | Options for the Diagram                                  |
| style?        | Record\<string,string> | Optional style object to apply to the container element. |
| url?          | string                 | Optional URL to load initial data from.                  |

## Ref Handle[​](#ref-handle "Direct link to Ref Handle")

If you bind this component to a ref, you get an object of type `DiagramComponentRef`:

DiagramComponentRef

Handle for a DiagramComponent.

| Name       | Type              | Description                               |
| ---------- | ----------------- | ----------------------------------------- |
| getDiagram | () => [Diagram]() | Gets the underlying Diagram from UI core. |
