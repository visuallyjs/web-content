ModelEventCallback\<T,E>

Type Parameters

|   |       |                                                                                                           |
| - | ----- | --------------------------------------------------------------------------------------------------------- |
| T |       | Maps the type of object the event pertains to - a Node, Group, Edge or Port.                              |
| E | Event | Maps the event class you expect as a return value. Providing this helps you to type things more strictly. |

Callback for a model event.

`(p:ModelEventCallbackPayload<T,E>) => any`
