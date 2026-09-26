PaperComponentProps

Props for the PaperComponent.

| Name           | Type                        | Description                                                                                                                   |
| -------------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| childProps?    | any                         | Any props to pass to children.                                                                                                |
| className?     | string                      | Optional class name to append to the root element's class list.                                                               |
| data?          | any                         | Optional initial data                                                                                                         |
| dataType?      | string                      | ID of the format that `data` or the data retrieved from `url` is expected to be in. Defaults to `JSON_DATATYPE`.              |
| model?         | [BrowserUIReactModel]()     | Optional instance to render. You mostly wont need to do this; the SurfaceComponent or PaperComponent will create an instance. |
| modelOptions?  | [ModelOptions]()            | Options for the underlying instance.                                                                                          |
| paperId?       | string                      | Optional ID to assign to the Paper that is created.                                                                           |
| renderOptions? | [ReactPaperRenderOptions]() | Render options such as layout, drag options etc                                                                               |
| style?         | Record\<string,string>      | Optional style object to apply to the container element.                                                                      |
| url?           | string                      | Optional URL to load initial data from.                                                                                       |
| viewOptions?   | [ReactPaperViewOptions]()   | Mappings of vertex types to components/jsx and edge types.                                                                    |
