### BrowserUISvelteModel

Extension of VisuallyJsModel suitable for use with the Svelte integration.

### Class Methods[​](#class-methods "Direct link to Class Methods")

#### render[​](#render "Direct link to render")

Configures the given element as a Surface, registering it so that it reflects any changes to the underlying data. If there is any data in the model at the time of this call it is rendered; any data subsequently loaded is automatically rendered. You can supply layout arguments to this method (layout type + layout specific parameters), as well as rules for paint styles etc.

Signature

render(container:[BrowserElement](), options:[BrowserUIOptions<]()[BrowserUIDefaults]()>, templateRenderer:TemplateRenderer\<any>)

Parameters

|                  |                                             |                            |
| ---------------- | ------------------------------------------- | -------------------------- |
| container        | [BrowserElement]()                          | The Element to render into |
| options          | [BrowserUIOptions<]()[BrowserUIDefaults]()> | Render options             |
| templateRenderer | TemplateRenderer\<any>                      |                            |

Return value

any
