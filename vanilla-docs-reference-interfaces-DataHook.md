DataHook

A DataHook is a pair of functions that are invoked during a `load` and a `save`. This mechanism is a means you can use for storing/retrieving custom data from the payload the UI exports.

| Name | Type                      | Description                                                                 |
| ---- | ------------------------- | --------------------------------------------------------------------------- |
| load | (d:[UISaveData]()) => any | Notification that data has been loaded.                                     |
| save | (d:[UISaveData]()) => any | Notification that data is being saved. Your hook can write its data to `d`. |
