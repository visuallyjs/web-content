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
