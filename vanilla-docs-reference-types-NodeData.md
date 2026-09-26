NodeData

The default type that represents a node in a dataset to load or a saved dataset. While there are no specific requirements for the entries in node data, the default configuration expects that you will at the minimum have provided an `id`. Nodes have an associated `type`, which VisuallyJs will set to "default" in the absence of you providing one; as you start to build more complex interfaces with VisuallyJs you will want to provide the `type` member.

`Record<string,any>`
