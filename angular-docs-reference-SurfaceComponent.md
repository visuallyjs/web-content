# Surface

HTML Tag

**vjs-surface**

Provides a pannable and zoomable canvas on which nodes, edges and groups can be drawn, with support for layouts and various plugins.

## Usage[​](#usage "Direct link to Usage")

This component is at the heart of VisuallyJs Angular, and is very customizable. There are three main sections of inputs that you should be familiar with:

* **renderOptions** This input contains all of the settings that control the behaviour and appearance of the component itself - what layout to use, whether to zoom to fit a dataset when it has been loaded, whether or not to use a grid, plugins, etc...the list is long.

* **viewOptions** This contains the mapping from node/edge/group types to their visual representation and behaviour. For nodes and groups this means mapping a component to use to render them; for edges this means specifying details of the connector to use to draw an edge, and how the edge should be anchored. You can also supply event mappings in your `viewOptions` to hook into user interaction with the various parts of the UI

* **modelOptions** This is used less often than `viewOptions` and `renderOptions`, but this is how you can provide settings for the underlying model.

```typescript

import { MyComponent } from './components/my.component'
import { SurfaceComponent } from "@visuallyjs/browser-ui-angular"

@Component({
    template:`<div>
        <vjs-surface [renderOptions]="renderOptions" 
                          [data]="data"
                          [viewOptions]="viewOptions" 
        />
        </div>`
})
export class MyApp {
    renderOptions = { ... }
    data = { ... }
    viewOptions={ 
        nodes:{
            default:{
                component:MyComponent
            }
        }
    }
    
}


```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name           | Type                              | Description                                                                                                                                                                |
| -------------- | --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data           | InputSignal\<Record\<string,any>> | Optional data to load after the view has been initialised. This input is a signal, and will reload the dataset if changed.                                                 |
| dataType?      | string                            | ID of the format that `data` or the data retrieved from `url` is expected to be in. Defaults to `JSON_DATATYPE`.                                                           |
| modelOptions?  | [ModelOptions]()                  | Optional parameters for the underlying model instance. These will be used only if the model instance with the given ID has not yet been created somewhere else in the app. |
| renderOptions? | [AngularRenderOptions]()          | Options for the underlying surface widget.                                                                                                                                 |
| url            | InputSignal\<string>              | Optional url from which to load data after the view has been initialised. This input is a signal, and will reload the dataset if changed.                                  |
| viewOptions?   | [AngularViewOptions]()            | Options for the view - mappings of components and behaviour to model object types.                                                                                         |

### Class Members[​](#class-members "Direct link to Class Members")

| Name                                  | Type                | Description                                                                                               |
| ------------------------------------- | ------------------- | --------------------------------------------------------------------------------------------------------- |
| model                                 | [BrowserUIModel]()  | The underlying model.                                                                                     |
| surface                               | [Surface]()         | The Surface from the UI core package that this component manages.                                         |
| exportData(options:[ExportOptions]()) | [SurfaceSaveData]() | Export the dataset only                                                                                   |
| save(options:[SaveOptions]())         | void                | Save the dataset and the surface's current pan/zoom, as well as any inspector context, via POST to a URL. |

### Outputs[​](#outputs "Direct link to Outputs")

| Name        | Type                                                                                                                          | Description                                                       |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| vertexEvent | EventEmitter<{<br />  component:ComponentRef\<any>,<br />  event:string,<br />  payload:any,<br />  vertex:[Vertex]()<br />}> | Output event emitter, for proxying events from vertex components. |
