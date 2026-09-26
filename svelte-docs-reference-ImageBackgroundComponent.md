# \<ImageBackgroundComponent/>

This component configures sets an image background for a `SurfaceComponent` or `PaperComponent`, and pastes it at the surface/paper origin.

## Usage[​](#usage "Direct link to Usage")

Declare the image background component inside a `SurfaceComponent`, `SurfaceProvider`, `PaperComponent` or `PaperProvider` and provide it a url:

```html
<script>
</script>
<SurfaceComponent renderOptions={renderOptions}>
	...
	<ImageBackgroundComponent url="/img/351032562.jpg"/>
</SurfaceComponent>

```

## Props[​](#props "Direct link to Props")

ImageBackgroundComponentProps

Props for the ImageBackgroundComponent

| Name | Type   | Description               |
| ---- | ------ | ------------------------- |
| url  | string | URL of the image to load. |
