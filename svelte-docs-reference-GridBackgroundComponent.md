# \<GridBackgroundComponent/>

This component configures a grid background for a `SurfaceComponent` or `PaperComponent`.

## Usage[​](#usage "Direct link to Usage")

### Default settings[​](#default-settings "Direct link to Default settings")

Declare the grid background component inside a `SurfaceComponent`, `SurfaceProvider`, `PaperComponent` or `PaperProvider`:

```html
<SurfaceComponent renderOptions={renderOptions}>
    ...
	<GridBackgroundComponent/>
</SurfaceComponent>

```

In this example, the grid will use the default settings, which is a grid of size 50. No grid is imposed on the movement or size of vertices - this setup is useful for a basic visual effect.

### Surface grid[​](#surface-grid "Direct link to Surface grid")

The grid background will paint itself according to the `grid` specified for a surface if you set one:

```html
<script>
    const renderOptions = {
		grid:{
			size:{width:20, height:20 }
		}
    }
</script>
<SurfaceComponent url={url} renderOptions={renderOptions}>
	...
	<GridBackgroundComponent/>
</SurfaceComponent>

```

## Props[​](#props "Direct link to Props")

GridBackgroundComponentProps

Props for the GridBackgroundComponent

| Name              | Type         | Description                                                                                                                                                                                                                                                                                                                                         |
| ----------------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| autoShrink?       | boolean      | Defaults to true, and instructs the grid that if the grid has grown beyond any minimum value set in either axis, if the content bounds subsequently shrink in that axis below the minimum, the grid should shrink back to the minimum. If you set this to false the grid will never shrink back to its minimum values once they have been exceeded. |
| dotRadius?        | number       | The radius for dots representing grid positions (when gridType id GridTypes.dotted). Defaults to 2.                                                                                                                                                                                                                                                 |
| grid?             | [Grid]()     | The grid to use. This is optional; if you do not supply one the background will attempt to read the grid definition from the Surface. If that is also not set then a default grid of 50x50 pixels will be used.                                                                                                                                     |
| gridType?         | [GridType]() | Type of grid - lines or dots. Defaults to lines.                                                                                                                                                                                                                                                                                                    |
| maxHeight?        | number       | The maximum height for the grid. The value you provided is divided by 2 and then the grid is guaranteed to never exceed the range of (-maxHeight / 2) - (maxHeight / 2). maxHeight takes precedence over minHeight.                                                                                                                                 |
| maxWidth?         | number       | The maximum width for the grid. The value you provided is divided by 2 and then the grid is guaranteed to never exceed the range of (-maxWidth / 2) - (maxWidth / 2). maxWidth takes precedence over minWidth.                                                                                                                                      |
| minHeight?        | number       | The minimum height for the grid. The value you provided is divided by 2 and then the grid is guaranteed to always at least span the range of (-minHeight / 2) - (minHeight / 2). Defaults to 20 000.                                                                                                                                                |
| minWidth?         | number       | The minimum width for the grid. The value you provided is divided by 2 and then the grid is guaranteed to always at least span the range of (-minWidth / 2) - (minWidth / 2). Defaults to 20 000.                                                                                                                                                   |
| showBorder?       | boolean      | Whether or not to show a thick border around the entire background. Defaults to false.                                                                                                                                                                                                                                                              |
| showTickMarks?    | boolean      | Defaults to false. If true, the grid will also draw tick marks between the grid lines.                                                                                                                                                                                                                                                              |
| tickDotRadius?    | number       | The radius for dots representing grid tick marks (when gridType id GridTypes.dotted). Defaults to 1.                                                                                                                                                                                                                                                |
| tickMarksPerCell? | number       | Number of tick marks to draw per cell. Defaults to 2.                                                                                                                                                                                                                                                                                               |
| visible?          | boolean      | Whether or not the background is initially visible. Defaults to true.                                                                                                                                                                                                                                                                               |
