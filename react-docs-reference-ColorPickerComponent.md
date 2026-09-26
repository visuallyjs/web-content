# \<ColorPickerComponent/>

A helper component that offers the ability to change color and keep a history of selected colors, for use with an [InspectorComponent](/react/docs/reference/InspectorComponent.md).

## Usage[​](#usage "Direct link to Usage")

If you haven't yet read the docs for [InspectorComponent](/react/docs/reference/InspectorComponent.md) we'd recommend it.

This component is used in the template for an inspector. You need to pass in the name of the property to manage.

```jsx

import { useState } from "react"
import { ColorPickerComponent } from "@visuallyjs/browser-ui-react"

export default function MyInspectorComponent(props) {

    const [currentType, setCurrentType] = useState('')
    const renderEmptyContainer = () => setCurrentType('')
    
    // a Node, Edge, Group or Port
    const refresh= (obj, cb) => {
        setCurrentType(obj.objectType)
    }

    return <InspectorComponent refresh={refresh}
                   renderEmptyContainer={renderEmptyContainer}>
        
        <ColorPickerComponent propertyName="bgColor"/>

    </InspectorComponent>
}
    

```

## Inputs[​](#inputs "Direct link to Inputs")

ColorPickerComponentProps

Props for the ColorPicker inspector component.

| Name         | Type   | Description                                                      |
| ------------ | ------ | ---------------------------------------------------------------- |
| maxColors?   | number | Maximum color swatches to show. Defaults to 10.                  |
| propertyName | string | Property name in the data that this picker represents. Required. |
