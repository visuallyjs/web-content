RotatedRectangle

Represents a rectangle with an optional rotation.

<br />

The rotation is in degrees, and defaults to 0.

<br />

The rotation is assumed to be around the center of the rectangle.

| Name    | Type        | Description                                                                                                                                                         |
| ------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| center? | [PointXY]() | Center of the box. In some cases the code has this information to hand<br />and populates it, but if it is absent you can figure it out from the<br />other values. |
| height  | number      | element height                                                                                                                                                      |
| width   | number      | Element width                                                                                                                                                       |
| x       | number      | X location                                                                                                                                                          |
| y       | number      | Y location                                                                                                                                                          |
