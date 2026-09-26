EdgeSnapOptions

Options for edge snap.

| Name            | Type             | Description                                                                                                                                                                           |
| --------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| enabled         | boolean          | Whether or not snap is enabled. Required.                                                                                                                                             |
| requireMagnets? | boolean          | If true, snapping will only operate on elements in the DOM that have been marked as magnets via the ATTRIBUTE\_VJS\_MAGNET attribute. Otherwise snapping will operate on all targets. |
| sizeThreshold?  | number           | Threshold in pixels for what determines a small vs a large target. See EdgeSnapType for discussion.                                                                                   |
| threshold?      | number           | Threshold in pixels for snapping to targets.                                                                                                                                          |
| type?           | [EdgeSnapType]() | How to snap - see docs for EdgeSnapType                                                                                                                                               |
