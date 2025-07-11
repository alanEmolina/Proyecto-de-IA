# Proyecto de IA



## Planteamiento del problema :

¿Se puede predecir si una persona abandonará un servicio de telecomunicaciones en base a características como el tipo de contrato, facturación, servicios contratados y antigüedad?

### Contexto:

La tasa de cancelación o pérdida de clientes, conocido como churn en marketing, es un problema crítico en la industria de telecomunicaciones, donde la retención de clientes impacta directamente en la rentabilidad de las empresas. Predecir el churn permite a las empresas implementar estrategias proactivas de retención, optimizar recursos y mejorar la satisfacción del cliente. Ya que existen patrones en el comportamiento de los clientes que abandonan, un modelo de IA puede identificar estos factores de riesgo.

### Objetivo:

Desarrollar un modelo de clasificación que prediga si un cliente abandonará el servicio en base a un conjunto de variables extraídas del dataset, con un metodo de aprendizaje supervisado para el dataset [Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn).


### Modelos

El presente proyecto busca predecir el abandono de clientes en una empresa de telecomunicaciones, utilizando variables como antigüedad del cliente (tenure), tipo de contrato, servicios contratados, facturación mensual, entre otras. Se trata de un problema clásico de **clasificación binaria supervisada**, donde la variable objetivo (`Churn`) indica si una persona abandonó el servicio (1) o no (0).

Para abordar este problema, se seleccionaron tres modelos con diferentes fortalezas, con el objetivo de comparar su rendimiento y balancear precisión con interpretabilidad:



#### Regresión Logística

**Ventajas:**
- Altamente interpretable: permite identificar qué variables contribuyen más a la probabilidad de abandono.
- Computacionalmente eficiente.
- Estable y confiable como modelo base (*baseline*) para clasificación binaria.

**Limitaciones:**
- Supone relaciones lineales entre variables independientes y la variable objetivo.
- Menor rendimiento en presencia de relaciones no lineales complejas.

**Pertinencia:**  
Se utiliza como punto de partida para establecer un benchmark básico y comprensible.



#### Árbol de Decisión

**Ventajas:**
- Interpretable visualmente: entrega reglas claras y comprensibles.
- Captura relaciones no lineales.
- No requiere normalización de los datos.

**Limitaciones:**
- Propenso al *overfitting* si no se aplica poda.
- Sensible a pequeñas variaciones en los datos.

**Pertinencia:**  
Adecuado para representar decisiones operativas simples del tipo "si antigüedad < 6 meses y el contrato es mensual, entonces hay alto riesgo de abandono". Útil en contextos donde se requiere transparencia en las decisiones del modelo.



#### Random Forest

**Ventajas:**
- Mayor precisión y robustez que modelos individuales.
- Menor riesgo de *overfitting*.
- Permite estimar la importancia de las variables.

**Limitaciones:**
- Menor interpretabilidad.
- Mayor demanda computacional.

**Pertinencia:**  
Ideal para obtener un modelo de alto rendimiento que pueda capturar relaciones complejas entre variables. Útil como modelo de producción o referencia final.



### Justifiacion para uso de 3 modelos

Se utilizarán los tres modelos de forma complementaria:

1. **Regresión Logística**: como línea base explicativa.
2. **Árbol de Decisión**: para generar reglas fácilmente comprensibles.
3. **Random Forest**: como modelo robusto y preciso de referencia.

Esta combinación permite equilibrar precisión, interpretabilidad y robustez, lo cual es fundamental en el ámbito empresarial, donde no solo importa predecir correctamente, sino también justificar las decisiones del modelo.



### Estructura de carpetas

La organización actual de este repositorio es la siguiente:

```plaintext
PROYECTO-DE-IA/
├── dataset/  
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv
├── proyecto.ipynb  
└── README.md  
```


### Resultados Importantes

A continuación presentamos de forma concisa los hallazgos más relevantes de todo el análisis, acompañados de la interpretación de métricas, las gráficas clave y una discusión crítica.

---

#### 1. Tabla resumen de desempeño

| Modelo                | CV F1  | Test F1 | Test AUC | AP (PR-Curve) |
|-----------------------|:------:|:-------:|:--------:|:-------------:|
| **Logistic Regression**    | 0.72   | 0.61    | 0.840    | 0.632         |
| **Decision Tree**          | 0.71   | 0.62    | 0.816    | 0.547         |
| **Random Forest (baseline)** | 0.70   | 0.51    | 0.816    | 0.650         |
| **Random Forest (tuned)**    | 0.74   | 0.61    | 0.837    | 0.650         |
 ---
> **Nota:**  
> - **CV F1**: media del F1-score en validación cruzada (5 folds, macro).  
> - **Test F1/AUC/AP**: métricas calculadas sobre el conjunto de prueba.

---

#### 2. Gráficas clave

##### 2.1 Curvas ROC comparativas



- La **Regresión Logística** tuned alcanza AUC = 0.840, seguida muy de cerca por el **Random Forest tuned** (AUC = 0.837).  
- El **Decision Tree** muestra una capacidad de discriminación ligeramente inferior (AUC = 0.816).

##### 2.2 Curvas Precision–Recall comparativas



- El área bajo la curva PR (AP) es más alta para **Random Forest** (0.650), indicando un mejor balance entre precision y recall cuando importa detectar churners.  
- La Regresión Logística tuned (AP = 0.632) y el Decision Tree (AP = 0.547) quedan por detrás.

##### 2.3 Matriz de confusión del mejor modelo (RF tuned)


