OverlayAnimationOptions

Options for animating an overlay along an edge

| Name      | Type                                                        | Description                                                                                    |
| --------- | ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| dwell?    | number                                                      | How long, in milliseconds, to dwell on the source before beginning to move. Defaults to 350ms. |
| events?   | Record\<string,(p:[AnimationEventCallbackParams]()) => any> | Optional set of event listeners.                                                               |
| forwards? | boolean                                                     | Defaults to true, meaning traverse from the source to the target.                              |
| loop?     | boolean                                                     | If true, the animation will loop.                                                              |
| paused?   | boolean                                                     | If true, the animation starts in a paused state.                                               |
| rate?     | number                                                      | Time between frames. Defaults to 30ms.                                                         |
| speed?    | number                                                      | How fast to travel, in pixels per second. Defaults to 100.                                     |
