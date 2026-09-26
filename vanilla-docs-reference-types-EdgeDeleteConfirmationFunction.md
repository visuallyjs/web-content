EdgeDeleteConfirmationFunction

Definition of the function you can provide as `deleteConfirm` on an edge definition. VisuallyJs gives you the edge to be possibly deleted and the pointer event that instigated the deletion. If you wish to delete the edge you must invoke the `proceed()` function.

`(params:{
  e:Event,
  edge:Edge
}, proceed:() => any) => any`