|              | Predicción No | Predicción Sí |
|--------------|:-------------:|:-------------:|
| **Real No**  | 830           | 205           |
| **Real Sí**  | 121           | 253           |

- **Verdaderos positivos (TP)**: 253 churners correctamente identificados.  
- **Falsos negativos (FN)**: 121 churners no detectados (riesgo de pérdida).  

---

#### 3. Interpretación de métricas

1. **F1-score vs. AUC**  
   - El F1-score pone énfasis en la clase minoritaria (churn). El RF tuned y el Decision Tree tuned empatan en 0.62, mientras que la Regresión Logística logra 0.61.  
   - El AUC mide la discriminación global: la Regresión Logística tuned lidera con 0.840, aunque sacrificando algo de balance (F1).  

2. **Precision vs. Recall**  
   - **Recall alto** en Regresión Logística (0.78) significa que casi todos los churners son detectados, pero su precision (0.50) implica más falsas alarmas.  
   - **Random Forest** tuned mejora la precision (0.57) sin descuidar el recall (0.68), logrando un mejor AP (0.650).

3. **Estabilidad vs. Complejidad**  
   - El gap reducido entre CV F1 y Test F1 en RF tuned (0.74 → 0.61) muestra buena generalización sin overfitting excesivo.  
   - El Decision Tree, a pesar de su simplicidad, compite bien en F1 pero pierde en AUC y estabilidad.

---

#### 4. Discusión crítica

- **Casos de negocio**  
  - Si la prioridad es **no perder** a ningún cliente en riesgo (minimizar FN), la Regresión Logística tuned es adecuada por su alto recall.  
  - Para **maximizar precisión de alertas** (minimizar FP) y aún detectar la mayoría de churners, el Random Forest tuned es la mejor opción.

- **Limitaciones**  
  - El churn (~26.5%) sigue estando desbalanceado; explorar SMOTE o focal loss podría mejorar recall sin sacrificar precision.  
  - El análisis no contempla **drift** temporal: un monitoreo continuo de métricas es recomendable.

---

> **Conclusión breve**  

> El **Random Forest tuned** ofrece el mejor compromiso entre precision y recall (F1 = 0.62, AUC = 0.837, AP = 0.650) y generaliza bien, por lo que es el candidato ideal para un sistema de alerta de churn en producción. Si la transparencia de decisiones es clave, la **Regresión Logística tuned** (AUC = 0.840) sigue siendo una alternativa sólida.  


### Conclusiones

Tras el análisis completo del proyecto de predicción de churn, extraemos las siguientes conclusiones claras y ordenadas:

#### 1. Desempeño de los modelos  
- **Random Forest (tuned)**  
  - **F1-test**: 0.62  
  - **AUC-test**: 0.837  
  - **AP (Precision–Recall)**: 0.650  
  - Es el modelo más equilibrado, con buena capacidad de discriminación y balance entre precisión y recall.  
- **Regresión Logística (tuned)**  
  - **F1-test**: 0.61  
  - **AUC-test**: 0.845  
  - **AP**: 0.632  
  - Destaca por su AUC ligeramente superior y por la interpretabilidad de sus coeficientes.  
- **Árbol de Decisión (tuned)**  
  - **F1-test**: 0.62  
  - **AUC-test**: 0.832  
  - **AP**: 0.547  
  - Ofrece reglas de decisión claras, pero muestra menor robustez frente a cambios en los datos.

#### 2. Interpretación de métricas clave  
- **Precision vs. Recall**  
  - La logística maximiza recall (0.78) capturando casi todos los churners, a costa de más falsas alarmas.  
  - El RF tuned mejora la precision (0.57) sin sacrificar demasiado el recall (0.68).  
- **AUC (ROC)**  
  - Mide la capacidad global de separación de clases; la regresión logística lidera con 0.845.  
- **AP (Curva PR)**  
  - Indica eficacia al identificar churners en escenarios desbalanceados; RF tuned alcanza 0.650, el valor más alto.

#### 3. Factores determinantes  
- **Tenure** y **TotalCharges**: principales predictores en todos los modelos.  
- **Contrato “Month-to-month”**: claramente asociado a mayor churn.  
- **Servicio de Internet (Fiber optic)**: incrementa la probabilidad de abandono.

#### 4. Limitaciones  
1. **Desbalance de clases** (~26.5% churn): podría mejorarse con técnicas de sobremuestreo (SMOTE) o funciones de pérdida focalizadas.  
2. **Variables no incluidas**: `SeniorCitizen` y `PaymentMethod` podrían aportar señal adicional.  
3. **Análisis estático**: no contempla drift temporal; se recomienda monitoreo y retraining periódicos.

#### 5. Recomendaciones y siguientes pasos  
- **Nuevas features**: ratio `TotalCharges/tenure`, agrupar “No internet service” en un dummy único.  
- **Modelos avanzados**: explorar XGBoost o LightGBM para mejorar las métricas en datasets heterogéneos.  
- **Despliegue**: serializar los pipelines con `joblib` y exponerlos mediante FastAPI o Streamlit.  
- **Monitoreo continuo**: generar dashboards que alerten de caídas en AUC o F1 por cambios en los datos.

> **Cierre**  
> El **Random Forest afinado** es el candidato óptimo para un sistema de alerta de churn en producción, gracias a su robustez y balance entre precision y recall. Si la trazabilidad de cada variable es prioritaria, la **Regresión Logística** sigue siendo una alternativa válida, con un desempeño competitivo y coeficientes de fácil interpretación.  
