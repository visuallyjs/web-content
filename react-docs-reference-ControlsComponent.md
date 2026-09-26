# \<ControlsComponent/>

This component provides a set of controls for a surface - such operations as zoom to extents, undo/redo, clear, etc. The operations that are available can be specified on the controls element, and you can also add your own buttons.

## Usage[​](#usage "Direct link to Usage")

### Apps[​](#apps "Direct link to Apps")

This component is context aware and will discover the Surface to attach itself to if it is a child of a `SurfaceComponent`:

```jsx
<SurfaceComponent renderOptions={...} data={...}>
    <ControlsComponent />
</SurfaceComponent>

```

or if it is a descendant of a `SurfaceProvider`:

```jsx
<SurfaceProvider>
    <SurfaceComponent renderOptions={...} data={...}/>
    <div className="someContainer">
        <ControlsComponent/>
    </div>
</SurfaceProvider>

```

### Diagrams[​](#diagrams "Direct link to Diagrams")

This component is context aware and will discover the Diagram to attach itself to if it is a child of a `DiagramComponent`:

```jsx
<DiagramComponent options={...} data={...}>
    <ControlsComponent />
</DiagramComponent>

```

or if it is a descendant of a `DiagramProvider`:

```jsx
<DiagramProvider>
    <DiagramComponent options={...} data={...}/>
    <div className="someContainer">
        <ControlsComponent/>
    </div>
</DiagramProvider>

```

## Props[​](#props "Direct link to Props")

ControlsComponentProps

Props for the controls component.

| Name           | Type                         | Description                                                                                                                                                                                                                                         |
| -------------- | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| buttons?       | [ControlsComponentButtons]() | Optional extra buttons to add to the controls component.                                                                                                                                                                                            |
| className?     | string                       | Optional class name to append to the root element's class list.                                                                                                                                                                                     |
| clear?         | boolean                      | Whether or not to show the clear button, defaults to true.                                                                                                                                                                                          |
| clearMessage?  | string                       | Optional message for the alert that the clear button shows by default. Defaults to `Clear dataset?`.                                                                                                                                                |
| onMaybeClear?  | (doClear:() => void) => void | Optional callback to invoke when the user presses the clear button. If you provide this, the component will not show an alert, and instead call this method, passing in a function you can invoke if you wish to continue with the clear operation. |
| orientation?   | "row" \| "column"            | Optional orientation for the controls. Defaults to 'row'.                                                                                                                                                                                           |
| style?         | Record\<string,string>       | Optional style object to apply to the container element.                                                                                                                                                                                            |
| surfaceId?     | string                       | The ID of surface to attach to. Optional. Will be inferred from context if not provided.                                                                                                                                                            |
| undoRedo?      | boolean                      | Whether or not to show undo/redo buttons, defaults to true                                                                                                                                                                                          |
| zoomButtons?   | boolean                      | Whether or not to show the zoom in/zoom out buttons, defaults to false                                                                                                                                                                              |
| zoomToExtents? | boolean                      | Whether or not to show the zoom to extents button, defaults to true                                                                                                                                                                                 |
