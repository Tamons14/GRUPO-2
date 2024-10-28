# GRUPO-2
PROBLEMA:
La industria de tarjetas de crédito enfrenta grandes desafíos con clientes que incumplen sus pagos mínimos, generando pérdidas financieras significativas. Según McKinsey, la morosidad global en este sector representa un 0.9% de la deuda total anual, lo que implica miles de millones en pérdidas. La falta de segmentación adecuada limita la capacidad de las instituciones para identificar clientes en riesgo, afectando sus finanzas y la relación con los clientes al no ofrecer soluciones personalizadas. Por ello, necesitan herramientas que permitan analizar el comportamiento de uso de las tarjetas, facilitando la predicción de riesgos, la retención de clientes y la optimización de estrategias de cobro.
LA SOLUCIÓN: 
Se enfoca en la segmentación de clientes a través de modelos de aprendizaje no supervisado. A partir de un análisis detallado de los datos de comportamiento financiero (como pagos, uso de crédito y frecuencia de compras), el objetivo es identificar patrones de uso de la tarjeta de crédito para clasificar a los clientes en diferentes segmentos. Esta segmentación permite a la empresa entender mejor el perfil de sus usuarios y anticiparse a comportamientos de riesgo, lo cual es útil para reducir pérdidas financieras y mejorar la retención de clientes.
En términos prácticos, el proceso incluye:
•	Entrenamiento de modelos de clustering: Dos algoritmos de clustering serán utilizados para identificar segmentos (como K-means y DBSCAN) con ajuste de hiperparámetros.
•	Evaluación y comparación de modelos: A través de métricas como el Silhouette Score, se evaluará cuál modelo logra una mejor segmentación.
•	Iteración y mejora: Se realizarán ajustes iterativos en las features, hiperparámetros y valores de clustering para optimizar los resultados.
En el mercado, existen diversas soluciones de machine learning que implementan clustering para problemas similares en la banca y las finanzas:
1.	Scotiabank usa algoritmos de clustering para segmentar clientes y personalizar ofertas, lo que ayuda a aumentar la retención.
2.	American Express aplica modelos de aprendizaje automático para la detección de fraudes y la segmentación de clientes según el uso de sus tarjetas, optimizando así las campañas de marketing y control de riesgo.
3.	Experian utiliza modelos de clustering y clasificación para evaluar riesgos crediticios y segmentar clientes en función de su perfil financiero, lo cual ayuda a las instituciones a decidir el tipo de producto adecuado para cada segmento de cliente.
ANÁLISIS EXPLORATORIO
El dataset contiene 8950 filas y 18 columnas, representando datos financieros de clientes con tarjetas de crédito. Cada columna se relaciona con características específicas del comportamiento de los clientes, lo cual será relevante para la segmentación en el análisis de clustering.
Descripción de las Columnas Relevantes
1.	CUST_ID: Identificador único de cada cliente.
2.	BALANCE: Monto total pendiente en la tarjeta de crédito. Indicador esencial para evaluar la dependencia de crédito de un cliente.
3.	BALANCE_FREQUENCY: Frecuencia con la cual el saldo cambia en la cuenta (valor entre 0 y 1).
4.	PURCHASES: Total de compras realizadas, útil para identificar el comportamiento de consumo.
5.	ONEOFF_PURCHASES y INSTALLMENTS_PURCHASES: Diferencian el tipo de compra, sea en un solo pago o en cuotas, lo cual es importante para entender patrones de gasto.
6.	CASH_ADVANCE: Monto total de avances en efectivo, útil para detectar clientes que usan efectivo sobre el crédito.
7.	CREDIT_LIMIT: Límite de crédito de la tarjeta, influye en el nivel de riesgo y comportamiento de gasto.
8.	PAYMENTS y MINIMUM_PAYMENTS: Monto total pagado y pago mínimo. Son críticas para evaluar la solvencia.
9.	TENURE: Tiempo de relación con la tarjeta (en meses).

