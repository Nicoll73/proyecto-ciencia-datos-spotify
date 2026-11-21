# ¿Qué hace popular a una canción? Análisis de datos de Spotify

Proyecto final del curso de Ciencia de Datos.

## Integrantes
- Miguel Ángel Malagón Villarreal
- Nicoll Sofia Oyola Sanchez
- (Nombre del integrante 3, si aplica)

## Video de presentación
(Aquí va el enlace al video de 2 a 5 minutos, o se indica que está en la carpeta `video/`.)

## Descripción del proyecto
En este proyecto trabajamos con un conjunto de datos públicos de cerca de 33 mil canciones de Spotify ([TidyTuesday, enero de 2020](https://github.com/rfordatascience/tidytuesday/tree/master/data/2020/2020-01-21)). Los datos incluyen características de audio (danceability, energy, valence, tempo, etc.), la popularidad de cada canción y su género.

La pregunta que guía el trabajo es: **¿qué características de audio se relacionan con la popularidad de una canción y cómo varían según el género?**

El proyecto se desarrolla en tres etapas, una por cada módulo del curso.

## Estructura del repositorio
```
├── README.md
├── datos/            datos originales y datos limpios (.csv)
├── notebook/         cuaderno de Google Colab (.ipynb)
├── presentacion/     presentación de apoyo (.pptx) e imágenes
└── video/            video de presentación o enlace
```

## Avance por etapas
| Etapa | Módulo | Estado |
|---|---|---|
| 1 | Fundamentos y preparación de datos | Terminada |
| 2 | Módulo 2 | En desarrollo |
| 3 | Módulo 3 | En desarrollo |

### Etapa 1: Fundamentos y preparación de datos
Seleccionamos el dataset, exploramos sus variables y distribuciones, y lo limpiamos. Pasó de 32 833 filas y 23 columnas a 28 352 filas y 24 columnas. Estos fueron los principales problemas y lo que hicimos:

- **Nulos:** 5 filas sin nombre, artista ni álbum. Las eliminamos.
- **Duplicados:** una misma canción aparecía en varias playlists. Dejamos un registro por `track_id`.
- **Fechas:** había tres formatos distintos. Las pasamos a tipo fecha y creamos la columna `anio`.
- **Tipos de datos:** `key` y `mode` eran números; los convertimos a notas musicales y modo (mayor/menor). El género quedó como categoría.
- **Valores no válidos:** `tempo = 0` lo dejamos como nulo y la duración la pasamos a minutos.

El detalle con el código está en el notebook.

## Cómo reproducir el análisis
[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/miguelmalgon-sys/proyecto-ciencia-datos-spotify/blob/main/notebook/proyecto_ciencia_datos.ipynb)

Abrir `notebook/proyecto_ciencia_datos.ipynb` en [Google Colab](https://colab.research.google.com/) y ejecutar las celdas en orden. Si el repositorio no está clonado, el notebook descarga los datos directamente desde la fuente original.

##Etapa 2 · Estadística Descriptiva y Preprocesamiento (`spotify_songs_limpio.csv`)

|Variable|medios de comunicación|Mediana|Moda|Mínimo|Máximo|Rango|Varianza|Desv. Estándar|
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| `seguimiento_popularidad` |39.335|42.000|0.000|0.000|100.000|100.000|561.664|23.899|
| `capacidad de baile` |0,653|0,670|0,690|0.000|0,983|0,983|0,021|0,146|
| `energía` |0,698|0,722|0,833|0.000|1.000|1.000|0,034|0,184|
| `tempo` |120.962|121.994|127.992|35.477|239.440|203.963|726.055|26.945|
| `anio` |2011.054|2016.000|2019.000|1957|2020|63|126.111|11.230|
| `duración_min` |3.776|3.616|4.000|0,067|8.630|8.564|1.036|1.018|


|Género (`género_lista_de_reproducción`)|Popularidad (Media / Mediana)|Bailabilidad (Media / Mediana)|Energía (Media / Mediana)|
|:---|:---:|:---:|:---:|
| `estallido` |43.500 / 47.0|0,637 / 0,649|0,702 / 0,728|
| `latín` |42.616 / 47.0|0,712 / 0,727|0,710 / 0,731|
| `rap` |41.198 / 45.0|0,715 / 0,733|0,649 / 0,665|
| `r&b` |37.541 / 39.0|0,595 / 0,590|0,595 / 0,600|
| `EDM` |32.007 / 34.0|0,657 / 0,660|0,806 / 0,833|


###1. Medidas de tendencia central (media, mediana, moda)
- **Popularidad (`seguimiento_popularidad`):**La media es**39.335**, la mediana es**42.000**y la moda es**0.000**. Esto indica que existe un grupo importante de canciones con popularidad cero, mientras que el centro del conjunto se ubica alrededor de los 40–42 puntos.
- **Atributos de audio (`capacidad de baile`,`energía`,`tempo`):** `capacidad de baile`tiene media**0,653**, mediana**0,670**y moda**0,690**, lo que muestra una distribución bastante equilibrada y tirando a valores moderados-altos.`energía`presenta media**0,698**, mediana**0,722**y moda**0,833**, reflejando temas en energías generales.`tempo`ronda los**120.962**de media y**121.994**de mediana (moda**127.992**).
- **Duración y año (`duración_min`,`anio`):**La duración media es**3,776 minutos**(mediana**3,616 minutos**, moda**4.000 minutos**), estándar para canciones comerciales. es`anio`, la media es**2011.054**, la mediana**2016.000**y la moda**2019.000**, evidenciando predominio de temas recientes con arrastre de canciones más antiguas.

###2. Medidas de dispersión (rango, varianza, desviación estándar)
- **Alta dispersión:** `seguimiento_popularidad`tiene un rango de**100.000**(0 a 100) y desviación estándar de**23.899**(varianza**561.664**), mostrando gran diferencia entre canciones poco escuchadas y éxitos masivos.`tempo`también varía bastante (rango**203.963**, desv. estándar**26.945**).
- **Dispersión moderada:** `capacidad de baile`(desv. estándar**0,146**, varianza**0,021**) y`energía`(desv. estándar**0,184**, varianza**0,034**) son más estables entre canciones.

###3. Comparación entre variables (por`género_lista_de_reproducción`)
-En la vista agrupada por género,**`estallido`**(medios de comunicación**43.500**, mediana**47.0**) y**`latín`**(medios de comunicación**42.616**, mediana**47.0**) muestran mayor popularidad promedio que**`EDM`**(medios de comunicación**32.007**).
-En atributos de audio,**`EDM`**destaca por su alta energía promedio (**0,806**), mientras que**`rap`**(**0,715**) y**`latín`**(**0,712**) presentan mayor bailabilidad promedio que géneros como**`r&b`**(**0,595**).

###4. Valores atípicos, relaciones e hipótesis
- **Valores atípicos (*valores atípicos*):**Se observan extremos en`seguimiento_popularidad`(valores en`0`frente a picos cercanos a`98–100`),`tempo`(mínimos cerca de`35.477`y máximos cerca de`239.440`),`duración_min`(desde`0,067`hasta`8.630`minutos) y`anio`(desde`1957`hasta`2020`).
- **Hipótesis planteadas:**
  1.El género de la playlist (`estallido`y`latín`frente a`EDM`) se asocia con diferencias en la popularidad promedio de las canciones.
  2.Debido a la presencia de valores extremos en variables como`tempo`,`duración_min`y`anio`, la mediana describe mejor el caso "típico" que la media.

Para curaduría de listas de reproducción, marketing musical o sistemas de recomendación, apoyarse solo en promedios puede distorsionarse por canciones con popularidad cero o duraciones/tempos atípicos. Segmentar por género y revisar medianas junto con la dispersión permite identificar mejor qué características acompañan a los temas más populares en cada categoría.
