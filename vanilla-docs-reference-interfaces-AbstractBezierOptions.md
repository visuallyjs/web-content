AbstractBezierOptions

Base options interface for Quadratic and Cubic Bezier connectors.

| Name              | Type   | Description                                                                                                                                                           |
| ----------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| cssClass?         | string | Optional class to set on the element used to render the connector.                                                                                                    |
| gap?              | number | Defines a number of pixels between the end of the connector and its anchor point. Defaults to zero.                                                                   |
| hoverClass?       | string | Optional class to set on the element used to render the connector when the mouse is hovering over the connector.                                                      |
| loopbackDistance? | number | When the connector's source and target is the same vertex, this is a measure of how far the control point will<br />be placed from the element. Defaults to 62 pixels |
| stub?             | number | Stub defines a number of pixels that the connector travels away from its element before the connector's actual path begins.                                           |
