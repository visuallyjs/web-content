JsxWrapperProps

These are the props that are passed to the `jsx` you provide to map a node, group or overlay component in the `viewOptions` of a SurfaceComponent or PaperComponent. VisuallyJs passes in the UI, the model (which you can get from the UI anyway), the object being rendered, the object's data, and any `childProps` that have been configured.

| Name   | Type               | Description                                                                                           |
| ------ | ------------------ | ----------------------------------------------------------------------------------------------------- |
| data   | [ObjectData]()     | The object's backing data                                                                             |
| model  | [BrowserUIModel]() | Underlying model. Can also be accessed via `ui.model`.                                                |
| obj    | T                  | The object to be rendered - a Node, Group or Edge.                                                    |
| props  | any                | Any extra props configured by the view to present to this JSX.                                        |
| ui     | [BrowserUI]()      | The UI that is rendering this object.                                                                 |
| vertex | T                  | The object to be rendered - a Node, Group or Edge. Use this in preference to `obj` from 1.2.0 onwards |
