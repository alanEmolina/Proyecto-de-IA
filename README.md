# Proyecto de IA



## Planteamiento del problema :

¿Se puede predecir si una persona tiene diabetes en base a sus características clínicas (edad, IMC, presión, historial familiar, etc.)?

### Contexto:

La diabetes tipo 2 es una enfermedad metabólica común que afecta a millones de personas en el mundo. Su detección temprana permite modificar hábitos y prevenir complicaciones graves como enfermedades cardíacas, renales o amputaciones. Dado que se conocen diversos factores de riesgo, un modelo de IA puede ser entrenado para predecir la probabilidad de desarrollar diabetes.

### Objetivo:

Desarrollar un modelo de clasificación que prediga si una persona tiene diabetes en base a un conjunto de variables clínicas extraídas de un dataset médico, con un metodo de aprendizaje supervisado para el dataset
Pima Indians Diabetes [Dataset](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database).

## Modelos

El presente proyecto busca predecir la presencia de diabetes tipo 2 en pacientes, utilizando variables clínicas como nivel de glucosa, índice de masa corporal (IMC), edad, presión arterial, entre otras. Se trata de un problema clásico de **clasificación binaria supervisada**, donde la variable objetivo (`Outcome`) indica si una persona tiene (1) o no tiene (0) diabetes.

Para abordar este problema, se seleccionaron tres modelos con diferentes fortalezas, con el objetivo de comparar su rendimiento y balancear precisión con interpretabilidad:



#### Regresión Logística

**Ventajas:**
- Altamente interpretable: permite identificar qué variables contribuyen más a la probabilidad de tener diabetes.
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
Adecuado para representar decisiones clínicas simples del tipo “si glucosa > X y edad > Y, entonces...”. Útil en contextos donde se requiere transparencia en las decisiones del modelo.



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

Esta combinación permite equilibrar precisión, interpretabilidad y robustez, lo cual es fundamental en el ámbito médico, donde no solo importa predecir correctamente, sino también justificar las decisiones del modelo.
