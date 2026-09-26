DiagramSaveOptions

Save options for a Diagram

| Name        | Type                | Description                                                                                                                                                          |
| ----------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| parameters? | Record\<string,any> | Optional parameters to pass to the exporter. If you write a custom exporter you may wish to use this.                                                                |
| type?       | string              | Specifies the data type in which to format the data. Defaults to `"json"`. This must match the name of an exporter registered with the given instance of VisuallyJs. |
