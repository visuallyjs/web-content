# \<DiagramComponent/>

Provides an SVG diagram component. This is a wrapper around a Surface or Paper, with a few flags set:

* We use an SVG container element
* Every cell is drawn as an SVG element from a ShapeLibrary
* Cell sizes and positions are stored inside the model

A Diagram is a pure SVG UI.

## Usage[​](#usage "Direct link to Usage")

```html
<script>
  export default {
    data:() => {
      data:{ ... },
      options:{ ... } 
    }
  } 
</script>
<template>
  <DiagramComponent :options="options" :data="data"/>    
</template>


```

## Props[​](#props "Direct link to Props")

DiagramComponentProps

| Name          | Type               | Description                                                                                                                            |
| ------------- | ------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| data?         | any                | Optional initial data to load                                                                                                          |
| diagramId?    | string             | Optional ID to assign to the Diagram so you can reference it elsewhere in the UI. It is preferable, though, to use providers for this. |
| modelOptions? | [ModelOptions]()   | Options for the underlying model.                                                                                                      |
| options       | [DiagramOptions]() | Options for the Diagram.                                                                                                               |
| url?          | string             | Optional URL from which to load data                                                                                                   |
