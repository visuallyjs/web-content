GroupData

The default type that represents a group in a dataset to load or a saved dataset. While there are no specific requirements for the entries in groups data, the default configuration expects that you will at the minimum have provided an `id`. Groups have an associated `type`, which VisuallyJs will set to "default" in the absence of you providing one; as you start to build more complex interfaces with VisuallyJs you will want to provide the `type` member.

`Record<string,any>`
