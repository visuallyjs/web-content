# Row Layout

This is a specialized instance of `GridLayout` with the number of rows fixed to 1.

### Example[​](#example "Direct link to Example")

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { RowLayout } from "@visuallyjs/browser-ui"
  const renderOptions = {
  layout: {
    type: RowLayout.type
  }
}
</script>

<SurfaceComponent {renderOptions}/>

```

### Sorting entries[​](#sorting-entries "Direct link to Sorting entries")

You can provide a `sort` function to the row layout to specify an order in which entries are placed. The layout will then arrange them in the specified order from left to right.

```html
<script>
  import { SurfaceComponent } from "@visuallyjs/browser-ui-svelte"
  import { RowLayout } from "@visuallyjs/browser-ui"
  const renderOptions = {
  layout: {
    type: RowLayout.type,
    options: {
      sort: (a,b) => parseInt(b.id, 10) - parseInt(a.id, 10)
    }
  }
}
</script>

<SurfaceComponent {renderOptions}/>

```

The `sort` function receives two arguments, `a` and `b`, which are either `Node` or `Group` objects, and it should return a number indicating their relative order.
