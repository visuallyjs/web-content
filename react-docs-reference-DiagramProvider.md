# \<DiagramProvider/>

This is a context provider that enables you to use various other components alongside a [SurfaceComponent](/react/docs/reference/DiagramComponent.md) without having to explicitly connect them up.

## Usage[​](#usage "Direct link to Usage")

```jsx
import { DiagramProvider, 
    DiagramComponent, 
    ControlsComponent, 
    MiniviewComponent} from "@visuallyjs/browser-ui-react"

export default function MyApp() {

    return <DiagramProvider>
        <DiagramComponent data={...}/>
        <ControlsComponent/>
        <MiniviewComponent/>
    </DiagramProvider>
    
}

```

In this example, `ControlsComponent` and `MiniviewComponent` can both find the surface to attach to due to them all being contained within the `DiagramProvider` element.

The list of components that are diagram context aware is:

* [Miniview](/react/docs/reference/MiniviewComponent.md)
* [Controls](/react/docs/reference/ControlsComponent.md)
* [ExportControls](/react/docs/reference/ExportControlsComponent.md)
* [DiagramPalette](/react/docs/reference/DiagramPaletteComponent.md)
* [Inspector](/react/docs/reference/InspectorComponent.md)
