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
