# Column Layout

This is a specialized instance of `GridLayout` with the number of columns fixed to 1.

### Example[​](#example "Direct link to Example")

```html
<script setup>

import { ColumnLayout } from "@visuallyjs/browser-ui"

const renderOptions = {
  layout: {
    type: ColumnLayout.type
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

### Sorting entries[​](#sorting-entries "Direct link to Sorting entries")

You can provide a `sort` function to the column layout to specify an order in which entries are placed. The layout will then arrange them in the specified order from top to bottom.

```html
<script setup>

import { ColumnLayout } from "@visuallyjs/browser-ui"

const renderOptions = {
  layout: {
    type: ColumnLayout.type,
    options: {
      sort: (a,b) => parseInt(b.id, 10) - parseInt(a.id, 10)
    }
  }
}


</script>
<template>
  <SurfaceComponent :renderOptions="renderOptions" />
</template>

```

The `sort` function receives two arguments, `a` and `b`, which are either `Node` or `Group` objects, and it should return a number indicating their relative order.
