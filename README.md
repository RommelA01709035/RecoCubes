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

## Trabajos relacionados.
En el artículo "MiDaS: a large-scale Minecraft dataset for non-natural image benchmarking" se presenta MiDaS como un dataset de imágenes de Minecraft. El objetivo principal del documento es proporcionar un benchmark para evaluar algoritmos de visión artificial en imágenes del mundo real o generadas en entornos virtuales. Se usaron 8 modelos distintos . El dataset contiene 36,000 imágenes etiquetadas distribuidas en 60 clases correspondientes a los bloques del juego, como pueden ser lava, cristal, arena, entre otros. En este caso solamente se midió el accuracy individual al reconocer cada bloque por parte del modelo y solamente se reportan los mejores y los peores. En la siguiente tabla podemos observar el accuracy de los bloques disponibles que igual usaremos para entrenar el modelo de RecoCube:

| Bloque | Accuracy | Modelo | Evaluación | % Labels |
|---|---|---|---|---|
| Brick | 0.0 | Sup-RN50-Rdm | Fine-tuning | 1% |
| Brick | 0.965 | DINO-RN50-IN | Linear evaluation | 5% |
| Glowstone | 0.082 | Sup-RN50-IN | Fine-tuning | 1% |
| Glowstone | 0.408 | Sup-RN50-Rdm | Linear evaluation | 5% |
| Glowstone | 0.964 | DINO-RN50-IN | Linear evaluation | 5% |
| Netherrack | 0.843 | DINO-RN50-MiDaS | Fine-tuning | 1% |
| Netherrack | 0.539 | Sup-RN50-Rdm | Linear evaluation | 1% |
| Netherrack | 0.585 | Sup-RN50-Rdm | Linear evaluation | 5% |
| Netherrack | 0.5 | Sup-RN50-Rdm | Fine-tuning | 1% |
| Netherrack | 0.958 | SimCLR-RN50-MiDaS | Linear evaluation | 1% |
| Netherrack | 0.77 | SimCLR-RN50-IN | Linear evaluation | 1% |
| Netherrack | 0.777 | DINO-RN50-IN | Linear evaluation | 1% |
| Oak_Planks | 0.868 | SimCLR-RN50-IN | Fine-tuning | 5% |
| Gold Ore | 1.0 | Sup-RN50-IN | Fine-tuning | 5% |
| Gold Ore | 1.0 | DINO-RN50-MiDaS | Linear evaluation | 5% |
| Gold Ore | 0.961 | DINO-RN50-MiDaS | Linear evaluation | 1% |
| Gold Ore | 1.0 | DINO-ViT-MiDaS | Fine-tuning | 5% |
| Gold Ore | 1.0 | DINO-ViT-MiDaS | Linear evaluation | 1% |
| Gold Ore | 1.0 | DINO-ViT-MiDaS | Linear evaluation | 5% |
| Gold Ore | 0.951 | DINO-ViT-MiDaS | Fine-tuning | 1% |
| Gold Ore | 0.965 | Sup-RN50-IN | Fine-tuning | 1% |
| Gold Ore | 0.958 | DINO-RN50-IN | Fine-tuning | 1% |
| Gold Ore | 0.916 | Sup-RN50-IN | Linear evaluation | 1% |
| Emerald Block | 0.999 | SimCLR-RN50-IN | Fine-tuning | 5% |
| Emerald Block | 0.998 | DINO-RN50-MiDaS | Fine-tuning | 5% |
| Emerald Block | 0.999 | DINO-ViT-MiDaS | Fine-tuning | 5% |
| Emerald Block | 0.985 | DINO-ViT-IN | Fine-tuning | 5% |
| Emerald Block | 0.595 | DINO-ViT-IN | Fine-tuning | 1% |
| Emerald Block | 1.0 | DINO-ViT-MiDaS | Linear evaluation | 1% |
| Emerald Block | 1.0 | DINO-ViT-MiDaS | Linear evaluation | 5% |
| Sand | No reportado | - | - | - |
| Diamond Ore | No reportado | - | - | - |
| Iron Ore | No reportado | - | - | - |

## Preprocesamiento:
1. Se verificó el tamaño de las imágenes para que todas tuvieran el mismo tamaño, en este caso, 128x128.
2. Se hizo la técnica de data augmentation para generar más datos usando el criterio del paper "Deep Learning in Endoscopic Ultrasound: A Breakthrough in Detecting Distal Cholangiocarcinoma" (Orzan et al., 2024) donde tenían un dataset reducido de 156 imágenes con una arquitectura de redes neuronales convolucionales usando ResNet50. Los criterios fueron:
   - A)   Rotación aleatoria -30 y +30
   - B)   Reflejo horizontal
   - C)   Traslación en X hasta +- 10 pixeles
   - D)   Traslación en Y hasta +- 10 pixeles
   - E)   Escalamiento entre 0.9 y 1.0

No se usó la generación de ruido gaussiano como dice en el paper porque lo consideré exagerado para este caso de uso.

4. Se convirtieron las imágenes a un rango de 0.0 a 1.0.

## Desarrollo de los modelos.

### Arquitectura:
En los dos modelos presentados tienen la arquitectura de capas secuenciales conformadas por:
1 capa convolucional de dos dimensiones con una función de activación relu, 10 filtros convolucionales, un kernel de tamaño 3x3 y un input shape 128x128 RGB.
1 Flatten de 126x126x10.
2 capas seguidas de capas densas con 256 neuronas con función de activación relu.
1 capa de salida con 9 neuronas (acorde al número de clases) que muestra las probabilidades de cuál clase sería.

La razón de esta arquitectura fue porque la usamos en el caso de uso de data augmentation en imágenes y decidí usarla y, como baseline, decidí aumentar una capa densa más.


## Link del Notebook:
[Este es el link del NoteBook](https://colab.research.google.com/drive/1Q5tc7Oq1ucE3rf68SjzLTgfQpv8-9B78?usp=sharing) si hay algún problema en este repositorio, dejo el archivo de igual forma.




## Referencias

Orzan, R. I., Santa, D., Lorenzovici, N., Zareczky, T. A., Pojoga, C., Agoston, R., Dulf, E.-H., & Seicean, A. (2024). Deep Learning in Endoscopic Ultrasound: A Breakthrough in Detecting Distal Cholangiocarcinoma. Cancers, 16(22), 3792. [https://doi.org/10.3390/cancers16223792](https://doi.org/10.3390/cancers16223792) 
