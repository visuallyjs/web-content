SurfacePopupProps

Props for the SurfacePopup component.

| Name     | Type                                                                               | Description                                                                                                                          |
| -------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| anchor?  | [PopupPosition]()                                                                  | Optional position to place this popup. Defaults to "bottom", and can also be overridden on a per-launcher basis via a DOM attribute. |
| popup    | Snippet<\[[Vertex]() \| null, [BrowserUIModel](), [BrowserUI\<any>](), () => any]> | The snippet that renders the content for the popup.                                                                                  |
| selector | string                                                                             | CSS3 selector identifying elements from which this popup is launched.                                                                |
