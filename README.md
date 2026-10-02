# Explorador de filtros ΔNDVI

Herramienta local para explorar cómo cada filtro (ΔBSI, pendiente, curvatura,
susceptibilidad, ΔNDVI final, DBSCAN) cambia la detección de movimientos en masa
y sus métricas por evento contra el inventario, y para validar candidatos uno a uno.

Proyecto SAMA, Universidad EAFIT.

## Contenido

| Archivo | Qué es |
|---|---|
| `notebooks/NDVI_mas_FIlters_6_Cisneros_object_P95.ipynb` | Notebook de detección (GEE). Las celdas 17–19 exportan las capas para el explorador. |
| `explorador/explorador_filtros_ndvi.html` | El explorador. Se abre en el navegador; no necesita servidor ni Python. |

## Uso

1. Correr el notebook completo. La **celda 17** genera `capas_explorador_<sitio>.json`
   (ΔNDVI, ΔBSI, pendiente, curvatura, DEM, susceptibilidad, RGB, inventario, OSM y municipios).
2. Abrir `explorador_filtros_ndvi.html` en Chrome, Firefox o Edge y arrastrar el `.json`.
   La **celda 18** lo abre automáticamente.
3. Para compartir con alguien sin Python: la **celda 19** genera un único
   `explorador_<sitio>_compartir.html` con los datos incluidos.

## Qué hace el explorador

- Compara ΔNDVI P90 / P95 / P99 y aplica la pila de filtros con switches y parámetros.
- Métricas por evento (TP, FN, recall, precisión, F1), idénticas a `metricas_por_evento()` del notebook;
  el encabezado indica si reproduce las etapas del notebook.
- Mapa con ortofoto Esri + hillshade ×1.5, drenajes y edificios OSM, inventario TP/FN.
- Validador de candidatos (clusters DBSCAN): ortofoto, RGB pre/post, ΔNDVI, hillshade,
  mapa de localización (Antioquia y municipio), atajos C / D / U, exportación CSV y GeoJSON.

## Datos

Los datos **no** están en el repositorio (`.gitignore`): inventario, rasters, `.json` exportados
y resultados de validación quedan locales. Las rutas de entrada están en la celda 17 del notebook.

La ortofoto se carga en línea desde Esri World Imagery (Esri, Maxar, Earthstar Geographics);
su fecha varía según la zona y no necesariamente corresponde al evento.
