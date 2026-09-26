# Column Layout

This is a specialized instance of `GridLayout` with the number of columns fixed to 1.

### Example[​](#example "Direct link to Example")

```javascript
import { newInstance, ColumnLayout } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  layout: {
    type: ColumnLayout.type
  }
})

```

### Sorting entries[​](#sorting-entries "Direct link to Sorting entries")

You can provide a `sort` function to the column layout to specify an order in which entries are placed. The layout will then arrange them in the specified order from top to bottom.

```javascript
import { newInstance, ColumnLayout } from "@visuallyjs/browser-ui"

const model = newInstance()

const surface = model.render({
  layout: {
    type: ColumnLayout.type,
    options: {
      sort: (a,b) => parseInt(b.id, 10) - parseInt(a.id, 10)
    }
  }
})

```

The `sort` function receives two arguments, `a` and `b`, which are either `Node` or `Group` objects, and it should return a number indicating their relative order.
