ModelUpdateFunction

Defines a function you can call from a vertex added callback to run some model updates that will be included in the same transaction as the one that just added the new vertex. You pass a function in to this method, which contains the model updates you wish to make. Your update function will be passed the UI, its model, and any `context` you provided as a second argument when you called doModelUpdate inside the vertex added callback.

`(updateFunction:(ui:BrowserUI, model:VisuallyJsModel, context:any) => any) => void`
