DiagramComponentProps

| Name          | Type               | Description                                                                                                                              |
| ------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| className?    | string             | Optional class name to set on the diagram component's container                                                                          |
| data?         | any                | Optional data to load after the component has been mounted.                                                                              |
| modelOptions? | [ModelOptions]()   | Options for the model used by the diagram. Only required for<br />certain advanced use cases.                                            |
| options?      | [DiagramOptions]() | Options for the diagram.                                                                                                                 |
| url?          | string             | Optional url from which to load data after the component has been mounted. If you provide this and also data, this will take precedence. |
