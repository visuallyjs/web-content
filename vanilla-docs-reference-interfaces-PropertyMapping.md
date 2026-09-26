PropertyMapping

A mapping of some property/properties to a set of appearance values. Currently only used by edges.

| Name     | Type                     | Description                                                                                                                                                                       |
| -------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| mappings | Record\<string,D>        | A map whose keys are expected values for the given property (or a space-separated string of values if an array of properties was provided), and the values are the type to apply. |
| name?    | string                   | Optional name to use for the mapping in the UI (for example, in an inspector)                                                                                                     |
| property | string \| Array\<string> | Property or properties to map. If an array is provided, values are matched against all properties in the order given.                                                             |
