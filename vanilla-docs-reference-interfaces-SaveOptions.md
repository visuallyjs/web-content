SaveOptions

Options for a save via ajax.

| Name        | Type                       | Description                                                                                                                                                                                                                       |
| ----------- | -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| data?       | any                        | optional data to save. If not provided we use the return value of `exportData()`.                                                                                                                                                 |
| error?      | (e:any, status:any) => any | Optional callback to execute if there was an error saving the data.                                                                                                                                                               |
| headers?    | Record\<string,string>     | Optional headers to set on the ajax request. By default, VisuallyJs will send a `Content-Type:"application/json"` header. If you provide your own headers this header will continue to be sent, unless of course you override it. |
| parameters? | Record\<string,any>        | Optional parameters to pass to the exporter. If you write a custom exporter you may wish to use this.                                                                                                                             |
| success?    | (r:any) => any             | Optional callback to execute once the data has saved successfully.                                                                                                                                                                |
| type?       | string                     | Specifies the data type in which to format the data. Defaults to `"json"`. This must match the name of an exporter registered with the given instance of VisuallyJs.                                                              |
| url         | string                     | URL to POST data to. Required.                                                                                                                                                                                                    |
