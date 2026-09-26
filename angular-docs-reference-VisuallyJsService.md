# VisuallyJsService

This service is at the heart of VisuallyJs Angular, providing management of data models and canvases. Every component in VisuallyJs has this service injected, and you can also inject it into your own components in order to access the various methods it offers.

Whether or not you find yourself interacting directly with the VisuallyJs service depends on the complexity of your app.

## Usage[​](#usage "Direct link to Usage")

If you want to access the service in your own components, you need to inject it:

```typescript
import { inject, Component } from "@angular/core"
import { VisuallyJsService } from "@visuallyjs/browser-ui-angular"

@Component({
    selector:"app-my-component",
    template:`<div><marquee>VisuallyJs Service</marquee></div>`
})
export class MyComponent {
    vjsService = inject(VisuallyJsService)
}

```

### Class Methods[​](#class-methods "Direct link to Class Methods")

#### getDiagram[​](#getdiagram "Direct link to getDiagram")

Retrieves the current diagram. If the diagram is not available, the callback will be stored and executed when the diagram becomes available.

Signature

getDiagram(cb:(p:[Diagram]()) => any)

Parameters

|    |                        |                                                                     |
| -- | ---------------------- | ------------------------------------------------------------------- |
| cb | (p:[Diagram]()) => any | A callback function that takes a `Diagram` object as its parameter. |

Return value

void

#### getInspector[​](#getinspector "Direct link to getInspector")

Retrieves the inspector instance. If the inspector is already available, the provided callback function is invoked with the inspector as an argument. If the inspector is not yet ready, the callback is stored in a queue to be executed once the inspector becomes available.

Signature

getInspector(cb:(s:[Inspector]()) => any)

Parameters

|    |                          |                                                                                                    |
| -- | ------------------------ | -------------------------------------------------------------------------------------------------- |
| cb | (s:[Inspector]()) => any | A callback function that receives the inspector instance as an argument when it becomes available. |

Return value

void

#### getModel[​](#getmodel "Direct link to getModel")

Retrieves the model and executes the provided callback function with it. If the model is already available, the callback is executed immediately. Otherwise, the callback is stored to be executed when the model becomes available.

Signature

getModel(cb:(p:[BrowserUIModel]()) => any)

Parameters

|    |                               |                                                  |
| -- | ----------------------------- | ------------------------------------------------ |
| cb | (p:[BrowserUIModel]()) => any | The callback function to execute with the model. |

Return value

void

#### getPaper[​](#getpaper "Direct link to getPaper")

Retrieves the paper object and executes the provided callback function with the paper as an argument. If the paper is not yet available, the callback is stored for execution once the paper becomes available.

Signature

getPaper(cb:(p:[Paper]()) => any)

Parameters

|    |                      |                                                                                    |
| -- | -------------------- | ---------------------------------------------------------------------------------- |
| cb | (p:[Paper]()) => any | A callback function that is called with the retrieved paper object as an argument. |

Return value

void

#### getSurface[​](#getsurface "Direct link to getSurface")

Retrieves the surface and executes the provided callback function with the surface as its argument. If the surface is not available, the callback is stored and will be invoked once the surface is ready.

Signature

getSurface(cb:(s:[Surface]()) => any)

Parameters

|    |                        |                                                                     |
| -- | ---------------------- | ------------------------------------------------------------------- |
| cb | (s:[Surface]()) => any | A callback function that takes a `Surface` object as its parameter. |

Return value

void

#### getUI[​](#getui "Direct link to getUI")

Retrieves the UI element and provides it to the callback function once available. If the UI element already exists, it is immediately passed to the callback. Otherwise, the callback is stored to be executed when the UI becomes available.

Signature

getUI(cb:(b:[BrowserUI]()) => any)

Parameters

|    |                          |                                                                                           |
| -- | ------------------------ | ----------------------------------------------------------------------------------------- |
| cb | (b:[BrowserUI]()) => any | A callback function that receives the UI element `b` of type `BrowserUI` as its argument. |

Return value

void