![image](https://github.com/user-attachments/assets/5d484e78-55a8-4713-84df-999fe0644798)

PROCESAMIENTO DE DATOS


![image](https://github.com/user-attachments/assets/f670d61c-5e92-4af8-b2e5-39d6069e1ed3)





1.	Valores Faltantes:
o	MINIMUM_PAYMENTS tiene 313 valores nulos, lo cual puede requerir imputación de datos o ser excluido dependiendo de su impacto en el modelo. Después de realizar una imputación quedaban 73 valores nulos y como es un porcentaje muy bajo (0.81) para todo el data set se procede a borrar esa información.
o	CREDIT_LIMIT presenta 1 valor nulo, posible de manejar con métodos de imputación básicos. Se evidencia que es una tarjeta relativamente nueva ya que solo tiene 6 meses así que como es 1 solo valor faltante se procede a borrar al cliente para el estudio respectivo.
2.	Distribución y Escalado:
o	La dispersión de los datos, especialmente en columnas como BALANCE y PURCHASES, sugiere la necesidad de escalado (por ejemplo, estandarización) antes de aplicar clustering.
3.	Feature Engineering:
o	Crear nuevas variables a partir de las ya existentes, como la ratio entre BALANCE y CREDIT_LIMIT, o la proporción de pagos, podría mejorar el análisis de segmentación.
o	Promedio de Pagos Mensuales ('PAYMENTS' y TENURE): Es una medida que indica cuánto paga un cliente en promedio cada mes hacia su saldo de tarjeta de crédito.
ENTRENAMIENTO Y TUNEO DE HIPERPARÁMETROS
1. Selección del Modelo de Clustering
Basado en los datos disponibles en el dataset y el objetivo de segmentar clientes según su comportamiento financiero, se decidió utilizar K-means como el principal modelo de clustering. 
Método del Codo: Se utiliza el método del codo para encontrar el número óptimo de clusters (K) en el dataset. Este método implica calcular la suma de las distancias cuadradas dentro de cada cluster (inercia) para distintos valores de K. El punto donde el gráfico de la inercia muestra una disminución menos pronunciada indica el número adecuado de clusters.
Coeficiente de Silhouette: También se calculó el coeficiente de Silhouette para los distintos valores de K. Esta métrica mide la cohesión y separación de los clusters, ayudando a confirmar el número de clusters al elegir el valor de K que maximiza la separación.
•	Sin embargo, al no tener un buen puntaje también probamos con DBSCAN y finalmente hicimos ROBUSTSCALER y aplicamos Agrupamiento Jerárquico Aglomerativo con diferentes números de clusters.
 
![image](https://github.com/user-attachments/assets/c4780107-8ef3-40e0-92e0-89abb6759219)


INTERPRETACIÓN DE LOS CLUSTERS

![image](https://github.com/user-attachments/assets/253ee96a-ef66-476c-b24f-efcef47a4510)




BALANCE:
Cluster 0 tiene un saldo promedio ligeramente mayor en comparación con Cluster 1, pero la diferencia no es muy significativa.
Ambos clusters presentan outliers altos, lo que sugiere que algunos individuos en ambos grupos tienen saldos muy elevados.
PURCHASES:
Cluster 0 muestra un rango de compras más amplio, incluyendo varios outliers que representan clientes con niveles altos de compras.
Cluster 1 tiene un rango de compras más pequeño, lo que indica que este grupo realiza menos compras en comparación con Cluster 0.
CASH_ADVANCE:
Cluster 0 parece tener valores de adelantos en efectivo (cash advance) más altos y con una mayor variabilidad, indicando que algunos clientes dependen más del adelanto de efectivo.
Cluster 1 muestra valores de adelanto de efectivo más bajos, lo que sugiere menor dependencia de esta opción.
CREDIT_LIMIT:
Cluster 0 tiene un límite de crédito ligeramente mayor en promedio, lo cual puede reflejar un perfil crediticio más alto en comparación con Cluster 1.
A pesar de que ambos clusters presentan outliers, los límites de crédito en el Cluster 1 son generalmente más bajos.
PAYMENTS:
Cluster 0 presenta pagos más altos y más dispersos, con algunos clientes que realizan pagos bastante grandes.
Cluster 1 tiene pagos más bajos en promedio, lo que podría indicar menor capacidad o disposición para pagar grandes montos.
CREDIT_UTILIZATION_RATIO:
La utilización de crédito es baja en ambos clusters, pero Cluster 0 muestra algunos valores más altos, indicando que algunos clientes están usando una proporción más alta de su crédito disponible.
Cluster 1 tiene menos outliers altos en esta métrica, lo que sugiere que estos clientes tienden a utilizar menos de su crédito disponible.


IMPLEMENTACIÓN EN EL NEGOCIO

1.	Mitigación de Riesgos de Incumplimiento: Identificar a clientes con alto riesgo de incumplimiento para implementar estrategias de intervención y asesoramiento financiero.
2.	Optimización de la Retención de Clientes: Ofrecer beneficios y promociones adaptadas a las necesidades de cada segmento, aumentando la satisfacción y fidelización.
3.	Personalización de Ofertas de Crédito: Incrementar el uso de productos financieros a través de ofertas de crédito personalizadas para los segmentos con capacidad de consumo responsable.
La estrategia propone integrar un modelo de clustering en el sistema de gestión de clientes del banco para realizar segmentación dinámica. Esto permitirá ajustar continuamente los perfiles de clientes en función de sus datos transaccionales actualizados (balances, pagos, compras), manteniendo clusters que reflejen su comportamiento actual. Esta implementación, similar a la de empresas como American Express y Experian, ayuda al banco a anticipar riesgos y aprovechar oportunidades de negocio al adaptarse a cambios en el comportamiento financiero de los clientes.

 LIMITACIONES
 
•	Considerando el espacio temporal de 6 meses, es posible que la data no haya podido capturar cambios en el comportamiento de los tarjetahabientes.

•	La data no considera factores externos que pueden afectar el comportamiento de consumo como crisis económicas o cambios en políticas fiscales; y factores internos como el nivel de ingreso y de educación.

CONCLUSIONES Y RECOMENDACIONES

•	El análisis muestra que existen variaciones significativas en el comportamiento de uso del crédito entre los titulares de tarjetas. La creación de nuevas variables como el Ratio de Utilización del Crédito y el Promedio de Pagos Mensuales permite entender mejor la relación entre el saldo y el límite de crédito, así como la regularidad en los pagos
•	Se aplicó el algoritmo K-Means para segmentar a los usuarios en clústeres basados en sus comportamientos. Se determinó que el número óptimo de clústeres es 4, con un Silhouette Score de aproximadamente 0.445, lo que indica una buena separación entre los grupos. o   Comparando K-Means y K-Medoids, el primero mostró un mejor desempeño en términos de cohesión y separación de clústeres.
•	La evaluación de los clústeres a través del Método del Codo y la Puntuación Silhouette sugiere que los modelos están bien ajustados, con el modelo jerárquico también revelando clústeres bien definidos al identificar 2 grupos óptimos.
•	La visualización de la distribución de variables numéricas entre los clústeres muestra cómo las características de los clientes varían, lo que puede ayudar en la construcción de perfiles de riesgo crediticio.

TRABAJO FUTURO
Realizar un análisis más profundo de cada clúster para identificar características clave a utilizar para el diseño de productos y servicios financieros personalizados o estrategias de marketing.
Incorporar modelos de riesgo crediticio basados en los clústeres identificados para anticipar la probabilidad de incumplimiento y mejorar la toma de decisiones sobre otorgamiento de líneas de crédito.
Analizar la viabilidad de incorporar datos externos (indicadores económicos o demográficos) para enriquecer el análisis y mejorar la segmentación.

