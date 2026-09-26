GroupAddedParams

Payload for a group added event in the model

| Name         | Type      | Description                                                               |
| ------------ | --------- | ------------------------------------------------------------------------- |
| group        | [Group]() | Group that was added                                                      |
| parentGroup? | [Group]() | If the group is a child of some other group, that group is provided here. |
