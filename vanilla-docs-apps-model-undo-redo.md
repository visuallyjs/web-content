# Undo/redo

VisuallyJs offers a comprehensive undo/redo manager, which is fully integrated into all the model and UI operations.

## Transactions[​](#transactions "Direct link to Transactions")

At the core of the undo/redo mechanism now is the concept of a `Transaction` - a set of operations which should be treated as an atomic unit. Certain internal methods in VisuallyJs use transactions, and it is also possible for a library user to declare their own.

The most direct way to work with transactions is via the `transaction` method on the model, which takes as argument a function to run inside the transaction. For instance, in this code snippet, we have some node that we wish to delete, and we're going to delete every other node this is connected to, inside a transaction. If the user subsequently undoes the operation, VisuallyJs will restore every node that was deleted, along with the edges that were deleted:

```typescript

const someNode:Node = ....

model.transaction(() => {

    // map all the edges for which this node is the source and get the target vertex
    const otherNodes = someNode.getSourceEdges().map(e => e.target)
    // remove them
    otherNodes.forEach(n => model.removeNode(n))
    // remove the focus node
    model.removeNode(someNode)
    
})

```

### Opening a transaction[​](#opening-a-transaction "Direct link to Opening a transaction")

To open a new transaction the basic call is:

```text
model.openTransaction()

```

Assuming you do not have a transaction already open this will create a new transaction in VisuallyJs. If you do have a transaction already open the method call as shown will throw an Error. VisuallyJs offers three flags you can use to instruct it what to do if a transaction is already open:

***Commit the current transaction and open a new one***

```text
import { COMMIT_CURRENT } from '@visuallyjs/browser-ui'

model.openTransaction(COMMIT_CURRENT)

```

***Rollback the current transaction and open a new one***

```text
import { ROLLBACK_CURRENT } from '@visuallyjs/browser-ui'

model.openTransaction(ROLLBACK_CURRENT)

```

***Append to the current transaction without opening a new one***

```text
import { APPEND_TO_CURRENT } from '@visuallyjs/browser-ui'

model.openTransaction(APPEND_TO_CURRENT)

```

### Closing a transaction[​](#closing-a-transaction "Direct link to Closing a transaction")

To close the current transaction you can either commit it or roll it back:

```javascript
model.commitTransaction()

```

```js
model.rollbackTransaction()

```

If there is no current transaction when these methods are called no action is taken.

### Closing a transaction that has been appended to[​](#closing-a-transaction-that-has-been-appended-to "Direct link to Closing a transaction that has been appended to")

If you use `APPEND_TO_CURRENT` when opening a transaction, and there was a current transaction at the time, you cannot directly commit or rollback the transaction: calling either of the above methods will result in a log message, but the transaction will remain open. VisuallyJs maintains a stack of append calls for the current transaction, and if you call `commitTransaction()` or `rollbackTransaction()` when there are append calls on the stack, VisuallyJs pops the stack instead of closing the transaction. Only when the append stack is empty will a `commitTransaction()` or `rollbackTransaction()` call succeed.

***

## Internal transactions[​](#internal-transactions "Direct link to Internal transactions")

As mentioned above, VisuallyJs performs a few key operations inside a transaction, These occur without user intervention and are included here purely for information.

* When a drag starts, a transaction is opened, and when the drag stops the transaction is closed. Since a drag cannot start in the middle of the execution of some other code (except perhaps in the case of a testing scenario), this transaction is opened with no flag to define how it should behave if there is an existing transaction: no transaction should already exist. If you see an error logged about opening a transaction when a drag starts then you have forgotten to close a transaction somewhere.

* `setMagnetizedPosition` operates within a transaction. All repositioning that occurs when a vertex is set and magnetized is bundled up into a single transaction (as more than one vertex generally moves when using the magnetizer).

* When a vertex is removed, a transaction is created and the vertex is removed along with any edges connected to it inside that transaction. The user can then undo the vertex and edge deletions as one operation.

***

## Constants[​](#constants "Direct link to Constants")

If you're using Javascript instead of Typescript, the constants you need are:

```javascript
export const COMMIT_CURRENT = "commitCurrent"
export const ROLLBACK_CURRENT = "rollbackCurrent"
export const APPEND_TO_CURRENT = "appendToCurrent"

```
