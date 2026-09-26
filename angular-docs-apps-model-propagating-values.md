# Graph propagation engine

Since:

<!-- -->

1.2.8

The `GraphPropagationEngine` is a class that you can use to automatically propagate values through a dataset, using a simple API in which you only need to define three things:

* the type of the value that will be propagated along edges
* the type of each node's computed internal state (actually optional)
* a calculator for each node type, which is responsible for returning each node's internal state and outputs

Use cases for this functionality are many and varied. Here's a simple maths equation UI where users can increment and decrement values and see changes downstream:

<!-- -->

## Setup[​](#setup "Direct link to Setup")

There are a few concepts you need to familiarise yourself with to use the graph propagation engine, but this seems like something where starting with an example will be better. Once you've read through the code in this section, the information in the [concepts](#concepts) section below will probably make a bit more sense.

For the maths app shown above, we have four node types:

* **variable** These are the inputs to an arithmetic node
* **plus** A node that performs the addition operation on its inputs
* **multiply** A node that performs the multiplication operation on its inputs
* **result** A node that displays a result

### Value type[​](#value-type "Direct link to Value type")

The type of value propagated along edges is `number`.

### Internal state[​](#internal-state "Direct link to Internal state")

All nodes in VisuallyJs have a `data` object backing them, which is internal state. Internal state in this page, though, refers to *computed* internal state, which can change each time the engine runs. It is stored inside the `data` object, keyed by the property name `computed`.

Our `variable` and `result` nodes don't need computed internal state. But we want our arithmetic nodes - `plus` and `multiply` - to compute a human readable representation of the equation they ran.

### Calculators[​](#calculators "Direct link to Calculators")

Each node type from which we wish to extract values must have an associated `Calculator` defined. In the case of this maths app, we need one for `variable`, `plus` and `multiply`. We do not need a calculator for `result` as we only write to that node type. So, this is the source code for the calculators used above:

```typescript
const mathsCalculators = {
  "plus":(node, context) => {
    const inputs = context.inputs()
    return {
      state:{
        // plus node's internal state is
        // a human readable equation
        equation:inputs.join(" + ")
      },
      outputs:{
        // plus node default output is the sum of its inputs
        default:inputs.length > 0 ? inputs.reduce((a, b) => a + b) : 0
      }
    }
  },
  "multiply":(node, context) => {
    const inputs = context.inputs()
    return {
      state:{
          // multiply node's internal state is
          // a human readable equation
        equation:inputs.join(" * ")
      }, 
      outputs:{
        // multiply node's default output is the product of
        // its inputs
        default:inputs.reduce((a, b) => a * b, 1)
      }
    }
  },
  "variable":(node, context) => {
    return {
      outputs:{
        // variable node outputs the `value` 
        // from its backing data
        default:node.data.value
      }
    }
  }
}

```

## UI Setup[​](#ui-setup "Direct link to UI Setup")

<!-- -->

In an app, configure the graph propagation engine via the plugin:

```typescript
import { Component, ViewChild } from '@angular/core';
import { SurfaceComponent } from '@visuallyjs/browser-ui-angular';
import { PLUGIN_TYPE_GRAPH_PROPAGATION } from "@visuallyjs/browser-ui"


@Component({
  selector: 'app-root',
  template: ` <vjs-surface [renderOptions]="renderOptions" [viewOptions]="viewOptions"></vjs-surface> `
})
export class AppComponent {
  renderOptions = {
  plugins: [
    {
      type: PLUGIN_TYPE_GRAPH_PROPAGATION,
      options: {
        calculators: mathsCalculators
      }
    }
  ]
};
  viewOptions = {
  nodes: {
    plus: {
      component: PlusNode
    },
    multiply: {
      component: MultiplyNode
    },
    variable: {
      component: VariableNode
    },
    result: {
      component: ResultNode
    }
  }
};
}

```

info

For the sake of brevity we're not including the source for the components mapped above. If you'd like the full source code for this example, [get in touch](/contact.md).

<!-- -->

## Example - Logic Gates[​](#example---logic-gates "Direct link to Example - Logic Gates")

Another example of the usefulness of this engine is that of logic gates:

<!-- -->

Try tapping the nodes on the left hand side - the boolean value in the given node will be toggled, and the new value will be propagated through the diagram.

We have four node types in this example:

* **AND gate** Performs a logical AND operation
* **OR gate** Performs a logical OR operation
* **source** A value source
* **sink** Displays an output value

### Value Type[​](#value-type-1 "Direct link to Value Type")

For this app, we're going to use this type (from the <!-- -->[Logic Gates](/demonstrations/logic-gates.md) starter app):

```typescript
export type BooleanValue = 1 | 0

```

### Internal State[​](#internal-state-1 "Direct link to Internal State")

We don't need to compute any internal state for this app.

### Calculators[​](#calculators-1 "Direct link to Calculators")

