# Overlays

This page provides a reference for the various simple overlays that ship with VisuallyJs.

## Arrow[​](#arrow "Direct link to Arrow")

An arrow with a configurable `foldback` point.

```javascript

{
  "type": "Arrow",
  "options": {
    "location": 1
  }
}

```

**********

ArrowOverlayOptions

Options for an Arrow overlay.

| Name        | Type                                                    | Description                                                                                                    |
| ----------- | ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| attributes? | Record\<string,string>                                  | Optional custom attributes to write to the overlay's element.                                                  |
| cssClass?   | string                                                  | Optional CSS class(es) to add to the overlay's element.                                                        |
| direction?  | number                                                  | 1 to point forwards (the default), -1 to point backwards. Only taken into consideration in some overlay types. |
| events?     | Record<[OverlayEvents](),(value:any, event:any) => any> | Optional event handlers to attach to the overlay.                                                              |
| foldback?   | number                                                  | How far, as a decimal, along the line from head to baseline to fold back into. Defaults to 0.623.              |
| hollow?     | boolean                                                 | Defaults to false. When true, the arrow is stroked but not filled.                                             |
| id?         | string                                                  | Optional ID for the overlay. Can be used to retrieve the overlay from a connection.                            |
| length?     | number                                                  | Length from the head to the baseline. Defaults to 20.                                                          |
| location?   | number                                                  | Defaults to 0.5. See docs.                                                                                     |
| paintStyle? | [PaintStyle]()                                          | Optional paint style to use.                                                                                   |
| visibility? | [OverlayVisibility]()                                   | Whether the overlay is always visible, or only on hover. Defaults to OVERLAY\_VISIBILITY\_ALWAYS.              |
| width?      | number                                                  | Width of the arrow's baseline. Defaults to 20.                                                                 |

### Arrow direction[​](#arrow-direction "Direct link to Arrow direction")

A point to note is that `location:0` for arrow overlays will not reverse the direction in which the arrow is pointing. To have the arrow point backwards along the path you have to provide a value for `direction`:

```javascript
overlays:[    
    {
        type:"Arrow",
        options:{
            width:10,
            length:15,
            location:0,
            direction:-1
        }
    }   
]

```

The `direction:-1` here instructs VisuallyJs to draw the arrow painting backwards. There are only two valid values for `direction` - `1` and `-1`. If you provide any other value - or no value - then VisuallyJs will use a value of 1, meaning the arrow points forwards.

***

## PlainArrow[​](#plainarrow "Direct link to PlainArrow")

This overlay is an extension of `Arrow` with the `foldback` parameter's value fixed to `1`. This results in an arrow with a flat back.

```javascript

{
  "type": "PlainArrow",
  "options": {
    "location": 1
  }
}

```

**********

***

## Diamond[​](#diamond "Direct link to Diamond")

This overlay is an extension of `Arrow` with the `foldback` parameter's value fixed to `2`. This results in an arrow shaped like a diamond.

```javascript

{
  "type": "Diamond",
  "options": {
    "location": 0.3
  }
}

```

**********

***

## Dot[​](#dot "Direct link to Dot")

This is a circle, with configurable radius.

```javascript

{
  "type": "Dot",
  "options": {
    "location": 0,
    "radius": 13
  }
}

```

**********

note

If you are a JsPlumb Toolkit user, note that a `Dot` overlay at location 0 or 1 is equivalent to using a `Dot` endpoint in JsPlumb.

DotOverlayOptions

Options for a Dot overlay

| Name        | Type                                                    | Description                                                                                                                                                                                                                                                                                                                     |
| ----------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| align?      | "center" \| "flush"                                     | When the overlay is at position 1 or 0 (or is being used a source/target marker), this determines how the dot intersects the vertex. A value of 'flush', which is the default, means a point on the circumference of the dot touches the vertex boundary. A value of 'center' means the dot's center is on the vertex boundary. |
| attributes? | Record\<string,string>                                  | Optional custom attributes to write to the overlay's element.                                                                                                                                                                                                                                                                   |
| cssClass?   | string                                                  | Optional CSS class(es) to add to the overlay's element.                                                                                                                                                                                                                                                                         |
| direction?  | number                                                  | 1 to point forwards (the default), -1 to point backwards. Only taken into consideration in some overlay types.                                                                                                                                                                                                                  |
| events?     | Record<[OverlayEvents](),(value:any, event:any) => any> | Optional event handlers to attach to the overlay.                                                                                                                                                                                                                                                                               |
| hollow?     | boolean                                                 | Defaults to false. When true, the arrow is stroked but not filled.                                                                                                                                                                                                                                                              |
| id?         | string                                                  | Optional ID for the overlay. Can be used to retrieve the overlay from a connection.                                                                                                                                                                                                                                             |
| location?   | number                                                  | Defaults to 0.5. See docs.                                                                                                                                                                                                                                                                                                      |
| paintStyle? | [PaintStyle]()                                          | Optional paint style to use.                                                                                                                                                                                                                                                                                                    |
| radius?     | number                                                  | Radius of the dot. Defaults to 5.                                                                                                                                                                                                                                                                                               |
| visibility? | [OverlayVisibility]()                                   | Whether the overlay is always visible, or only on hover. Defaults to OVERLAY\_VISIBILITY\_ALWAYS.                                                                                                                                                                                                                               |

***

## Rectangle[​](#rectangle "Direct link to Rectangle")

This is a rectangle, with configurable width and height.

```javascript

{
  "type": "Rectangle",
  "options": {
    "location": 1,
    "width": 15,
    "height": 10
  }
}

```

**********

note

