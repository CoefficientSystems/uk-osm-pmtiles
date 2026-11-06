# UK OpenStreetMap vector tiles (PMTiles)

A UK extract of the [Protomaps](https://protomaps.com) basemap: OpenStreetMap vector tiles in a single
[PMTiles](https://docs.protomaps.com/pmtiles/) file, for offline map display with `pmtiles serve`.

The file is published as a release asset, not committed to this repo:

https://github.com/CoefficientSystems/uk-osm-pmtiles/releases/download/uk-z14-20261104/uk.pmtiles

## The file

| | |
|---|---|
| File | `uk.pmtiles` |
| Size | 1,494,436,508 bytes (1.5 GB) |
| sha256 | `593f9b94bc70f22109049031385c3e281bb43d8c0754a2a35387e20736a0b6d2` |
| Area | bbox `-8.75,49.8,1.9,60.95` (west, south, east, north) |
| Zoom | 0 to 14 |
| Tiles | Mapbox Vector Tiles (mvt), gzip compressed |
| Schema | Protomaps basemap schema v4 (basemap version 4.15.2) |
| OSM data as of | 2026-11-04 04:00 UTC |

## How it was made

Source: the Protomaps daily planet build of 2026-11-04, `https://build.protomaps.com/20261104.pmtiles`.

Cut with [go-pmtiles](https://github.com/protomaps/go-pmtiles) v1.31.2 (`go-pmtiles-1.31.2_Darwin_arm64.zip`,
sha256 checked against the GitHub release digest before use):

```sh
pmtiles extract https://build.protomaps.com/20261104.pmtiles uk.pmtiles --bbox=-8.75,49.8,1.9,60.95 --maxzoom=14
```

`pmtiles verify uk.pmtiles` passed on the result.

## Using it

Check the download first. On Windows (PowerShell):

```powershell
(Get-FileHash .\uk.pmtiles -Algorithm SHA256).Hash
```

The result should equal the sha256 above (PowerShell prints it in upper case). Then serve the folder holding the file:

```sh
pmtiles serve .
```

The tiles are then at `http://localhost:8080/uk/{z}/{x}/{y}.mvt`, with TileJSON at `http://localhost:8080/uk.json`.

## Licence and attribution

Map data © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright), available under the
[Open Database Licence](https://opendatacommons.org/licenses/odbl/). See https://www.openstreetmap.org/copyright.

Basemap tiles built by [Protomaps](https://protomaps.com).

Any map displaying these tiles must show the OpenStreetMap attribution.
