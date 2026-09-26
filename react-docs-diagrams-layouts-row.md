# Row Layout

This is a specialized instance of `GridLayout` with the number of rows fixed to 1.

### Example[​](#example "Direct link to Example")

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { RowLayout } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  layout: {
    type: RowLayout.type
  }
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

### Sorting entries[​](#sorting-entries "Direct link to Sorting entries")

You can provide a `sort` function to the row layout to specify an order in which entries are placed. The layout will then arrange them in the specified order from left to right.

```jsx
import { SurfaceComponent } from "@visuallyjs/browser-ui-react"

import { RowLayout } from "@visuallyjs/browser-ui"

export default function MyComponent() {

  const renderOptions = {
  layout: {
    type: RowLayout.type,
    options: {
      sort: (a,b) => parseInt(b.id, 10) - parseInt(a.id, 10)
    }
  }
}
  return <SurfaceComponent renderOptions={renderOptions}/>
}

```

The `sort` function receives two arguments, `a` and `b`, which are either `Node` or `Group` objects, and it should return a number indicating their relative order.
