# \<SurfaceComponent/>

Provides a pannable and zoomable canvas on which nodes, edges and groups can be drawn, with support for layouts and various plugins.

## Usage[​](#usage "Direct link to Usage")

This component is at the heart of VisuallyJs Svelte, and is very customizable, but there are three main sections of props that you should be familiar with:

* **renderOptions** This prop contains all of the settings that control the behaviour and appearance of the component itself - what layout to use, whether to zoom to fit a dataset when it has been loaded, whether or not to use a grid, plugins, etc.

* **viewOptions** This contains the mapping from node/edge/group types to their visual representation and behaviour. For nodes and groups this means mapping a component to use to render them; for edges this means specifying details of the connector to use to draw an edge, and how the edge should be anchored. You can also supply event mappings in your `viewOptions` to hook into user interaction with the various parts of the UI.

* **modelOptions** This is used less often than `viewOptions` and `renderOptions`, but this is how you can provide settings for the underlying model.

```html
<script>
    
import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
    
const renderOptions = { ... }
const viewOptions = {
  nodes:{
    default:{
      component:MyNodeComponent
    }
  }
}
const modelOptions = {...} 
const data = { ... }
    
</script>

<SurfaceComponent renderOptions={renderOptions}
  viewOptions={viewOptions}
  modelOptions={modelOptions}
  data={data}>
</SurfaceComponent>


```

## Props[​](#props "Direct link to Props")

SurfaceComponentProps

| Name             | Type                                  | Description                                                                                                                                                                                                                                                                                          |
| ---------------- | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| additionalProps? | Array\<Record\<string,any>>           | An optional array of reactive objects. The properties from these objects will be<br />merged into the props passed to each WrapperComponent, preserving reactivity.                                                                                                                                  |
| className?       | string                                | Optional class name to set on the surface component's container                                                                                                                                                                                                                                      |
| data?            | any                                   | Optional data to load after the component has been mounted.                                                                                                                                                                                                                                          |
| dataType?        | string                                | ID of the format that `data` or the data retrieved from `url` is expected to be in. Defaults to `JSON_DATATYPE`.                                                                                                                                                                                     |
| injector?        | (v:[Vertex]()) => Record\<string,any> | Optional function that is used to generate a set of props for a given vertex before rendering it. This provides a mechanism for you to inject specific items into the components you use to render your vertices. The return value of this function should be `Record<string, any>`. It may be null. |
| model?           | [BrowserUIModel]()                    | Optional Visually JS instance to use. If this is not provided, a Visually JS instance will be created, with `modelOptions` if you provide them.                                                                                                                                                      |
| modelOptions?    | [ModelOptions]()                      | Options for the underlying model instance.                                                                                                                                                                                                                                                           |
| renderOptions?   | [SvelteSurfaceRenderOptions]()        | Render options for the Surface.                                                                                                                                                                                                                                                                      |
| shapeLibrary?    | [ShapeLibraryImpl<]()[ObjectData]()>  | Shape library to use to render SVG shapes. Optional.                                                                                                                                                                                                                                                 |
| url?             | string                                | Optional url from which to load data after the component has been mounted. If you provide this and also data, this will take precedence.                                                                                                                                                             |
| viewOptions?     | [SvelteSurfaceViewOptions]()          | View options for the Surface.                                                                                                                                                                                                                                                                        |
