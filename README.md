# Clasificador de ¿ Es Hot Dog ?
Este proyecto implementa un sistema de clasificación binaria de imágenes para distinguir entre "Perros Calientes" y "No Perros Calientes" utilizando el conjunto de datos Food-101. Explora diferentes estrategias para manejar el desequilibrio de clases y mejorar el rendimiento del modelo, incluyendo el balanceo básico, la aumentación extensiva de datos y el ajuste fino de un modelo ResNet18 preentrenado.

 ## Características
- Manejo de Conjuntos de Datos Personalizados: Clases BinaryFoodDataset y AugmentedHotdogDataset para preparar conjuntos de datos balanceados y aumentados para la clasificación binaria.
- Aumentación de Datos: Transformaciones de imagen completas que incluyen redimensionamiento, recortes aleatorios, volteos, rotaciones, ajuste de color (color jitter) y borrado aleatorio para mejorar la generalización del modelo.
- Modelo CNN Personalizado: Una red neuronal convolucional simple (CNNBinary) para un rendimiento de referencia.
- Aprendizaje por Transferencia con ResNet18: Ajuste fino de un modelo ResNet18 preentrenado para una mayor precisión.
- Experimentos Comparativos: Tres experimentos distintos para evaluar diferentes metodologías de entrenamiento:
- Balanceo Básico: Entrenamiento con un conjunto de datos pequeño y balanceado.
- Aumentación Extensiva de Datos: Entrenamiento con un conjunto de datos mucho más grande generado mediante Data Augmentation.
- Ajuste Fino de ResNet18: Aprovechando un modelo de aprendizaje profundo preentrenado con el conjunto de datos aumentado.
- Métricas de Evaluación Detalladas: Proporciona precisión (accuracy), exactitud (precision), exhaustividad (recall), puntuación F1 (F1-score), verdaderos positivos (TP), verdaderos negativos (TN), falsos positivos (FP) y falsos negativos (FN) para cada experimento.

## Experimentos
El proyecto lleva a cabo tres experimentos comparativos:
1. Balanceo Básico (750 Perros Calientes + 750 No Perros Calientes)
- Objetivo: Establecer una línea de base utilizando un subconjunto pequeño y balanceado de los datos de entrenamiento de Food-101 (750 imágenes de perros calientes y 750 imágenes de no perros calientes).
- Modelo: Un modelo CNNBinary personalizado.
- Transformaciones: Redimensionamiento y normalización básicas.
Épocas: 15
2. Aumentación Extensiva de Datos (10,000 Perros Calientes + 10,000 No Perros Calientes)
- Objetivo: Mejorar el rendimiento generando un conjunto de datos de entrenamiento mucho más grande utilizando diversas técnicas de aumentación de datos para las imágenes de perros calientes (para equilibrar las instancias naturalmente menos frecuentes) y muestreando 10,000 imágenes de no perros calientes.
- Modelo: Un modelo CNNBinary personalizado.
- Transformaciones: Aumentación agresiva (recorte aleatorio redimensionado, volteo horizontal, rotación, ajuste de color, borrado aleatorio) para ambas clases.
Épocas: 7
3. ResNet18 Preentrenado (10,000 Perros Calientes + 10,000 No Perros Calientes)
- Objetivo: Aprovechar el poder de los modelos de aprendizaje profundo preentrenados (aprendizaje por transferencia) ajustando un modelo ResNet18 en el conjunto de datos extensivamente aumentado.
- Modelo: models.resnet18(pretrained=True) con la capa de clasificación final reemplazada por una salida binaria. Las capas anteriores se congelan y solo las últimas capas (layer4, avgpool y la nueva capa fc) se ajustan.
- Transformaciones: La misma aumentación agresiva que en el Experimento 2.
Épocas: 7
4. Adicional se realizó el mismo entrenamiento en otro archivo ipynb, pero con 25250 datos de Test (Para asemejar casos de la vida real).
  
## Resultados Esperados
Observarás que a medida que la complejidad de la estrategia de entrenamiento aumenta (desde el balanceo básico hasta la aumentación de datos y el aprendizaje por transferencia), el rendimiento del modelo, particularmente la Precisión en el Test (Test Accuracy), debería mejorar significativamente. Se espera que el modelo ResNet18 Preentrenado produzca los mejores resultados debido a su capacidad para aprovechar las características aprendidas de un conjunto de datos masivo (ImageNet) y adaptarlas a la tarea de clasificación de perros calientes.

## Contribuciones
Siéntete libre de bifurcar este repositorio, abrir problemas o enviar solicitudes de extracción. ¡Todas las contribuciones son bienvenidas!

## Licencia
Este proyecto es de código abierto y está disponible bajo la Licencia MIT.
