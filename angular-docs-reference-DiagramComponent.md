# Diagram

HTML Tag

**vjs-diagram**

Provides an SVG diagram component. This is a wrapper around a Surface or Paper, with a few flags set:

* We use an SVG container element
* Every cell is drawn as an SVG element from a ShapeLibrary
* Cell sizes and positions are stored inside the model

A Diagram is a pure SVG UI.

## Usage[​](#usage "Direct link to Usage")

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name          | Type                              | Description                                                                                                                               |
| ------------- | --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| data          | InputSignal\<Record\<string,any>> | Optional data to load after the view has been initialised. This input is a signal, and will reload the dataset if changed.                |
| modelOptions? | [ModelOptions]()                  | Options for the underlying model                                                                                                          |
| options?      | [DiagramOptions]()                | Options for the Diagram                                                                                                                   |
| url           | InputSignal\<string>              | Optional url from which to load data after the view has been initialised. This input is a signal, and will reload the dataset if changed. |

### Class Members[​](#class-members "Direct link to Class Members")

| Name    | Type        | Description             |
| ------- | ----------- | ----------------------- |
| diagram | [Diagram]() | The underlying Diagram. |
