# Portland Sanborn 1901

The 1901 Sanborn Fire Insurance Map of Portland, Oregon, Volume 1, georeferenced by hand, sheet by sheet, and published as
[IIIF Georeference Annotations](https://iiif.io/api/extension/georef/) for [Allmaps](https://allmaps.org).

**Map:** <https://anthonyblackham.com/portland-sanborn-1901/>

All 119 scanned sheets are placed (sheet 67 was never scanned by the Library of Congress). Nothing is hosted here except
the georeferencing itself: the map and every viewer that reads these files fetch the scans directly from the
[Library of Congress](https://www.loc.gov/collections/sanborn-maps/) IIIF image service and warp them in the browser.

## Using the annotations

| What | Where |
|---|---|
| Every sheet, panel and block in one AnnotationPage | [`annotations/portland_1901_v1.iiif.json`](annotations/portland_1901_v1.iiif.json) |
| One AnnotationPage per sheet | [`annotations/sheets/sheet-NNN.json`](annotations/sheets/) |
| Where each sheet or panel landed, with its accuracy | [`data/sheets.geojson`](data/sheets.geojson), [`data/accuracy.csv`](data/accuracy.csv) |
| The volume's key-page sheet outlines (approximate, all 120) | [`data/sheet_index.geojson`](data/sheet_index.geojson) |

Open a sheet in the Allmaps Viewer by passing its file's URL, for example sheet 79:

    https://viewer.allmaps.org/?url=https://anthonyblackham.com/portland-sanborn-1901/annotations/sheets/sheet-079.json

The whole volume works the same way with `annotations/portland_1901_v1.iiif.json`. In code, add either file to an
Allmaps plugin ([MapLibre](https://github.com/allmaps/allmaps/tree/main/packages/maplibre),
[Leaflet](https://github.com/allmaps/allmaps/tree/main/packages/leaflet),
[OpenLayers](https://github.com/allmaps/allmaps/tree/main/packages/openlayers)); `index.html` is a small MapLibre example.

## How it was made

- **Control:** every sheet was georeferenced by hand in QGIS against Multnomah County tax lots (EPSG:2913, Oregon North ft):
  1,844 ground control points in all, on block and lot corners that survive.
- **Transform:** a Helmert (similarity) transform per sheet, so nothing is stretched or bent. The sheets come out at about
  0.161-0.165 ft per scan pixel, the drawing's 50 ft to the inch.
- **Downtown:** where Sanborn drew streets off their true width (cross streets on sheets 47, 48 and 57 are 42-60 ft too wide,
  1st St about 187 ft) a single fit can't hold every block, so those sheets carry one fit per drawn block: a whole-sheet
  annotation underneath and one block annotation, masked to the block, on top (226 block annotations on 29 sheets and panels).
- **Panels and insets:** sheets with several panels, or insets drawn somewhere else, have one annotation per panel, each with
  its own fit and masked to its outline (44 panels).
- **Masks:** each annotation is cut to the mapped area of its sheet, panel or block.

## Accuracy

| | Count | Notes |
|---|---|---|
| One Helmert per sheet or panel | 109 | median 1.4 ft rms at the points, 90% under 2.3 ft |
| Per-block fits | 29 | worst block within about 5 ft |
| Approximate insets | 4 | far-off insets with no surviving streets, placed from other evidence (below) |
| Not placed | 1 | sheet 29's inset, the Western Packing Co. cannery at Linnton: only a riverbank, since filled |

Residuals only measure agreement at the points. Away from them, expect a few feet on street-grid sheets and more on
riverfront sheets where control is sparse (notes per sheet in `data/accuracy.csv`; the `approximate` column marks the guesses).

**Approximate insets:**

- **Sheet 2, Portland Clay Co. brick yard:** from the key-page box, the Riverview Abbey land history and county survey
  35163 (the clay pit on Stephens Creek); 100-300 ft.
- **Sheet 2, Palatine Hill pumping station:** today 10940 S Riverwood Rd, fitted to the shore and rail grade in the 1925 aerial; about 100 ft.
- **Sheet 30, Fleischman's and Adams' slaughterhouses:** on St. Helens Road by the north-west arm of Guild's Lake, from
  the USGS 1896 Portland sheet; about 50 ft across the road, 200 ft or more along it.
- **Sheet 31, Multnomah County Hospital and Poor Farm:** the Hillside Farm in today's Washington Park, from the 1925
  aerial (its loop drive and last buildings); 50-150 ft.

**Known weak spots:** sheet 31's tannery inset (two close points; scale about 8% high) and the river end of sheet 44
(all points on its west edge) could use one more point each.

## Sources and credits

- Sanborn Map Company, *Insurance Maps of Portland, Oregon*, Vol. 1 (1901), scans from the Library of Congress
  Geography and Map Division (public domain).
- Multnomah County tax lots; Portland Maps 1925 aerial scans; USGS 1896 Portland topographic sheet.
- [Allmaps](https://allmaps.org) for the warping, [MapLibre](https://maplibre.org) and [CARTO](https://carto.com) basemaps for the map page.

## License

The annotations and data are released under [CC0 1.0](LICENSE): use them for anything, no permission needed.
