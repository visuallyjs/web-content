BackgroundComponentProps

Props for the background component. `type` defines the type of background to render, and each background type has its own set of options.

| Name               | Type                          | Description                                                                           |
| ------------------ | ----------------------------- | ------------------------------------------------------------------------------------- |
| onBackgroundReady? | [OnBackgroundReadyCallback]() | Optional function to call when the image has loaded (or otherwise claims to be ready) |
| type               | string                        | Type of background to render.                                                         |
| visible?           | boolean                       | Whether or not the background should initially be visible. Defaults to true.          |
