DiagramCellTemplateEventCallbackPayload

Payload passed to a cell template event callback.

| Name        | Type                  | Description                                                                          |
| ----------- | --------------------- | ------------------------------------------------------------------------------------ |
| cell        | [DiagramCell]()       | The diagram cell whose rendered template contained the matching event target.        |
| diagram     | [Diagram]()           | The diagram that owns the cell.                                                      |
| event       | E                     | The original browser event.                                                          |
| eventTarget | [BrowserElement]()    | The element inside the rendered shape template that matched the configured selector. |
| model       | [BrowserUIModel]()    | The underlying VisuallyJs model.                                                     |
| ui          | [BrowserUI]()         | The UI that rendered the diagram.                                                    |
| vertex      | [Node]() \| [Group]() | The backing vertex for the cell.                                                     |
