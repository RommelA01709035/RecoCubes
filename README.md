# RecoCubes
Este repositorio es para el proyecto de la materia tc2002b. En este proyecto vamos a usar redes neuronales convolutivas para la clasificación de imagenes.

# Descripción del Proyecto
RecoCubes (Reconocer Cubos) tiene como objetivo desarrollar un modelo clasificador de imágenes con la capacidad suficiente para distinguir entre 9 cubos distintos de Minecraft. 

## Contexto 

En la materia vemos redes neuronales convolucionales, las cuales tienen la capacidad de inferir alguna cosa, en nuestro contexto vamos a estar infiriendo casos de clasificación o regresión. Este problema aborda la clasificación de imágenes.

## Descripción del Dataset
El dataset proveniente de [esta página](https://huggingface.co/datasets/HaiPenglai/BlockCraft-Dataset) tiene 100 fotos de 20 bloques divididas en carpetas como se ve en las siguientes imágenes:

<div align="center">
  <figure>
    <img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/53136c0d-8a1b-4e5b-a380-aca174ca29eb">
    <br>
    <figcaption><em>Figura 1. Lista de carpetas del dataset.</em></figcaption>
  </figure>

  <br>

  <figure>
    <img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/290a58b1-8a46-4eee-b478-c008adb103dc">
    <br>
    <figcaption><em>Figura 2. Fotos dentro de una carpeta del dataset.</em></figcaption>
  </figure>
</div>

Como podemos observar, por la cantidad de imágenes y su similitud, a pesar de tener la misma cantidad de imágenes por cada bloque, se van a preprocesar las imágenes para que tengan fondos distintos y se va a hacer data augmentation para tener más cantidad de imágenes.

## Alcance
Este proyecto va a identificar los siguientes cubos:

1. Brick
2. Glowstone
3. Netherrack
4. Sand
5. Planks Oak
6. Emerald Block
7. Diamond Ore
8. Iron Ore
9. Gold Ore

## Datatset en drive
[Link del drive](https://drive.google.com/drive/folders/1sjX1jhd8eWBE2OShA1Z7cXSgO0JAbkWT?usp=sharing)

## Preprocesamiento:
1. Se verificó el tamaño de las imágenes para que todas tuvieran el mismo tamaño, en este caso, 128x128.
2. Se hizo la técnica de data augmentation para generar más datos.
3. Se convirtieron las imágenes a rangos entre 0.0 y 1.0.

## Link del Notebook:
[Este es el link del NoteBook](https://colab.research.google.com/drive/1Q5tc7Oq1ucE3rf68SjzLTgfQpv8-9B78?usp=sharing) si hay algún problema en este repositorio dejo el archivo de igual forma
