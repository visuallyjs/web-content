EllipseOverlayOptions

Options for a Ellipse overlay

| Name        | Type                                                    | Description                                                                                                    |
| ----------- | ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| attributes? | Record\<string,string>                                  | Optional custom attributes to write to the overlay's element.                                                  |
| cssClass?   | string                                                  | Optional CSS class(es) to add to the overlay's element.                                                        |
| direction?  | number                                                  | 1 to point forwards (the default), -1 to point backwards. Only taken into consideration in some overlay types. |
| events?     | Record<[OverlayEvents](),(value:any, event:any) => any> | Optional event handlers to attach to the overlay.                                                              |
| hollow?     | boolean                                                 | Defaults to false. When true, the arrow is stroked but not filled.                                             |
| id?         | string                                                  | Optional ID for the overlay. Can be used to retrieve the overlay from a connection.                            |
| location?   | number                                                  | Defaults to 0.5. See docs.                                                                                     |
| paintStyle? | [PaintStyle]()                                          | Optional paint style to use.                                                                                   |
| rx?         | number                                                  | Radius in X. Defaults to 8                                                                                     |
| ry?         | number                                                  | Radius in Y. Defaults to 5                                                                                     |
| visibility? | [OverlayVisibility]()                                   | Whether the overlay is always visible, or only on hover. Defaults to OVERLAY\_VISIBILITY\_ALWAYS.              |
