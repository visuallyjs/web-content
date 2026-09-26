# UI Data & State

The `Surface` component provides `save` and `load` methods that allow you to persist and restore the entire state of your canvas, including the underlying data model, the UI's pan/zoom state, and the state of any registered plugins/components, such as the `Inspector`. You'll need to access the surface to use these methods programmatically - expand the section below for details.

How to access the surface

## Saving data & state[​](#saving-data--state "Direct link to Saving data & state")

The [save]() method is used to capture a complete snapshot of the current `Surface` state. It returns a JSON object (conforming to the `SurfaceSaveData` interface) containing:

* **Graph Data**: The full dataset of all nodes, groups, edges, and ports that have been loaded into the underlying model.
* **UI State**: The current pan and zoom configuration of the `Surface` viewport, including the pan position (x, y) and the zoom transform origin. This ensures that the visual position of the canvas is preserved.
* **Plugin/Component State**: The state of any plugins or components that have registered a data hook. Out of the box, the `Inspector` component uses this capability, savings its context (such as recently used colors) in the saved data under the `inspectorContext` key.

```typescript
// Example of saving the surface state
const currentState = surface.save();

// The `currentState` object now holds the complete snapshot.
// This can be serialized to JSON and stored.
const jsonState = JSON.stringify(currentState);

```

SurfaceSaveData

Definition of the payload returned from the Surface's `save` method.

| Name            | Type        | Description                                             |
| --------------- | ----------- | ------------------------------------------------------- |
| data            | any         | Data exported from the model                            |
| pan             | [PointXY]() | The current pan position of the surface canvas          |
| transformOrigin | [PointXY]() | The current position of the surface's transform origin. |
| zoom            | number      | The current zoom level                                  |

## Loading data & state[​](#loading-data--state "Direct link to Loading data & state")

The [load]() method is the counterpart to `save()`. It takes a state object (of type `SurfaceSaveData`) and uses it to restore the `Surface` to a previously saved state. The `load` method restores:

* **Graph Data**: It clears the current model and loads the graph data from the provided state object.
* **UI State**: After the data is loaded, it restores the pan and zoom of the `Surface` viewport to their saved values.
* **Plugin/Component State**: The data is then passed to each of the registered data hooks, which may load their own data and take action as necessary.

```typescript
// Example of loading a saved state
const savedJsonState = getMySavedState(); // retrieve the stored JSON string
const stateToLoad = JSON.parse(savedJsonState);

surface.load(stateToLoad, () => {
    console.log("Surface has been restored to its previous state.");
});

```

## Data Hooks[​](#data-hooks "Direct link to Data Hooks")

The save/load mechanism is extensible, allowing you to include custom data from your own components in the process. This is achieved through the `Surface`'s [registerDataHook]() method. If you have a custom component that manages its own state and you want this state to be persisted along with the rest of the diagram, you can call this method on a surface and register your interest in adding data to the saved data and of loading data from a newly loaded dataset.

The `Inspector` uses this mechanism out of the box - this is the code:

```javascript
this.$ui.registerDataHook({
    load:(d:SurfaceSaveData) => {
        // extract inspector context from the load data
        const c = d["inspectorContext"]
        // inspector-specific code...your code will be different
        if (c != null && c.recentColors != null) {
            this.updateContext(INSPECTOR_CONTEXT_RECENT_COLORS, c.recentColors.slice())
        }
    },
    save:(d:SurfaceSaveData) => {
        // store the inspector context on the save data
        d["inspectorContext"] = Object.assign({}, this.$context)
    }
})

```
