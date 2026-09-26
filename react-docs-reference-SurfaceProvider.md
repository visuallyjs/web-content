# \<SurfaceProvider/>

This is a context provider that enables you to use various other components alongside a [SurfaceComponent](/react/docs/reference/SurfaceComponent.md) without having to explicitly connect them up.

## Usage[​](#usage "Direct link to Usage")

```jsx
import { SurfaceProvider, 
    SurfaceComponent, 
    ControlsComponent, 
    MiniviewComponent} from "@visuallyjs/browser-ui-react"

export default function MyApp() {

    return <SurfaceProvider>
        <SurfaceComponent data={...}/>
        <ControlsComponent/>
        <MiniviewComponent/>
    </SurfaceProvider>
    
}

```

In this example, `ControlsComponent` and `MiniviewComponent` can both find the surface to attach to due to them all being contained within the `SurfaceProvider` element.

The list of components that are surface context aware is:

* [Miniview](/react/docs/reference/MiniviewComponent.md)
* [Controls](/react/docs/reference/ControlsComponent.md)
* [ExportControls](/react/docs/reference/ExportControlsComponent.md)
* [Palette](/react/docs/reference/PaletteComponent.md)
* [ShapePalette](/react/docs/reference/ShapePaletteComponent.md)
* [Inspector](/react/docs/reference/InspectorComponent.md)
* [ShapeComponent](/react/docs/reference/ShapeComponent.md)
