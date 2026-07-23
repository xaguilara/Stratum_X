# Stratum X - Drone Route Viewer v10

Stratum X is a browser-based geospatial route viewer designed for drone mission review, route analysis, KML/KMZ imports, layer management, manual pins, measurement workflows, and geometry inspection.

The application runs as a self-contained `.dc.html` page powered by a generated `support.js` runtime. Its main experience is a full-screen Leaflet map with technical HUD-style controls for operational geospatial work.

## Main Features

- Full-screen interactive Leaflet map.
- Dark and light themes.
- Multiple basemap options: Dark Matter, Positron, Voyager, Satellite, and Terrain.
- KML/KMZ import with automatic layer creation.
- Layer visibility, color, opacity, renaming, ordering, and removal.
- Feature inspector for points, lines, and polygons.
- Vertex editing for lines and polygons through Leaflet-Geoman.
- Advanced measurement mode with draggable points, vertex snapping, distance, and area calculations.
- Manual dropped pins with editable labels and custom marker shapes.
- Geographic search using OpenStreetMap Nominatim.
- Mission summary and GIS metrics for visible layers.
- Persistent local preferences through `localStorage`.

## Version 10 Highlights

Version 10 improves the measurement workflow:

- Click to add measurement points.
- Drag measurement points after placing them.
- Snap measurement points to nearby existing vertices.
- Double-click to finish a measurement.
- Show total distance.
- Show polygon area when the measurement has three or more points.
- Display live measurement details in the footer.

The footer also clarifies the coordinate reference as `WGS 84 EPSG:4326`.

## Files

- `Stratum X.dc.html`: main application file with the UI, styles, template, and viewer logic.
- `support.js`: generated runtime that mounts the `.dc.html` document and powers the declarative template system.
- `uploads/`: image assets used by the page.
- `screenshots/`: screenshot references for the interface.
- `Stratum X - resumen.md`: Spanish summary of the page contents.

## Map Experience

The map includes:

- Zoom in and zoom out controls.
- Fit-to-data view.
- Recenter mission control.
- Basemap selector.
- Measurement tool.
- Graticule toggle.
- Saved-default reset control.
- Live coordinate readout.
- Dynamic scale bar.
- Layer and feature counters.

The app uses `WGS 84 EPSG:4326` as its coordinate reference display.

## Supported Basemaps

- Dark Matter
- Positron
- Voyager
- Satellite
- Terrain

The satellite basemap uses Esri imagery and adds an Esri reference label layer.

## Layer Management

The `LAYERS` panel allows users to:

- Toggle layer visibility.
- Change layer color.
- Rename layers.
- Reorder layers by dragging.
- Remove layers.
- Adjust opacity.
- Change marker shape for point layers.
- Focus the map on a selected layer.

The panel also shows GIS metrics for visible layers:

- Points.
- Lines.
- Polygons.
- Total line length.
- Total polygon area.

Available length units:

- `m`
- `km`
- `ft`
- `mi`

Available area units:

- `m2`
- `ha`
- `ac`
- `km2`

## Data Import

The import modal supports file selection and drag-and-drop upload for:

- `.KML`
- `.KMZ`

The interface text also mentions GeoJSON, but the implemented import flow processes KML/KMZ files. KMZ files are unpacked with `JSZip`, and KML content is converted with `@mapbox/togeojson`.

During import, the app:

- Reads one or more files.
- Extracts KML from KMZ archives.
- Converts KML to GeoJSON.
- Builds point, line, and polygon layers.
- Calculates feature counts.
- Calculates line length and polygon area.
- Assigns an automatic layer color.
- Fits the map view to imported data.
- Reports per-file errors when import fails.

## Demo Dataset

The page includes a built-in sample dataset with four layers:

- **Mission Alpha**: orthomosaic survey mission with survey extent, flight path, waypoints, and home/takeoff point.
- **Mission Bravo**: closed perimeter route with waypoints and flight parameters.
- **Ground Assets**: operational points of interest such as ground control station, charging dock, visual observer, and inspection target.
- **Restricted Zone**: no-fly or restricted airspace polygon with a permanent warning tooltip.

The mission summary shows:

- Distance.
- Survey area.
- Waypoints.
- Estimated time.

## Feature Inspector

Selecting a feature opens an inspector with:

- Feature name.
- Source layer.
- Geometry type.
- Source file.
- Feature metrics.
- Attached properties.
- Coordinate preview.
- Zoom-to-feature action.
- Geometry edit action for lines and polygons.

The inspector includes an `EXPORT` button in the UI, but no connected export behavior was found in the reviewed code.

## Geometry Editing

Line and polygon features can be edited with Leaflet-Geoman.

While editing, the app shows an `EDITING VERTICES` bar with:

- Geometry type.
- Live length or area value.
- `CANCEL` action.
- `SAVE` action.

Saving updates the geometry coordinates and related metrics. Canceling restores the original geometry.

## Measurement Tool

The measurement tool supports:

- Multipoint distance measurement.
- Area measurement when three or more points exist.
- Draggable measurement points.
- Snapping to nearby vertices.
- Double-click finish behavior.
- Live footer feedback.

The tool prevents conflicting actions such as dropping pins while measurement mode is active.

## Manual Pins

Users can drop pins directly on the map or from search results.

Pins support:

- Editable names.
- Drag repositioning.
- Layer assignment or unassigned status.
- Selection.
- Zoom-to-pin.
- Individual removal.
- Clear-all action.
- Shape customization.

Available pin shapes:

- Pin
- Circle
- Star
- Flag
- Triangle
- Square
- Diamond
- Cross

## Geographic Search

The search input accepts:

- Place names.
- Latitude/longitude coordinates.

Place search uses OpenStreetMap Nominatim. Results can be opened on the map or converted into dropped pins.

## Preferences

The profile menu includes a simulated user account:

- User: Alex Rivera
- Plan: PRO
- Email: alex.rivera@stratum.io

Preferences are saved locally on the device:

- Theme.
- Default basemap.
- Default length unit.
- Default area unit.

## External Dependencies

- Leaflet
- Leaflet-Geoman
- JSZip
- `@mapbox/togeojson`
- Google Fonts: IBM Plex Sans and IBM Plex Mono
- CARTO basemap tiles
- Esri imagery and labels
- OpenTopoMap tiles
- OpenStreetMap Nominatim search

## Role of `support.js`

`support.js` is a generated runtime. It is not the Stratum X application logic itself.

It handles:

- Locating the `<x-dc>` document block.
- Extracting the template, props, and embedded script.
- Creating the root container.
- Mounting the component with React.
- Resolving `{{ ... }}` expressions.
- Supporting declarative structures such as `sc-if` and `sc-for`.
- Applying runtime rendering support.

## Summary

Stratum X v10 is an advanced geospatial viewer for drone mission planning and review. It combines an interactive map, KML/KMZ imports, operational layer controls, feature inspection, geometry editing, manual pins, place search, persistent preferences, and an improved measurement system with distance, area, draggable points, snapping, and double-click completion.
