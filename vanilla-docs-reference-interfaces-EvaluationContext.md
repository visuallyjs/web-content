EvaluationContext

Helper API passed to calculators so they can read upstream values without knowing graph details.

| Name   | Type                                              | Description                                                                                                                                                                                      |
| ------ | ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| input  | (terminalId:string) => ValueType                  | Reads the value connected to one input terminal. Omit `terminalId` or pass `DEFAULT_TERMINAL` for direct node-body connections. Otherwise terminalId is assumed to map to a port ID on the node. |
| inputs | (terminalIds:Array\<string>) => Array\<ValueType> | Reads named input terminals in order. When omitted, reads every edge connected directly to the node body, in edge order.                                                                         |
