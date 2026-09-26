# \<ImageBackgroundComponent/>

This component configures sets an image background for a `SurfaceComponent` or `PaperComponent`, and pastes it at the surface/paper origin.

## Usage[​](#usage "Direct link to Usage")

Declare the image background component inside a `SurfaceComponent`, `SurfaceProvider`, `PaperComponent` or `PaperProvider` and provide it a url:

```jsx
export default function MyComponent() {
    
    return <SurfaceComponent renderOptions={...} data={...}>
        <ImageBackgroundComponent url="/img/351032562.jpg"/>
    </SurfaceComponent>
}

```

## Zoom to background[​](#zoom-to-background "Direct link to Zoom to background")

To show the entire background image, invoke `zoomToBackground()` on a surface:

```jsx
export default function ZoomToBackground() {

    const ref = useRef(null)

    function ztb() {
        ref.current.getSurface().zoomToBackground()
    }

    return <div className="vjs-inline-example">
        <SurfaceComponent ref={ref} data={{nodes:[
                {id:"1", left:50, top:50},
                {id:"2", left:250, top:150},
            ]}} viewOptions={{
            nodes:{
                default:{
                    jsx:(ctx) => <div style={{width:"80px", height:"60px", backgroundColor:"white"}}>{ctx.data.id}</div>
                }
            }
        }}>
            <ImageBackgroundComponent url="https://static.visuallyjs.com/img/cow.jpg"/>
        </SurfaceComponent>
        <button style={{position:"absolute", top:"1rem", right:"1rem", zIndex:"60"}} onClick={() => ztb()}>Zoom to background</button>
    </div>
}

```

Zoom to background

## Props[​](#props "Direct link to Props")

ImageBackgroundComponentProps

Props for the image background component.

| Name | Type   | Description                  |
| ---- | ------ | ---------------------------- |
| url  | string | The URL of the image to load |
