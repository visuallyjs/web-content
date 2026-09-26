PanOptions

Options to control how a user pans the canvas.

| Name        | Type                    | Description                                                                                                                                                                                        |
| ----------- | ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| axis?       | [PanAxis]()             | Optional axes in which to constrain pan - 'x', 'y' or 'both'. Defaults to 'both'.                                                                                                                  |
| enabled?    | boolean                 | Defaults to true, meaning panning is enabled.                                                                                                                                                      |
| filter?     | (el:Element) => boolean | Optional function which is called at the start of panning and can return false to reject pan starting.                                                                                             |
| useMetaKey? | boolean                 | Optional, defaults to false. When true, the user must hold down the meta key (ctrl on windows) in order to pan.                                                                                    |
| wheel?      | boolean                 | Defaults to false, meaning panning works via canvas drag. If you set this to true, the mousewheel (or move events on a touchpad) will pan the canvas. This will also override any zoom wheel flag. |
