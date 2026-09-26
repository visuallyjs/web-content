Calculator\<ValueType,StateType>

Type Parameters

|           |   |                                                |
| --------- | - | ---------------------------------------------- |
| ValueType |   | Defines the type of the node's output values.  |
| StateType |   | Defines the type of the node's internal state. |

Evaluates a node from its current upstream inputs - the function has access to the `input(...)` and `inputs(..)` methods on the evaluation context that is passed in, for resolving the input values on the node.

`(node:Node, context:EvaluationContext<ValueType>) => NodeEvaluation<ValueType,StateType> | undefined`
