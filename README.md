Clasificación de Tipos de Tráfico de Red mediante Aprendizaje Automático
========================================================================

Descripción
-----------
Este proyecto implementa modelos de **aprendizaje supervisado** para clasificar distintos tipos de tráfico de red, incluyendo:

- game
- instant-message
- mail
- network-storage
- video
- web-browsing

Se comparan dos enfoques principales:

1. **Aprendizaje Superficial**: Random Forest Classifier.
2. **Aprendizaje Profundo**: Red neuronal utilizando TensorFlow/Keras.

El objetivo es analizar cómo la complejidad de las features (simples vs complejas) afecta el desempeño del modelo.

Dataset
-------
El conjunto de datos original se encuentra disponible en:

https://springernature.figshare.com/articles/dataset/Tracffic_data_from_real_network_environment/28380347

El conjunto de datos contiene métricas de flujo de red, organizadas en dos tipos:

1. **Métricas simples (por flujo `flow_id`)**:
- `flow_id`
- `packets`
- `bytes`
- `duration`
- `avg_pkt_size`
- `syn_count`, `ack_count`, `fin_count`, `rst_count`
- `class` (etiqueta de tipo de tráfico)

2. **Métricas complejas (agregadas por ventana de tiempo `window_start` y `window_end`)**:
- `window_start`, `window_end`
- `packets`
- `bytes`
- `duration`
- `avg_pkt_size`
- `throughput`, `pkt_rate`
- `class` (etiqueta de tipo de tráfico)

Estas ventanas permiten capturar patrones agregados de tráfico que mejoran significativamente el desempeño de los modelos.

Metodología
-----------
1. **Preprocesamiento de Datos**: Limpieza y normalización.
2. **División de Datos**: Conjuntos de entrenamiento, prueba y validación.
3. **Entrenamiento de Modelos**:
   - Random Forest (superficial) con optimización de hiperparámetros.
   - Red neuronal (profundo) con capas densas y activación ReLU.
4. **Evaluación**: Precisión, recall, F1-score, accuracy y validación cruzada.
5. **Visualización**: Curvas de aprendizaje, importancia de features, matriz de confusión.

Resultados
----------
Aprendizaje Superficial (Random Forest)

Métricas simples:
<img width="980" height="415" alt="image" src="https://github.com/user-attachments/assets/5862cc17-9163-4172-a4cc-9790300305bc" />


Clase                | Precision | Recall | F1-score | Support
-------------------- | --------- | ------ | -------- | -------
game                 | 0.53      | 0.77   | 0.63     | 1072
instant-message      | 0.48      | 0.38   | 0.42     | 875
mail                 | 0.57      | 0.43   | 0.49     | 609
network-storage      | 0.71      | 0.55   | 0.62     | 822
video                | 0.80      | 0.79   | 0.79     | 626
web-browsing         | 0.59      | 0.62   | 0.60     | 963

- Accuracy (Validation): 0.595
- F1-score (macro): 0.592
- F1-score (weighted): 0.589
- Accuracy promedio CV: 0.611 ± 0.005

Métricas complejas:
<img width="982" height="427" alt="image" src="https://github.com/user-attachments/assets/933a3fba-ffcb-405a-b693-5fce348e1b1d" />

Clase                | Precision | Recall | F1-score | Support
-------------------- | --------- | ------ | -------- | -------
game                 | 1.00      | 0.99   | 0.99     | 231
instant-message      | 1.00      | 0.98   | 0.99     | 55
mail                 | 0.94      | 0.97   | 0.95     | 60
network-storage      | 0.98      | 1.00   | 0.99     | 177
video                | 0.98      | 0.98   | 0.98     | 121
web-browsing         | 0.97      | 0.96   | 0.96     | 119

- Accuracy (Validation): 0.982
- F1-score (macro): 0.977
- F1-score (weighted): 0.982
- Accuracy promedio CV: 0.987 ± 0.002

Aprendizaje Profundo (Red Neuronal)

Métricas simples:
<img width="1001" height="429" alt="image" src="https://github.com/user-attachments/assets/c7fa3f58-6489-4f1c-8b0a-d90658a74889" />

Clase                | Precision | Recall | F1-score | Support
-------------------- | --------- | ------ | -------- | -------
game                 | 0.41      | 0.76   | 0.53     | 1072
instant-message      | 0.37      | 0.34   | 0.35     | 875
mail                 | 0.60      | 0.18   | 0.27     | 609
network-storage      | 0.69      | 0.30   | 0.41     | 822
video                | 0.47      | 0.60   | 0.53     | 626
web-browsing         | 0.43      | 0.37   | 0.39     | 963

- Accuracy (Validation): 0.442
- F1-score (macro): 0.415
- F1-score (weighted): 0.422

Métricas complejas:
<img width="984" height="405" alt="image" src="https://github.com/user-attachments/assets/0f14a867-09b1-4fa4-847b-a132ec921e8e" />

Clase                | Precision | Recall | F1-score | Support
-------------------- | --------- | ------ | -------- | -------
game                 | 0.94      | 0.90   | 0.92     | 231
instant-message      | 0.96      | 0.96   | 0.96     | 55
mail                 | 0.74      | 0.85   | 0.79     | 60
network-storage      | 0.86      | 0.90   | 0.88     | 177
video                | 0.88      | 0.94   | 0.91     | 121
web-browsing         | 0.88      | 0.76   | 0.81     | 119

- Accuracy (Validation): 0.886
- F1-score (macro): 0.880
- F1-score (weighted): 0.886

Conclusión Comparativa
---------------------
- Ambos modelos dependen fuertemente de la calidad y complejidad de las features.
- Con métricas simples, el desempeño es limitado (accuracy ~0.44-0.59).
- Con métricas complejas, se alcanza un desempeño muy alto (accuracy ~0.88-0.98).
- El modelo profundo puede escalar mejor a datasets más grandes o ruidosos, aunque ambos mejoran claramente con la complejidad de las features.

Tecnologías Utilizadas
---------------------
- Python 3.x
- scikit-learn
- pandas
- numpy
- matplotlib
- seaborn
- TensorFlow / Keras

Ejecución
---------
1. Clonar el repositorio:

```bash
git clone https://github.com/Daysi9712/DProyecto.git
cd DProyecto
