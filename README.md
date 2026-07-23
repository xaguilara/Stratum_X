# Stratum X - Drone Route Viewer v10 ENGLISH VERSION

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


SPANISH VERSION

[Stratum X - resumen.md](https://github.com/user-attachments/files/30287503/Stratum.X.-.resumen.md)
# Resumen de la pagina: Stratum X version 10

## Archivos revisados

- `Stratum X.dc.html`: contiene la interfaz, estilos, plantilla declarativa y logica principal de la aplicacion.
- `support.js`: runtime generado que monta el documento `.dc.html`, interpreta plantillas y conecta React/ReactDOM.

## Descripcion general

**Stratum X** es una aplicacion web tipo **Geospatial Route Viewer** para visualizar y analizar rutas geoespaciales de drones. La pagina muestra un mapa interactivo a pantalla completa con una interfaz tecnica tipo HUD, pensada para operaciones de vuelo, inspeccion de rutas, levantamientos, puntos de interes, zonas restringidas y gestion de capas geograficas.

La version 10 mantiene el enfoque operativo de las versiones anteriores y refuerza la herramienta de medicion: permite crear mediciones multipunto, ajustar puntos a vertices existentes, arrastrar puntos ya creados, cerrar/finalizar con doble clic y calcular area cuando hay tres o mas puntos.

## Interfaz principal

La pagina se organiza alrededor de un mapa Leaflet de pantalla completa. Encima del mapa aparecen:

- Barra superior con marca `STRATUM X`, version `v1.2`, menu de pines, buscador, selector de tema, boton de importacion y perfil.
- Panel lateral de capas.
- Inspector de elementos seleccionados.
- Barra de herramientas vertical para zoom, ajuste de vista, mapas base, medicion, graticula y reset.
- Pie de pantalla con coordenadas, escala, sistema de referencia, estado de medicion, numero de capas y creditos del mapa base.
- HUD opcional con vineta, esquinas y reticula central.

## Mapa y mapas base

La aplicacion usa Leaflet como motor de mapa. Permite:

- Hacer zoom y alejar.
- Ajustar vista a todos los datos cargados.
- Recentrar la mision.
- Ver coordenadas en tiempo real.
- Mostrar escala dinamica.
- Activar o desactivar graticula.
- Ver la referencia `WGS 84 EPSG:4326`.

Mapas base disponibles:

- Dark Matter
- Positron
- Voyager
- Satellite
- Terrain

El mapa `Satellite` agrega etiquetas de referencia desde Esri. Las preferencias del mapa base se pueden guardar localmente.

## Gestion de capas

El panel `LAYERS` permite administrar datos geoespaciales cargados o generados por el dataset demo. Cada capa puede:

- Activarse o desactivarse.
- Cambiar de color.
- Renombrarse.
- Reordenarse por arrastre.
- Eliminarse.
- Ajustar su opacidad.
- Cambiar la forma de marcadores cuando contiene puntos.

El panel tambien muestra conteos y metricas de capas visibles:

- Puntos.
- Lineas.
- Poligonos.
- Longitud total de lineas.
- Area total de poligonos.

Unidades disponibles:

- Longitud: `m`, `km`, `ft`, `mi`.
- Area: `m2`, `ha`, `ac`, `km2`.

## Importacion de datos

El modal `IMPORT LAYERS` permite arrastrar archivos o seleccionarlos desde el dispositivo.

Formatos soportados por la implementacion:

- `.KML`
- `.KMZ`

El texto de ayuda tambien menciona GeoJSON, pero el flujo de codigo revisado extrae y procesa KML/KMZ. Para KMZ usa `JSZip`; para KML usa `@mapbox/togeojson` para convertirlo a GeoJSON interno.

Al importar, la aplicacion:

- Lee uno o varios archivos.
- Extrae el KML si el archivo es KMZ.
- Convierte geometria KML a GeoJSON.
- Crea capas con puntos, lineas y poligonos.
- Calcula longitud y area.
- Limpia propiedades KML no relevantes.
- Asigna colores automaticamente.
- Ajusta la vista al conjunto de datos.
- Reporta errores por archivo cuando algo falla.

## Dataset de ejemplo

La pagina incluye un dataset demo cargable desde el panel lateral. Contiene cuatro capas:

- **Mission Alpha**: levantamiento tipo orthomosaic con poligono de area, ruta de vuelo, waypoints y punto Home/Takeoff.
- **Mission Bravo**: ruta perimetral cerrada con waypoints, altitud y parametros de vuelo.
- **Ground Assets**: puntos de interes como Ground Control Station, Charging Dock, Visual Observer e Inspection Target.
- **Restricted Zone**: zona restringida/no-fly representada como poligono con tooltip permanente.

El resumen de mision incluye distancia, area de survey, waypoints y tiempo estimado.

## Inspector de elementos

Al seleccionar una geometria del mapa se abre un inspector con:

- Nombre del elemento.
- Capa asociada.
- Tipo de geometria: punto, linea o poligono.
- Archivo fuente u origen.
- Metricas especificas.
- Propiedades del elemento.
- Coordenadas en formato abreviado.
- Accion `ZOOM TO`.
- Accion `EDIT` para lineas y poligonos.
- Boton visual `EXPORT`, aunque no se observa una funcion de exportacion conectada en el codigo revisado.

## Edicion de geometria

La pagina usa Leaflet-Geoman para editar vertices de lineas y poligonos seleccionados. Durante la edicion aparece una barra inferior con:

- Estado `EDITING VERTICES`.
- Tipo de geometria editada.
- Longitud o area actualizada en vivo.
- Acciones `CANCEL` y `SAVE`.

Al guardar, se actualizan las coordenadas, metricas y valores acumulados de la capa. Al cancelar, la geometria vuelve a su estado original.

## Medicion avanzada

La version 10 incorpora una herramienta de medicion mas completa:

- Se activa desde la barra vertical con el boton `Measure`.
- Permite hacer clic para crear puntos de medicion.
- Ajusta puntos a vertices existentes si estan cerca.
- Dibuja una linea punteada entre puntos.
- Si hay tres o mas puntos, dibuja un poligono semitransparente y calcula area.
- Los puntos de medicion se pueden arrastrar.
- Al soltar un punto arrastrado, vuelve a intentar ajustar a vertices cercanos.
- El doble clic finaliza la medicion.
- El pie de pantalla muestra distancia, area cuando aplica y numero de puntos.

Esta herramienta bloquea temporalmente otros modos como soltar pines para evitar conflictos.

## Pines manuales

La aplicacion permite soltar pines manuales en el mapa o desde resultados del buscador. Los pines pueden:

- Tener nombre editable.
- Moverse arrastrandolos.
- Asociarse a la capa activa o quedar sin asignar.
- Cambiar de forma.
- Seleccionarse, acercarse o eliminarse.
- Agruparse por capa dentro del menu de pines.
- Limpiarse todos a la vez.

Formas disponibles:

- Pin
- Circle
- Star
- Flag
- Triangle
- Square
- Diamond
- Cross

## Busqueda geografica

El buscador acepta:

- Nombres de lugares.
- Coordenadas en formato latitud/longitud.

Para busquedas por nombre consulta Nominatim de OpenStreetMap. Cada resultado permite:

- Volar hacia la ubicacion.
- Crear un pin en esa ubicacion.

## Perfil y preferencias

El menu de perfil simula la cuenta:

- Usuario: Alex Rivera.
- Plan: PRO.
- Correo: alex.rivera@stratum.io.

Desde ahi se guardan preferencias en `localStorage`:

- Tema oscuro o claro.
- Mapa base por defecto.
- Unidad de longitud por defecto.
- Unidad de area por defecto.

Tambien existe un boton de reset para devolver el mapa y unidades a los valores guardados.

## Dependencias externas

La pagina depende de:

- Leaflet para mapas.
- Leaflet-Geoman para edicion de vertices.
- JSZip para leer archivos KMZ.
- `@mapbox/togeojson` para convertir KML a GeoJSON.
- Google Fonts para IBM Plex Sans e IBM Plex Mono.
- Proveedores de tiles CARTO, Esri y OpenTopoMap.
- Nominatim de OpenStreetMap para busqueda geografica.

## Rol de support.js

`support.js` no contiene la logica especifica del visor Stratum X. Es un runtime generado que:

- Busca el bloque `<x-dc>`.
- Extrae plantilla, propiedades y script embebido.
- Crea el contenedor raiz.
- Monta el componente con React.
- Resuelve expresiones `{{ ... }}`.
- Implementa estructuras declarativas como `sc-if` y `sc-for`.
- Aplica estilos base y soporte de renderizado.

En resumen, `support.js` es la infraestructura que permite que `Stratum X.dc.html` funcione como una aplicacion interactiva.

## Resumen final

Stratum X version 10 es un visor geoespacial avanzado para rutas y misiones de drones. Combina mapa interactivo, gestion de capas, importacion KML/KMZ, dataset demo, metricas automaticas, inspeccion y edicion de geometria, busqueda geografica, pines manuales, preferencias persistentes y una herramienta de medicion mejorada que calcula distancia y area con puntos editables y ajuste a vertices.
