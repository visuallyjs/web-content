### BrowserUIAngularModel

Extension of the VisuallyJsModel for use in Angular. You'll rarely need to create one of these manually, but this is the class of the `model` exposed in several UI components.

### Class Methods[​](#class-methods "Direct link to Class Methods")

#### render[​](#render "Direct link to render")

Configures the given element as a Surface, registering it so that it reflects any changes to the underlying data. If there is any data in the model at the time of this call it is rendered; any data subsequently loaded is automatically rendered. You can supply layout arguments to this method (layout type + layout specific parameters), as well as rules for paint styles etc.

Signature

render(container:Element, options:[SurfaceOptions]())

Parameters

|           |                    |                            |
| --------- | ------------------ | -------------------------- |
| container | Element            | The Element to render into |
| options   | [SurfaceOptions]() | Render options             |

Return value

[Surface]()
