FontSpec

Specs for a font. The default values depend on the context.

| Name    | Type           | Description                                                                                                    |
| ------- | -------------- | -------------------------------------------------------------------------------------------------------------- |
| family? | string         | Font family to use.                                                                                            |
| size?   | number         | Size of the font. Default value depends on the context this spec occurs in.                                    |
| style?  | [FontStyle]()  | Font style to use. Default value depends on the context this spec occurs in.                                   |
| weight? | [FontWeight]() | Font weight to use (e.g., "normal", "bold", "100", "300"). Defaults to null, which browsers treat as "normal". |
