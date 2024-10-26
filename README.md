# Modelo-ML-Arbol-Telecomunicaciones

Paso 1: **Descripción del proyecto:**

* La compañía móvil Megaline no está satisfecha al ver que muchos de sus clientes utilizan planes heredados. Quieren desarrollar un modelo que pueda analizar el comportamiento de los clientes y recomendar uno de los nuevos planes de Megaline: Smart o Ultra.

Paso 2: **Importar librerias, abrir el archivo de datos**

* Importarmos las librerias a trabajar como pandas, matplotlib, scikit-learn y sus diferentes modulos para uso de importar la base de datos, generar visualización, tratamiento, análisis de datos como los gráficos correspondientes y por último generar los diferentes modelos para su recomendación.



paso 3: **Segmenta los datos fuente en un conjunto de entrenamiento, uno de validación y uno de prueba.**

* Segmentamos los datos para entrenamiento, validación y prueba. El peso es de 70%, 15% y 15% respectivamente para usarlos en los diferentes modelos desarrollados como arboles de decisión, bosque aleatorio y regresión lineal.

* 70% del conjunto de datos:

  * features_train = train_df.drop(['is_ultra'], axis=1) # entrenamiento
  * target_train = train_df['is_ultra']

* 15% del conjunto de datos para validación:
  * features_valid = valid_df.drop(['is_ultra'], axis=1) # validación
  * target_valid = valid_df['is_ultra']

* 15% del conjunto de datos para prueba
   * features_test = test_df.drop(['is_ultra'], axis=1) # prueba
   * target_test = test_df['is_ultra']



Paso 4: **Investiga la calidad de diferentes modelos cambiando los hiperparámetros.**

* Con respecto al modelo de arbol de decisión se utilizo los diferentes hiperparámetros de profundidad desde 1 hasta 19 para ver como se comporta la métrica de exactitud en la validación, se utilizo un random_state para obtener el mismo modelo para todas las profundidades.

* El modelo de bosque aleatorio se cambio los hiperparámetros de número de arboles(n_estimators) desde 10 hasta 100 arboles de 10 en 10, se fijo random_state para obtener el mismo modelo.

* El modelo de regresión logística no cuenta con hiperparámetros pero se especifico el solver=liblinear para utilizar el algoritmo adecuado al dataset, random_state para obtener el mismo modelo.

Paso 5: **Calidad del modelo usando el conjunto de prueba.**

* Los 3 modelos con sus diferentes tamaños de características y objetivos se utilizaro para la métrica de prueba.
* El modelo con el mejor resultado y para recomendar a la empresa Megaline es arbol de decisión porque sus nivel de entrenamiento es de 80% y validación de 78% y prueba del 78% a diferencia de el bosque aleatorio que tiene similar validación y prueba pero entrenamiento de 99% indicio de estar sobreajustado, por otro lado la regresión logística no cumple con las exigencias del proyecto al tener una exactitud de validación < 75%.
* Al parecer nuestro modelo esta subajustado porque el nivel de entrenamiento es de 80% y la validación y prueba son menores pero las otras opciones de bosque aleatorio que muestra un sobreajuste y la regresión lineal al no cumplir con las métricas del modelo seria nuestra mejor opción.

Paso 6: **Prueba de cordura al modelo.**

* La prueba de cordura muestra que nuestro modelo esta funcionando en buenas condiciones al convertir el DataFrame original en similar tamaño al que fue entrenado.
* El DataFrame original se segmento en 70% de caracterícticas y 30% objetivo para nuestra prueba de cordura.
* Utilizamos nuestro modelo recomendado que es model_arbol para entrenarlo 'model_arbol.fit(features_train_pc, target_train_pc)' y que realice las predicciones al objetivo 'test_predictions = model_arbol.predict(features_test_pc)'.
* Finalmente le realizamos que tan bien predijo nuestro modelo con respecto al target y obtenemos un resultado de 78% superior a la métrica exigida del proyecto.

Objetivo del proyecto: **Desarrollar un modelo que pueda analizar el comportamiento de los clientes y recomendar uno de los nuevos planes de Megaline: Smart o Ultra.**

Recomendaciones:

1. Se recomienda utilizar el modelo de arbol de decisión por  cumplir con las métricas del proyecto exactitud superior al 75% para los niveles de validación y prueba.
2. La prueba de cordura muestra la robuztes del modelo siendo el resultado de accuracy del 78%.
