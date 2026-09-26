# Image Background

HTML Tag

**vjs-image-background**

This component configures sets an image background for a `SurfaceComponent` or `PaperComponent`, and pastes it at the surface/paper origin.

## Usage[​](#usage "Direct link to Usage")

Declare the image background component inside a `SurfaceComponent`, `SurfaceProvider`, `PaperComponent` or `PaperProvider` and provide it a url:

```html
<vjs-surface [renderOptions]="renderOptions">
	...
	<vjs-image-background url="/img/351032562.jpg"/>
</vjs-surface>

```

## Definition[​](#definition "Direct link to Definition")

### Inputs[​](#inputs "Direct link to Inputs")

| Name | Type   | Description     |
| ---- | ------ | --------------- |
| url  | string | The url to load |
