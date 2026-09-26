# Scrollable Lists

The `ListManagerPlugin` is used to manage lists within groups in VisuallyJS, and is great for applications such as data mappers. It handles the visibility and connection management of nodes within a scrollable list, ensuring that connections remain visible or are hidden appropriately as list items are scrolled out of view. In this canvas, try scrolling the groups - you'll see the edges scroll with their vertices, until one or both of the vertices is scrolled out of the view, at which point the edge is proxied onto the group element.

**********

## Configuration[​](#configuration "Direct link to Configuration")

To tell VisuallyJS to configure a list, you must add the `data-vjs-list="true"` attribute to the element you wish to act as the list container.

### Groups and CSS[​](#groups-and-css "Direct link to Groups and CSS")

It is important to note that the setup **must be a Group, not a node**. CSS plays a critical part in the correct functioning of a list:

1. The Group must have an element with the `data-vjs-group-content` attribute.
2. This content element must have a `max-size` and `overflow: auto`. (Without the `max-size` the list will just be drawn as big as it needs to be)

```css
.my-list-container {
    max-height: 200px;
    overflow: auto;
}

```

<!-- -->

## Setup[​](#setup "Direct link to Setup")

Configuration is in two parts.

### Register the plugin[​](#register-the-plugin "Direct link to Register the plugin")

Firstly, you need to register the plugin in your render options:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { ListManagerPlugin } from "@visuallyjs/browser-ui"
  const renderOptions = {
  plugins: [
    ListManagerPlugin.type
  ]
}
</script>

<SurfaceComponent {renderOptions}/>

```

### Configure UI[​](#configure-ui "Direct link to Configure UI")

How you configure

## Behaviors[​](#behaviors "Direct link to Behaviors")

The `ListManagerPlugin` supports two main behaviors when a node is scrolled out of view:

### Proxy (Default)[​](#proxy-default "Direct link to Proxy (Default)")

The default behavior is "proxy". When an item is scrolled out of view, any edges connected to it are "proxied" to the edge of the list container. This keeps the connection visible and indicates that it is connected to something currently off-screen within the list.

### Hide[​](#hide "Direct link to Hide")

In the "hide" behavior, edges connected to an item are simply hidden when that item is scrolled out of view.

You can configure the behavior globally in the plugin options:

```javascript
plugins:[
    {
        type:ListManagerPlugin.type,
        options: {
            behavior: "hide"
        }
    }
]

```

Or you can override it on a per-list basis using the `data-vjs-list-behavior` attribute:

```html
<div data-vjs-list="true" data-vjs-list-behavior="hide">
    ...
</div>

```

## Options[​](#options "Direct link to Options")

ListManagerPluginOptions

Options for the list manager plugin.

| Name      | Type              | Description                                                                                                                        |
| --------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| behavior? | "hide" \| "proxy" | Whether to proxy edges that are scrolled out of view, or to hide them. Possible values are "proxy" or "hide". Defaults to "proxy". |
