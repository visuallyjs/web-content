GraphPropagationEnginePluginOptions

Options for the graph propagation plugin.

| Name           | Type                                                 | Description                                                            |
| -------------- | ---------------------------------------------------- | ---------------------------------------------------------------------- |
| calculators    | Record\<string,[Calculator\<ValueType,StateType>]()> | Calculator functions keyed by node or group type.                      |
| property?      | string                                               | Model property used for propagated values. Defaults to `value`.        |
| stateProperty? | string                                               | Model property used for calculated node state. Defaults to `computed`. |
