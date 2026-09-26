PaperComponentProps

Supported props for the PaperComponent.

| Name           | Type              | Description                                                                                                                                                                                        |
| -------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data?          | any               | Optional dataset to load.                                                                                                                                                                          |
| dataType?      | string            | ID of the format that `data` or the data retrieved from `url` is expected to be in. Defaults to `JSON_DATATYPE`.                                                                                   |
| modelOptions?  | [ModelOptions]()  | Options for the underlying model.                                                                                                                                                                  |
| paperId?       | string            | ID of the paper to attach to. This is optional; Visually JS will use the default paper ID if you do not<br />provide this. For apps where there's only one paper there is no need to provide this. |
| renderOptions? | [RenderOptions]() | Parameters to configure the underlying paper.                                                                                                                                                      |
| url?           | string            | Optional url for a dataset to load.                                                                                                                                                                |
| viewOptions?   | [ViewOptions]()   | Mapping of model object types to components and behaviour                                                                                                                                          |
