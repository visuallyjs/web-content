TilingStrategy

Defines how the tiles are arranged in a tiled background layer. With `TILING_STRATEGY_LOGARITHMIC` each layer is assumed to have a maximum of (2^level+1) tiles in each axis (for instance at level 0, 2 tiles). This setup is how apps like Google maps arrange their tiles. With `TILING_STRATEGY_ABSOLUTE` tiling, the number of tiles in each axis is computed as the size of the image in that axis divided by the tile size in that axis. Thus, for each zoom level, there are the same number of tiles.

`TILING_STRATEGY_ABSOLUTE | TILING_STRATEGY_LOGARITHMIC`
