PaletteEventHandlers

Hadlers you can pass as an argument to palette drag handlers,

| Name        | Type     | Description                                                                          |
| ----------- | -------- | ------------------------------------------------------------------------------------ |
| after?      | Function | Fired after the operation has been completed                                         |
| afterMove?  | Function | fired after the initial move event is posted and before the 2nd move event is posted |
| beforeDown? | Function | Fired before the mousedown event is posted                                           |
| beforeMove? | Function | Fired before an initial move event is posted                                         |
| beforeUp?   | Function | Fired after the 2nd move event, before the up event                                  |
