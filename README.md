# RecoCubes
Este repositorio es para el proyecto de la materia tc2002b. En este proyecto vamos a usar redes neuronales convolutivas para la clasificación de imágenes.

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
En el artículo "MiDaS: a large-scale Minecraft dataset for non-natural image benchmarking" se presenta MiDaS como un dataset de imágenes de Minecraft. El objetivo principal del documento es proporcionar un benchmark para evaluar algoritmos de visión artificial en imágenes del mundo real o generadas en entornos virtuales. Se usaron 8 modelos distintos . El dataset contiene 36,000 imágenes etiquetadas distribuidas en 60 clases correspondientes a los bloques del juego, como pueden ser lava, cristal, arena, entre otros. En este caso, solo se midió el accuracy individual al reconocer cada bloque por parte del modelo y solo se reportan los mejores y los peores. En la siguiente tabla podemos observar el accuracy de los bloques disponibles que igual usaremos para entrenar el modelo de RecoCube:

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
Tras hacer el primer modelo, decidí experimentar con el data augmentation, ya que mi dataset es pequeño, por lo que decidí hacer dos modelos: uno sin data augmentation y otro con data augmentation. Antes de implementarlo decidí buscar una criterio similar que se haya trabajado por lo que encontré el paper de " Deep Learning in Endoscopic Ultrasound: A Breakthrough in Detecting Distal Cholangiocarcinoma." y use su criterio en mi segundo modelo. En este avance no implementé el ResNet50 que se menciona en el paper  "MiDaS: a large-scale Minecraft dataset for non-natural image benchmarking".

## Arquitectura:
En los dos modelos presentados tienen la arquitectura de capas secuenciales conformadas por:
1 capa convolucional de dos dimensiones con una función de activación relu, 10 filtros convolucionales, un kernel de tamaño 3x3 y un input shape 128x128 RGB.
1 Flatten de 126x126x10.
2 capas seguidas de capas densas con 256 neuronas con función de activación relu.
1 capa de salida con 9 neuronas (acorde al número de clases) que muestra las probabilidades de cuál clase sería.

La razón de esta arquitectura fue que la usamos en el caso de uso de data augmentation en imágenes y decidí usarla y, como baseline, decidí aumentar una capa densa más.

## Resultados
### Train

#### Modelo 1:

<img width="547" height="435" alt="image" src="https://github.com/user-attachments/assets/4e3063ea-de63-439b-bb07-f7fb08386dc5" />

<img width="556" height="435" alt="image" src="https://github.com/user-attachments/assets/b97ace84-e738-4429-8e12-d3b6b8bcefeb" />

#### Modelo 2:
<img width="553" height="435" alt="image" src="https://github.com/user-attachments/assets/2c19e189-4460-4f70-992d-1d4652bd3410" />

<img width="553" height="435" alt="image" src="https://github.com/user-attachments/assets/c615eae7-8145-4dc7-94f5-132d095a831a" />

### Validation

#### Modelo 1:
loss:       0.19886770844459534
precision:  1.0
recall:     0.9629629850387573
f1_score:   [1.         1.         1.         1.         0.96774185 0.96551716
 1.         1.         1.        ]
accuracy:        0.9925925731658936

#### Modelo 2:
loss:       0.032184671610593796
precision:  1.0
recall:     1.0
f1_score:   [1. 1. 1. 1. 1. 1. 1. 1. 1.]
accuracy:     1.0

### Test

#### Modelo 1:
loss:       0.17742317914962769
precision:  0.9922480583190918
recall:     0.9481481313705444
f1_score:   [1.         1.         1.         0.96551716 0.96774185 0.96551716
 1.         0.96774185 1.        ]
accuracy:        0.9851852059364319

#### Modelo 2:
loss:       0.03148989379405975
precision:  1.0
recall:     1.0
f1_score:   [1. 1. 1. 1. 1. 1. 1. 1. 1.]
accuracy:        1.0

### Matriz de confusión

#### Modelo 1:

<img width="888" height="790" alt="image" src="https://github.com/user-attachments/assets/df66e7e0-6f9e-4305-8682-b74806827fe2" />

#### Modelo 2:

