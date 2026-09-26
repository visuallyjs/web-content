ViewportBounds

Models the current bounds of a viewport, containing its x/y location,

<br />

width/height and current zoom.

| Name        | Type   | Description                                                                                                                                                                                                                                                                                             |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| height      | number | Height of the content displayed in the viewport                                                                                                                                                                                                                                                         |
| minimumFill | number | The content in each axis fills the viewport at some ratio to the viewport size in that axis. This field provides the smaller of those two ratios. The axis it pertains to is not specified. The inverse of this value gives you the zoom level that would allow all the content to fit in the viewport. |
| vh          | number | The height of the viewport element.                                                                                                                                                                                                                                                                     |
| vw          | number | The width of the viewport element.                                                                                                                                                                                                                                                                      |
| width       | number | Width of the content displayed in the viewport                                                                                                                                                                                                                                                          |
| x           | number | Minimum value in X of the content displayed in the viewport                                                                                                                                                                                                                                             |
| y           | number | Minimum value in Y of the content displayed in the viewport                                                                                                                                                                                                                                             |
| zoom        | number | The current zoom level applied in the viewport.                                                                                                                                                                                                                                                         |
