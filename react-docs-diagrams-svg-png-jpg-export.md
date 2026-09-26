# SVG, PNG and JPG export

To export SVG, PNG or JPG from a diagram there are two approaches available to you - use VisuallyJs's export helper UI, or use the low level programmatic API.

## Export helper UI[​](#export-helper-ui "Direct link to Export helper UI")

The export helper UI provides a simple interface to allow your users to export the contents of a surface to an SVG file.

**********

Export SVGExport PNGExport JPG

### SVG Export[​](#svg-export "Direct link to SVG Export")

The code to invoke the SVG exporter UI is:

```jsx

import React, { useRef } from "react"
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import { SVGExporterUI } from "@visuallyjs/browser-ui"

export default function MyComponent() {
    const surfaceRef = useRef(null)
    
    const exportToSvg = () => {
        // create an exporter and invoke the export method on it
        new SVGExporterUI(surfaceRef.current.surface).export()    
    }
    
    return <div>
        <SurfaceComponent ref={surfaceRef}/>
        <button onClick={() => exportToSvg()}>Export SVG</button>
        </div>
}


```

There are a number of options you can pass in to the export method - they are defined in the [SvgExportOptions]() interface.

### PNG Export[​](#png-export "Direct link to PNG Export")

You can export to PNG with this code:

```jsx

import React, { useRef } from "react"
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import { ImageExporterUI } from "@visuallyjs/browser-ui"

export default function MyComponent() {
    const surfaceRef = useRef(null)
    
    const exportToPng = () => {
        // create an exporter and invoke the export method on it
        new ImageExporterUI(surfaceRef.current.surface).export()    
    }
    
    return <div>
        <SurfaceComponent ref={surfaceRef}/>
        <button onClick={() => exportToPng()}>Export PNG</button>
        </div>
}


```

There are a number of options you can pass in to the export method - they are defined in the [ImageExportOptions]() interface.

### JPG Export[​](#jpg-export "Direct link to JPG Export")

You can export to JPG with this code:

```jsx

import React, { useRef } from "react"
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import { ImageExporterUI } from "@visuallyjs/browser-ui"

export default function MyComponent() {
    const surfaceRef = useRef(null)
    
    const exportToJpg = () => {
        // create an exporter and invoke the export method on it
        new ImageExporterUI(surfaceRef.current.surface).export({type:"image/jpeg"})    
    }
    
    return <div>
        <SurfaceComponent ref={surfaceRef}/>
        <button onClick={() => exportToJpg()}>Export JPG</button>
        </div>
}


```

There are a number of options you can pass in to the export method - they are defined in the [ImageExportOptions]() interface.

### CSS Classes[​](#css-classes "Direct link to CSS Classes")

The export helper UI exposes a few CSS classes you can use to style it:

| Class                       | Purpose                                                                              |
| --------------------------- | ------------------------------------------------------------------------------------ |
| `vjs-export-underlay`       | The modal backing element for SVG/PNG/JPG export dialog                              |
| `vjs-export-overlay`        | Content element for SVG/PNG/JPG export dialog                                        |
| `vjs-export-cancel`         | Assigned to the cancel button on an export dialog                                    |
| `vjs-export-dimensions`     | Assigned to the dimensions drop down in an export dialog                             |
| `vjs-export-download-tools` | Assigned to the element containing buttons and dimensions picker on an export dialog |

### Setting PNG/JPG export size[​](#setting-pngjpg-export-size "Direct link to Setting PNG/JPG export size")

When exporting a PNG or JPG you can provide a desired width or height for the exported image - just provide `width` or `height` as an option:

```jsx

import React, { useRef } from "react"
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import { ImageExporterUI } from "@visuallyjs/browser-ui"

export default function MyComponent() {
    const surfaceRef = useRef(null)
    
    const exportToPng = () => {
        // create an exporter and invoke the export method on it
        new ImageExporterUI(surfaceRef.current.surface).export({width:3000})    
    }
    
    return <div>
        <SurfaceComponent ref={surfaceRef}/>
        <button onClick={() => exportToPng()}>Export PNG</button>
        </div>
}


```

**********

Export PNG

