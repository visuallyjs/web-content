# Events

You can map a number of events to nodes and groups in a view, and when the event fires, VisuallyJs will supply the event from the browser, the DOM element on which the event occurred, and the model object related to the event.

You can bind a listener to anything listed as a **BindableViewEvent**:

BindableViewEvent

Events that can be bound in a view.

`EVENT_CLICK | EVENT_DBLCLICK | EVENT_TAP | EVENT_DBLTAP | EVENT_CONTEXTMENU | EVENT_MOUSEDOWN | EVENT_MOUSEOUT | EVENT_MOUSEUP | EVENT_MOUSEOVER | EVENT_MOUSEMOVE`

## Mapping events[​](#mapping-events "Direct link to Mapping events")

To map an event, provide an `events` object inside a node or group definition:

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { NodeEventCallbackPayload, GroupEventCallbackPayload, DEFAULT, EVENT_TAP, EVENT_MOUSEOVER } from "@visuallyjs/browser-ui"
</script>

<SurfaceComponent/>

```

## Event Payload[​](#event-payload "Direct link to Event Payload")

The payload for events mapped in a view depends on the vertex type:

### Nodes[​](#nodes "Direct link to Nodes")

NodeEventCallbackPayload

The payload passed to a NodeEventCallback

| Name  | Type                | Description                                                   |
| ----- | ------------------- | ------------------------------------------------------------- |
| e     | MouseEvent          | The pointer event that caused the event handler to be invoked |
| el    | EL                  | Element that represents the vertex in the UI                  |
| model | [VisuallyJsModel]() | The underlying VisuallyJs model                               |
| obj   | [Node]()            | The model object for the vertex                               |
| ui    | UICore\<EL>         | The UI that rendered this vertex                              |

### Groups[​](#groups "Direct link to Groups")

GroupEventCallbackPayload

The payload passed to a GroupEventCallback

| Name  | Type                | Description                                                   |
| ----- | ------------------- | ------------------------------------------------------------- |
| e     | MouseEvent          | The pointer event that caused the event handler to be invoked |
| el    | EL                  | Element that represents the vertex in the UI                  |
| model | [VisuallyJsModel]() | The underlying VisuallyJs model                               |
| obj   | [Group]()           | The group in the model                                        |
| ui    | UICore\<EL>         | The UI that rendered this vertex                              |
