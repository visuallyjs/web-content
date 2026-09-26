NodeEvaluation\<ValueType,StateType>

Type Parameters

|           |   |                                                |
| --------- | - | ---------------------------------------------- |
| ValueType |   | Defines the type of the node's output values.  |
| StateType |   | Defines the type of the node's internal state. |

Result returned by a node calculator.

{

<br />

  outputs:Record\<string,ValueType | undefined>,

<br />

  state:StateType

<br />

}
