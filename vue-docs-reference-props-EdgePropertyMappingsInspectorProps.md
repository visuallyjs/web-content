EdgePropertyMappingsInspectorProps

| Name             | Type                                                | Description                                                                                                                            |
| ---------------- | --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| className?       | string                                              | Optional class name to use on the wrapper div. Defaults to `vjs-inspector-section`.                                                    |
| getPropertyName? | (pm:[PropertyMapping<]()[EdgeMapping]()>) => string | Optional, you can implement this method to return your own names to use for properties in the inspector.                               |
| mappings?        | [EdgePropertyMappings]()                            | Optional property mappings to render a form for. The default behaviour is to retrieve the property mappings from the inspector context |
| showName?        | boolean                                             | Optional, whether or not to show property names. Defaults to true.                                                                     |
