SourceValueTargetCsvParserOptions

Options for a source,target,value CSV parser.

| Name           | Type                                                                               | Description                                                                                      |
| -------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| edgeDecorator? | (e:[ObjectData](), source:[ObjectData](), target:[ObjectData]()) => [ObjectData]() | Optional function that you can use to decorate loaded edges prior to their addition to the model |
| nodeDecorator? | (o:[ObjectData](), isSource:boolean) => [ObjectData]()                             | Optional function that you can use to decorate loaded nodes prior to their addition to the model |
| readHeaders?   | boolean                                                                            | Defaults to true - whether or not the file is expected to have headers                           |