If you are a JsPlumb user, note that a `Rectangle` overlay at location 0 or 1 is equivalent to using a `Rectangle` endpoint in JsPlumb.

RectangleOverlayOptions

Options for a Rectangle overlay

| Name        | Type                                                    | Description                                                                                                                                                                                                                                                                                                                                  |
| ----------- | ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| align?      | "center" \| "flush"                                     | When the overlay is at position 1 or 0 (or is being used a source/target marker), this determines how the rectangle intersects the vertex. A value of 'flush', which is the default, means a point on the boundary of the rectangle touches the vertex boundary. A value of 'center' means the rectangle's center is on the vertex boundary. |
| attributes? | Record\<string,string>                                  | Optional custom attributes to write to the overlay's element.                                                                                                                                                                                                                                                                                |
| cssClass?   | string                                                  | Optional CSS class(es) to add to the overlay's element.                                                                                                                                                                                                                                                                                      |
| direction?  | number                                                  | 1 to point forwards (the default), -1 to point backwards. Only taken into consideration in some overlay types.                                                                                                                                                                                                                               |
| events?     | Record<[OverlayEvents](),(value:any, event:any) => any> | Optional event handlers to attach to the overlay.                                                                                                                                                                                                                                                                                            |
| height?     | number                                                  | Height of the rectangle. Defaults to 10.                                                                                                                                                                                                                                                                                                     |
| hollow?     | boolean                                                 | Defaults to false. When true, the arrow is stroked but not filled.                                                                                                                                                                                                                                                                           |
| id?         | string                                                  | Optional ID for the overlay. Can be used to retrieve the overlay from a connection.                                                                                                                                                                                                                                                          |
| location?   | number                                                  | Defaults to 0.5. See docs.                                                                                                                                                                                                                                                                                                                   |
| paintStyle? | [PaintStyle]()                                          | Optional paint style to use.                                                                                                                                                                                                                                                                                                                 |
| rotate?     | boolean                                                 | Whether or not to rotate the rectangle so that it is always perpendicular to the connector path. Defaults to false.                                                                                                                                                                                                                          |
| visibility? | [OverlayVisibility]()                                   | Whether the overlay is always visible, or only on hover. Defaults to OVERLAY\_VISIBILITY\_ALWAYS.                                                                                                                                                                                                                                            |
| width?      | number                                                  | Width of the rectangle. Defaults to 10.                                                                                                                                                                                                                                                                                                      |

***

## Label[​](#label "Direct link to Label")

```javascript

{
  "type": "Label",
  "options": {
    "label": "Hello"
  }
}

```

**********

LabelOverlayOptions

Options for a label overlay

| Name                    | Type                                                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| attributes?             | Record\<string,string>                                  | Optional custom attributes to write to the overlay's element.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| backgroundStyle?        | [LabelBackgroundStyle]()                                | Optional style for the label's background.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| cssClass?               | string                                                  | Optional CSS class(es) to add to the overlay's element.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| direction?              | number                                                  | 1 to point forwards (the default), -1 to point backwards. Only taken into consideration in some overlay types.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| events?                 | Record<[OverlayEvents](),(value:any, event:any) => any> | Optional event handlers to attach to the overlay.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| font?                   | [FontSpec]()                                            | Optional spec for the font to use on this label.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| id?                     | string                                                  | Optional ID for the overlay. Can be used to retrieve the overlay from a connection.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| label                   | string \| Function                                      | String, or a function returning a string, for the label.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| labelLocationAttribute? | string                                                  | Optional name of the attribute that identifies this overlay's location on the path. Defaults to `location`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| location?               | number                                                  | Defaults to 0.5. See docs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| rotatable?              | boolean \| "strict" \| "legible"                        | Sets whether the label can be rotated to match the gradient of the connector at that location at which it is positioned. If you supply boolean true here, the label will be made rotatable, in "legible" mode - in which VisuallyJs ensures that the label is legible by avoiding rotating the text so that it is upside down or otherwise awkward to read. You can set "strict" mode, which will rotate the label to the appropriate angle regardless of whether or not it will make the label difficult to read. If you supply boolean false, the label will not be rotatable in any situation. |
| useHTMLElement?         | boolean                                                 | Whether or not to use an HTML element. Defaults to false (uses an SVG element)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| visibility?             | [OverlayVisibility]()                                   | Whether the overlay is always visible, or only on hover. Defaults to OVERLAY\_VISIBILITY\_ALWAYS.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

The `label` for a label overlay can be a string or a function, but in practice with VisuallyJs you'll generally be defining labels as strings, as the values presented to the renderer are extracted from the JSON backing data for each edge.

#### SVG vs HTML elements[​](#svg-vs-html-elements "Direct link to SVG vs HTML elements")

By default, regardless of whether or not the container is an SVG element, a label overlay will be rendered as an SVG element. This is the most memory efficient and also allows a label to be printed by an SVG exporter. You can instruct VisuallyJs to use an HTML element via the `useHTMLElement` option for the label.

***

## Custom[​](#custom "Direct link to Custom")

The custom overlay allows you to create your own overlays, which VisuallyJs will position for you. You need to implement one method - `create(component)` - which is passed the component on which the overlay is located as an argument, and which returns a DOM element:

```javascript

  overlays:[
    {
        type:"Custom",
        options:{
          create:(component) => {
              const d = document.createElement("select")
              d.innerHTML = "<option value='foo'>foo</option><option value='bar'>bar</option>"
              return d
          },
          location:0.7
        }
    }
  ]

```

Here we have created a select box with a couple of values, assigned to it the id of 'customOverlay' and placed it at location 0.7.

note

A custom overlay is a plain HTML element - you may wish to consider using a component overlay instead.
