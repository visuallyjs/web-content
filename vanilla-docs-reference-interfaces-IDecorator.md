IDecorator

Base interface for the methods a decorator needs to provide.

| Name         | Type    | Description                                                                                                                                                                                                                                                                                                                             |
| ------------ | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| incremental? | boolean | When true, indicates that this Decorator updates its associated elements incrementally with each call. When false, the<br />surface will clear everything associated with this decorator prior to invoking `decorate`. The default value for this is false,<br />meaning the surface will clear everything prior to calling `decorate`. |
| reset        |         | no description                                                                                                                                                                                                                                                                                                                          |
