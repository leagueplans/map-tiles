# Map tiles for League Plans

Map imagery for the map on [League Plans](https://www.leagueplans.com), served from this
repository's `docs/` folder by GitHub Pages at `https://www.leagueplans.com/map-tiles/`.

The tiles are rendered from the Old School RuneScape game cache, as archived by
[OpenRS2](https://archive.openrs2.org), using RuneLite's
[cache library](https://github.com/runelite/runelite/tree/master/cache).

## Layout

`docs/<plane>/<zoom>/<x>_<y>.png`, served as `<plane>/<zoom>/<x>_<y>.png`: 256 px tiles in
Leaflet's tile scheme for a simple coordinate system where one map unit is one game tile.
At zoom 2 a tile is one 64 × 64 region at 4 px per game tile, with `x` the region's x and
`y` minus one more than the region's y. Each zoom below halves the scale. Only tiles with
something on them exist.

Tile paths depend only on game coordinates, so a new render replaces images in place and never
moves anything.

## Attribution

Created using intellectual property belonging to Jagex Limited under the terms of Jagex's Fan
Content Policy. This content is not endorsed by or affiliated with Jagex.
