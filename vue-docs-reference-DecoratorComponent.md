# \<DecoratorComponent/>

This component allows you to position content relative to the canvas in your UI - either floating on top, or positioned with the canvas content.

Content can be any valid Vue markup - including components.

## Usage[​](#usage "Direct link to Usage")

### Floating content[​](#floating-content "Direct link to Floating content")

The default behaviour is to float the content above the UI canvas, where `position` is relative to the canvas viewport:

```html
<SurfaceComponent .../>
    <Decorator :position="{x:50, y:50}">
        <h4>Hello World</h4>
		<button @click="invokeAMethod($event)">click me</button>
    </Decorator>
</SurfaceComponent>

```

### Fixed content[​](#fixed-content "Direct link to Fixed content")

You can specify "'fixed'" positioning if you want to place the conent on the canvas. Here, `position` will be treated as a point relative to the canvas origin, and the content will be drawn on the UI canvas alongside the vertices and edges:

```html
<SurfaceComponent .../>
    <Decorator :position="{x:50, y:50}" :placement="'fixed'">
        <h4>Hello World</h4>
		<button @click="invokeAMethod($event)">click me</button>
    </Decorator>
</SurfaceComponent>

```

### Clamping to canvas[​](#clamping-to-canvas "Direct link to Clamping to canvas")

When using `fixed` content, you can instruct VisuallyJs to prevent the fixed element from being panned out of the viewport, by supplying constraints to the decorator - here we instruct VisuallyJs to clamp in both the left and top directions:

```jsx
<SurfaceComponent .../>
    <Decorator position="{x:50, y:50}"
               placement="'fixed'" 
               constraints="{left:true, top:true}">
        <h4>Hello World</h4>
        <button @click="invokeAMethod($event)">click me</button>
    </Decorator>
</SurfaceComponent>

```

## Props[​](#props "Direct link to Props")

DecoratorComponentProps

Props for the DecoratorComponent

| Name         | Type                        | Description                                                                                                                                                                                                        |
| ------------ | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| constraints? | [FixedElementConstraints]() | Optional constraints when using fixed placement: you can instruct the UI to restrict movement in one or both axes.                                                                                                 |
| placement?   | "fixed" \| "floating"       | Whether to float the element over the UI, so that it does not move with the content (floating), or to place the element onto the canvas, so that it moves/zooms with the content (fixed). Floating is the default. |
| position?    | [PointXY]()                 | For floating placement, this is a point relative to the viewport origin. for fixed placement, this is a point relative to the canvas origin. Defaults to 0,0.                                                      |
