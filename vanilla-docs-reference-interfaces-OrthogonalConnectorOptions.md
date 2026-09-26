OrthogonalConnectorOptions

Options for an orthogonal connector.

| Name                | Type    | Description                                                                                                                           |
| ------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| alwaysRespectStubs? | boolean | Defaults to true, meaning always draw a stub of the desired length, even when the source and target elements are very close together. |
| cornerRadius?       | number  | Optional curvature of the corners in the connector. Defaults to 0.                                                                    |
| cssClass?           | string  | Optional class to set on the element used to render the connector.                                                                    |
| gap?                | number  | Defines a number of pixels between the end of the connector and its anchor point. Defaults to zero.                                   |
| hoverClass?         | string  | Optional class to set on the element used to render the connector when the mouse is hovering over the connector.                      |
| loopbackRadius?     | number  | For a loopback connection, the size of the loop.                                                                                      |
| midpoint?           | number  | The point to use as the halfway point between the source and target. Defaults to 0.5.                                                 |
| slightlyWonky?      | boolean | If true, and a cornerRadius is set, the lines are drawn in such a way that they look slightly hand drawn.                             |
| stub?               | number  | Stub defines a number of pixels that the connector travels away from its element before the connector's actual path begins.           |
