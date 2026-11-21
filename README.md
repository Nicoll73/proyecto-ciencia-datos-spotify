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
