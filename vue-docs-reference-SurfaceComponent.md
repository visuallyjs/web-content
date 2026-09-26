# \<SurfaceComponent/>

Provides a pannable and zoomable canvas on which nodes, edges and groups can be drawn, with support for layouts and various plugins.

## Usage[​](#usage "Direct link to Usage")

This component is at the heart of VisuallyJs Vue, and is very customizable, but there are three main sections of props that you should be familiar with:

* **renderOptions** This prop contains all of the settings that control the behaviour and appearance of the component itself - what layout to use, whether to zoom to fit a dataset when it has been loaded, whether or not to use a grid, plugins, etc...the list is long.

* **viewOptions** This contains the mapping from node/edge/group types to their visual representation and behaviour. For nodes and groups this means mapping a component to use to render them; for edges this means specifying details of the connector to use to draw an edge, and how the edge should be anchored. You can also supply event mappings in your `viewOptions` to hook into user interaction with the various parts of the UI

* **modelOptions** This is used less often than `viewOptions` and `renderOptions`, but this is how you can provide settings for the underlying model.

```html
<script>
    export default {
        data:() => {
            
        }
    } 
</script>
<template>
	<SurfaceComponent :renderOptions="renderOptions"
      :viewOptions="viewOptions"
      :modelOptions="modelOptions"
      :data="this.getData()"
	></SurfaceComponent>    
</template>


```

## Props[​](#props "Direct link to Props")

SurfaceComponentProps

Supported props for the SurfaceComponent.

| Name           | Type              | Description                                                                                                                                                                                              |
| -------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data?          | any               | Optional dataset to load.                                                                                                                                                                                |
| dataType?      | string            | ID of the format that `data` or the data retrieved from `url` is expected to be in. Defaults to `JSON_DATATYPE`.                                                                                         |
| modelOptions?  | [ModelOptions]()  | Options for the underlying model.                                                                                                                                                                        |
| renderOptions? | [RenderOptions]() | Parameters to configure the underlying surface.                                                                                                                                                          |
| surfaceId?     | string            | ID of the surface to attach to. This is optional; Visually JS will use the default surface ID if you do not<br />provide this. For apps where there's only one surface there is no need to provide this. |
| url?           | string            | Optional url for a dataset to load.                                                                                                                                                                      |
| viewOptions?   | [ViewOptions]()   | Mapping of model object types to components and behaviour                                                                                                                                                |
