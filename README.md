# Proyecto de IA



## Planteamiento del problema :

¿Se puede predecir si una persona abandonará un servicio de telecomunicaciones en base a características como el tipo de contrato, facturación, servicios contratados y antigüedad?

### Contexto:

La tasa de cancelación o pérdida de clientes, conocido como churn en marketing, es un problema crítico en la industria de telecomunicaciones, donde la retención de clientes impacta directamente en la rentabilidad de las empresas. Predecir el churn permite a las empresas implementar estrategias proactivas de retención, optimizar recursos y mejorar la satisfacción del cliente. Ya que existen patrones en el comportamiento de los clientes que abandonan, un modelo de IA puede identificar estos factores de riesgo.

### Objetivo:

Desarrollar un modelo de clasificación que prediga si un cliente abandonará el servicio en base a un conjunto de variables extraídas del dataset, con un metodo de aprendizaje supervisado para el dataset [Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn).

## Modelos

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