<img width="888" height="790" alt="image" src="https://github.com/user-attachments/assets/96ed379f-8f9b-45f9-af2b-d04635d2c607" />


## Interpretación de los datos
Podemos observar que los dos modelos aprendieron bien, ya que podemos ver un comportamiento esperado en las gráficas de loss y accuracy (accuracy sube y loss baja), lo que es una buena señal para nuestra arquitectura, pues no hay una sospecha de que el dataset sea complejo. En validation podemos observar valores altos en los dos modelos, pero el modelo 1 tiende a confundir ciertas clases lo cual podemos observarlo en la precisioón midiendo y en recall ya que los dos aunque se acercan a uno nos estan diciendo que hay muy pocos casos donde se confunde el modelo 1 (algo que podemos ver en la matriz de confusión d euna manera más detallada), mientras que el modelo 2 tiene metricas muy elevadas significando que probablemente puede hjaber un overfitting si cambiamos las imagenes con las cuales se está probando. En el test podemos observar que el modelo 1 empeoró y confunde más clases, lo que nos indica que no sabe generalizar mucho los patrones. Aunque tenga métricas altas, podríamos eliminar esa confusión con un mejor entrenamiento (como lo hicimos con el modelo 2) o modificar los hiperparámetros, porque si le movemos a la arquitectura del modelo, en mi opinión, si hacemos más complejo el modelo, posiblemente se pueda confundir más.

## Conclusión
Al comparar los datos del estado del arte en el paper que encontré y mi problemática, considero que tal vez mi problemática se puede volver un poco más compleja, ya que el caso de uso del paper compara biomas enteros y no solo cubos. Comparando algunos modelos que se mencionan en el paper, podemos sobrevalorar mi modelo y decir que tiene mejores estadísticas para detectar algunos cubos mejor que otros modelos mencionados en el paper, como por ejemplo el bloque de esmeralda, el netherrack y los ladrillos. También podemos ver una gran similitud cuando detectan los ores de diamante, oro y hierro. Al probar con otras imágenes del mundo real, en mi modelo 2 podemos ver una notoriedad en el resultado del modelo 2 vs. modelo 1 porque hay patrones que aprendió de una mejor manera que el modelo 1.Finalmente, en los siguientes pasos podríamos probar el modelo con imágenes más complejas, como veremos en secciones posteriores.

## Probando en el mundo real
Aquí comparamos los dos modelos con imagenes sacadas de la web.

Imagen Fácil - Reconocer el diamante
<img width="736" height="736" alt="diamond_ore_test" src="https://github.com/user-attachments/assets/696d739c-4210-4d86-89c0-6fadc48c5730" />

Resultado:
<img width="777" height="647" alt="image" src="https://github.com/user-attachments/assets/28d65312-9ad6-4ca0-b062-c2a3a5f13f60" />

Imagen Mediana - Reconocer Glowstone

<img width="278" height="181" alt="glostone_group" src="https://github.com/user-attachments/assets/8a707e97-2a77-4cc0-b493-825b03fa1487" />

Resultado:

<img width="647" height="690" alt="image" src="https://github.com/user-attachments/assets/e288250e-643f-4e9c-956c-c311a1c0c38b" />


## Link del Notebook:
[Este es el link del NoteBook](https://colab.research.google.com/drive/1Q5tc7Oq1ucE3rf68SjzLTgfQpv8-9B78?usp=sharing) si hay algún problema en este repositorio, dejo el archivo de igual forma.

## Referencias
Torpey, D., Parkin, M., Alter, J., Klein, R., & James, S. (2024). MiDaS: A large-scale Minecraft dataset for non-natural image benchmarking. Journal of Electronic Imaging, 33(1), 013035. [https://doi.org/10.1117/1.JEI.33.1.013035](https://doi.org/10.1117/1.JEI.33.1.013035)

Orzan, R. I., Santa, D., Lorenzovici, N., Zareczky, T. A., Pojoga, C., Agoston, R., Dulf, E.-H., & Seicean, A. (2024). Deep Learning in Endoscopic Ultrasound: A Breakthrough in Detecting Distal Cholangiocarcinoma. Cancers, 16(22), 3792. [https://doi.org/10.3390/cancers16223792](https://doi.org/10.3390/cancers16223792) 
