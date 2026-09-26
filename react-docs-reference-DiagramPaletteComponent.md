# \<DiagramPaletteComponent/>

A shape palette for linking with a [DiagramComponent](/react/docs/reference/DiagramComponent.md). This component will automatically display the shapes available to the Diagram it is attached to, allowing your users to drag them onto your Diagram, or to click to add.

## Usage[​](#usage "Direct link to Usage")

You'll need to declare a `DiagramProvider` in your JSX, and have the `DiagramComponent` and `DiagramPaletteComponent` both be descendants of that element:

```jsx
import {DiagramProvider, DiagramComponent, DiagramPaletteComponent } from "@visuallyjs/browser-ui-react";

export default function MyApp() {
    return <DiagramProvider>
        <DiagramComponent options={...}/>
        <DiagramPaletteComponent/>
    </DiagramProvider>
}


```

## Props[​](#props "Direct link to Props")

Sorry - we could not find this document.
