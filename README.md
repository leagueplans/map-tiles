# Map tiles for leagueplans

Map imagery for the map on [leagueplans](https://www.leagueplans.com), served from this repository's `docs/` folder by GitHub Pages at `https://www.leagueplans.com/map-tiles/`.

The tiles are rendered from the Old School RuneScape game cache, as archived by [OpenRS2](https://archive.openrs2.org), using RuneLite's [cache library](https://github.com/runelite/runelite/tree/master/cache).

## Layout

`docs/<plane>/<zoom>/<x>_<y>.png`, served as `<plane>/<zoom>/<x>_<y>.png`: 256 px tiles in Leaflet's tile scheme for a simple coordinate system where one map unit is one game tile. At zoom 2 a tile is one 64 × 64 region at 4 px per game tile, with `x` the region's x and `y` minus one more than the region's y. Each zoom below halves the scale. Only tiles with something on them exist.

Tile paths depend only on game coordinates, so a new render replaces images in place and never moves anything.

`docs/index.json` lists every tile so that the deployed map can avoid requesting tiles which don't exist, and `docs/places.json` lists the place names from the game's world map.

## Updates

The [Update the map](.github/workflows/update-map.yml) workflow runs every Thursday, after the game's weekly update, and can be run by hand. It renders the game's newest cache with the renderer in the [leagueplans repository](https://github.com/leagueplans/leagueplans.github.io/tree/master/maprender), and opens a pull request with the tiles whose pixels changed and a report of what changed. Merging the pull request publishes them. A run that changes nothing opens no pull request.

The report links to an overview: the whole map with the regions that changed highlighted, saved with the workflow run. Tile sets should be validated before merging, as it is possible for an incompatible cache library to produce partial tile sets from a cache. The [renderer's README](https://github.com/leagueplans/leagueplans.github.io/blob/master/maprender/README.md#the-cache-library) has recommendations for how to handle this scenario.

The render runs third-party code on a cache from a third party's archive, so it has no write access to the repository. A second job checks that the render holds only tiles, `index.json`, `places.json`, `.nojekyll` and `CNAME` before opening the pull request, since anything else in `docs/` would be served from the same site as the app. Files added to `docs/` by hand get no such check.

## Attribution

Created using intellectual property belonging to Jagex Limited under the terms of Jagex's [Fan Content Policy](https://legal.jagex.com/docs/policies/fan-content-policy). This content is not endorsed by or affiliated with Jagex.
