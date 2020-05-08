# Reconstrucción de Rostros basado en redes Cgan (Pix2Pix)
___

El siguiente repositorio contiene el proyeccto de reconstrucción de rostros utilizando la arquitectura Pix2Pix. Para la construcción base del modelo se han tomado dos referencias:

- El [tutorial](https://www.tensorflow.org/tutorials/generative/pix2pix)  oficial de la pagina de tensorflow.
- El [tutorial](https://www.youtube.com/watch?v=YsrMGcgfETY) de DotCSV acerca de pix2pix.

El proyecto fue hecho para el curso de **Python para Data Science** del Diplomado de Inteligencia Artificial de la Pontificia Universidad Católica del Perú.

___
## Dependencias:
Se está utilizando como framework principal Tensorflow 2.2.0, usando parte del API Keras para la arquitectura del modelo y el API nativo tensorflow para el entrenamiento.
- Tensorflow (2.2.0)
- Matplotlib (3.2.1)
- Numpy (1.18.4)
___

## Proceso

### Objetivo
El proyecto se enfoca en la reconstrucción de rostros de personas teniendo como base una imágen tipo trazado de lápiz. Una posible aplicación importante sería el apoyo a la contrucción de retratos hablados (Police Sketches) en criminalística.

### Dataset
Se extrajeron datos de la página [This Person Doesn't Exist](https://thispersondoesnotexist.com/) para evitar problemas de datos personales. Reunimos 754 imágenes para la prueba.
Al ser una red GAN, se requiere de una imágen tanto como para el dataset de entrada como para el label. Con las imágenes arriba completamos los labels, y para las imágenes de entrada se hicieron las siguientes modificaciones a los targets:
- Efecto fotocopia:
    - Detalle: 15
    - Darkness: 3
- Posterize:  
    - Nivel 10
Lo ideal sería completar este dataset con imágenes hechas por efectivos policiales dedicados a la materia, pero debido al contexto del desarrollo este procedimiento nos pareció el más acertado para el trabajo.

### Parámetros
La arquitectura utilizada fue Pix2Pix (véase [Paper Oficial](https://arxiv.org/pdf/1611.07004.pdf)). Según este documento, se utilzaró Binary Crossentropy como función de pérdida tanto para el discriminador como para el generador. Como optimizador, se hicieron pruebas con Adam y Rectified Adam, probando distintos learning rates desde el rango de 1e-3 hasta 1e.7.