If you click the export button above you'll get an image with width 3000 pixels. You can also specify height instead of width if you prefer, but if you specify height and width we'll only use the width you provide - the exporter always maintains the aspect ratio of the original image.

### Specifying a set of exportable dimensions[​](#specifying-a-set-of-exportable-dimensions "Direct link to Specifying a set of exportable dimensions")

If you'd like your users to be able to pick the dimensions of their exported image you can also do that:

```typescript
import { ImageExporterUI } from "@visuallyjs/browser-ui"
new ImageExporterUI(someSurface).export({
    dimensions:[
        { width:3000 },
        { width:1200 },
        { width:800 }
    ]
})

```

The entries in `dimensions` can have either width or height, but if you supply both we will, as discussed above, only honour the width. Try clicking the export button here - you'll see a dropdown from which you can pick the size of the export:

**********

Export PNG

## Programmatic export[​](#programmatic-export "Direct link to Programmatic export")

The various methods shown above are wrappers around a lower level API that you can use instead if you wish to.

### SVG Export[​](#svg-export-1 "Direct link to SVG Export")

```jsx

import React, { useRef } from "react"
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import { SVGExporter } from "@visuallyjs/browser-ui"

export default function MyComponent() {
    const surfaceRef = useRef(null)
    
    const exportToSvg = () => {
        // create an exporter and invoke the export method on it
        new SVGExporter(surfaceRef.current.surface).export()    
    }
    
    return <div>
        <SurfaceComponent ref={surfaceRef}/>
        <button onClick={() => exportToSvg()}>Export SVG</button>
        </div>
}


```

### PNG Export[​](#png-export-1 "Direct link to PNG Export")

```jsx

import React, { useRef } from "react"
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import { ImageExporter } from "@visuallyjs/browser-ui"

export default function MyComponent() {
    const surfaceRef = useRef(null)
    
    const exportToPng = () => {
        // create an exporter and invoke the export method on it
        new ImageExporter(surfaceRef.current.surface).export()    
    }
    
    return <div>
        <SurfaceComponent ref={surfaceRef}/>
        <button onClick={() => exportToPng()}>Export PNG</button>
        </div>
}


```

### JPG Export[​](#jpg-export-1 "Direct link to JPG Export")

```jsx

import React, { useRef } from "react"
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import { ImageExporter } from "@visuallyjs/browser-ui"

export default function MyComponent() {
    const surfaceRef = useRef(null)
    
    const exportToJpg = () => {
        // create an exporter and invoke the export method on it
        new ImageExporter(surfaceRef.current.surface).export({type:"image/jpeg"})    
    }
    
    return <div>
        <SurfaceComponent ref={surfaceRef}/>
        <button onClick={() => exportToJpg()}>Export JPG</button>
        </div>
}


```

## Exporting a Selection or Path[​](#exporting-a-selection-or-path "Direct link to Exporting a Selection or Path")

You can export a Selection or Path to SVG/PNG/JPG. For example here we create a Selection and add nodes "1", "2" and "5" to it, and then export that selection only:

```javascript
import { SVGExporter } from "@visuallyjs/browser-ui"

const selection = new Selection(model)
selection.append(["1", "2", "5"])
const exporter = new SVGExporter(surface)
const result = exporter.export({ selection })

```

<!-- -->

You can supply a `selection` to all of the UI exporter methods discussed above.

## Exporting the current selection[​](#exporting-the-current-selection "Direct link to Exporting the current selection")

You can export the [current selection](/react/docs/diagrams/model/selections#currentSelection) for some model instance to SVG/PNG/JPG. This can be very handy in conjunction with the lasso tool, for example - your users can snag a few nodes and print just those out.

```javascript
import React, { useRef, useEffect } from "react"
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"
import { SVGExporter } from "@visuallyjs/browser-ui"

export default function MyComponent() {
    const surfaceRef = useRef(null)
    
    const exportToSvg = () => {
        // create an exporter and invoke the `export` method on it
        const exporter = new SVGExporter(surfaceRef.current.surface)
        const result = exporter.exportCurrentSelection()
    }
    
    return <div>
        <SurfaceComponent ref={surfaceRef}/>
        <button onClick={() => exportToSvg()}>Export SVG</button>
        </div>
}


```
