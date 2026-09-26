# \<SurfaceComponent/>

Provides a pannable and zoomable canvas on which nodes, edges and groups can be drawn, with support for layouts and various plugins.

## Usage[​](#usage "Direct link to Usage")

This component is at the heart of VisuallyJs React, and is very customizable, but there are three main sections of props that you should be familiar with:

* **renderOptions** This prop contains all of the settings that control the behaviour and appearance of the component itself - what layout to use, whether to zoom to fit a dataset when it has been loaded, whether or not to use a grid, plugins, etc...the list is long.

* **viewOptions** This contains the mapping from node/edge/group types to their visual representation and behaviour. For nodes and groups this means mapping some JSX to use to render them; for edges this means specifying details of the connector to use to draw an edge, and how the edge should be anchored. You can also supply event mappings in your `viewOptions` to hook into user interaction with the various parts of the UI

* **modelOptions** This is used less often than `viewOptions` and `renderOptions`, but this is how you can provide settings for the underlying model.

```jsx
<SurfaceComponent 
    className="..."
    data={ ... }
    url=" ... "
    renderOptions={ ... }
    viewOptions={ ... }
    modelOptions={ ... }
/>

```

## Props[​](#props "Direct link to Props")

SurfaceComponentProps

Props for the SurfaceComponent.

| Name           | Type                                              | Description                                                                                                                        |
| -------------- | ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| childProps?    | any                                               | Any props to pass to children.                                                                                                     |
| className?     | string                                            | Optional class name to append to the root element's class list.                                                                    |
| data?          | any                                               | Optional initial data                                                                                                              |
| dataType?      | string                                            | ID of the format that `data` or the data retrieved from `url` is expected to be in. Defaults to `JSON_DATATYPE`.                   |
| model?         | [BrowserUIReactModel]()                           | Optional instance to render. You mostly wont need to do this; the SurfaceComponent or PaperComponent will create<br />an instance. |
| modelOptions?  | [ModelOptions]()                                  | Options for the underlying instance.                                                                                               |
| renderOptions? | [ReactSurfaceRenderOptions]()                     | Render options such as layout, drag options etc                                                                                    |
| selection?     | [VisuallyJsSelection]() \| [SelectionGenerator]() | Optional selection (or selection generator) to render, rather than the entire model.                                               |
| style?         | Record\<string,string>                            | Optional style object to apply to the container element.                                                                           |
| surfaceId?     | string                                            | Optional ID to assign to the surface that is created.                                                                              |
| url?           | string                                            | Optional URL to load initial data from.                                                                                            |
| viewOptions?   | [ReactSurfaceViewOptions]()                       | Mappings of vertex types to components/jsx and edge types.                                                                         |

## Ref Handle[​](#ref-handle "Direct link to Ref Handle")

If you bind this component to a ref, you get an object of type `SurfaceComponentRef`:

SurfaceComponentRef

Reference to a SurfaceComponent. Offers methods to get the underlying surface and VisuallyJs instance.

| Name       | Type                          | Description                                                            |
| ---------- | ----------------------------- | ---------------------------------------------------------------------- |
| getModel   | () => [BrowserUIReactModel]() | Gets the underlying model instance, on which you can manage the model. |
| getSurface | () => [Surface]()             | Gets the Surface canvas component.                                     |