We'll be pulling values from nodes of type **and**, **or** and **source**, so we need a calculator defined for each of those types:

```typescript

const booleanCalculators = {
  "and":(node, context) => {
    const inputs = context.inputs()
    // compute the logical AND of all the inputs
    const out = inputs.length > 0 ? inputs.reduce((a, b) => a && b) : 0
    return {
      outputs:{
        // return the logical AND as the default output
        default:out
      }
    }
  },
  "or":(node, context) => {
    const inputs = context.inputs()
    // compute the logical OR of all the inputs
    const out = inputs.reduce((a, b) => a || b, 0)
    return {
      outputs:{
        // return the logical OR as the default output
        default:out
      }
    }
  },
  "source":(node, context) => {
    return {
      outputs:{
        // the source node returns 'value'
        // from its backing data
        default:node.data.value
      }
    }
  }
}


```

## Concepts[​](#concepts "Direct link to Concepts")

The above examples reference several interfaces - this section presents the interface definitions and offers some explanatory text on each one.

### ValueType[​](#valuetype "Direct link to ValueType")

This defines the type of value that flows along edges. In our maths example on this page we used `number` for the value type, and in the logic gates example we used `BooleanType`. You can use any type.

### Calculator[​](#calculator "Direct link to Calculator")

A `Calculator` is a function that takes a `Node` and an `EvaluationContext` and returns a `NodeEvaluation` or `undefined`.. The definition of this type is:

Calculator\<ValueType,StateType>

Type Parameters

|           |   |                                                |
| --------- | - | ---------------------------------------------- |
| ValueType |   | Defines the type of the node's output values.  |
| StateType |   | Defines the type of the node's internal state. |

Evaluates a node from its current upstream inputs - the function has access to the `input(...)` and `inputs(..)` methods on the evaluation context that is passed in, for resolving the input values on the node.

`(node:Node, context:EvaluationContext<ValueType>) => NodeEvaluation<ValueType,StateType> | undefined`

### EvaluationContext[​](#evaluationcontext "Direct link to EvaluationContext")

This is the context object passed to each calculator so it can ask for the current value on an input terminal without needing to know how the graph is connected.

EvaluationContext

Helper API passed to calculators so they can read upstream values without knowing graph details.

| Name   | Type                                              | Description                                                                                                                                                                                      |
| ------ | ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| input  | (terminalId:string) => ValueType                  | Reads the value connected to one input terminal. Omit `terminalId` or pass `DEFAULT_TERMINAL` for direct node-body connections. Otherwise terminalId is assumed to map to a port ID on the node. |
| inputs | (terminalIds:Array\<string>) => Array\<ValueType> | Reads named input terminals in order. When omitted, reads every edge connected directly to the node body, in edge order.                                                                         |

### NodeEvaluation[​](#nodeevaluation "Direct link to NodeEvaluation")

This is the return value from a `Calculator`:

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

## Advanced usage - ports[​](#advanced-usage---ports "Direct link to Advanced usage - ports")

The two examples given on this page have both worked with datasets where values are propagated at a node level. In many real world scenarios, though, you'll be working with a dataset involving ports. This is the case with our <!-- -->[Logic Gates](/demonstrations/logic-gates.md) starter app:

![Logic gates graph propagation](https://static.visuallyjs.com/img/tech-talk/logic-gates-graph-propagation-execution.png)

Each logic gate contains two named input ports ("in1" and "in2"), and one named output port ("out"). The `source` and `sink` nodes use values at the node level.

The only difference when working with ports is inside your calculator functions - where in our previous examples we used the `inputs()` method of the evaluation context to retrive all inputs to some node, when working with ports it is more usual to use the `input(terminalId:string)` method. You can find the code for the logic gates starter app [here on Github](https://github.com/visuallyjs-angular/logic-gates), but here's an example of how the AND gate calculator is written:

```typescript
{
    "and-gate":(node:Node, context:EvaluationContext<BooleanValue>) => {
        const in1 = context.input("in1")
        const in2 = context.input("in2")
        return {
            outputs:{
                out:in1 && in2
            }
        }
    }
}

```

You can see how the code retrieves named inputs "in1" and "in2", and exports a named "out" output. Compare this with the code for the `junction` type (which uses node level state, and passes it through to its output):

```typescript
"junction": (_node:Node, context:EvaluationContext<BooleanValue>):NodeEvaluation<BooleanValue, BooleanState> => {
  const value = context.input(DEFAULT_TERMINAL)
  return {
    outputs: {
      [DEFAULT_TERMINAL]: value
    },
    state: {
      value
    }
  }
}

```

..and the `source` node type, which just extracts a value from its `data`:

```typescript
"source": (node: Node) => {
  const value = node.data.value as BooleanValue
  return {
    outputs: {
      [DEFAULT_TERMINAL]: value
    },
    state: {
      value
    }
  }
}

```
