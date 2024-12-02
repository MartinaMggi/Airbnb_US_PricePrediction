# Airbnb_US_PricePrediction
# Introducción
Este repositorio contiene el código y los materiales correspondientes al proyecto de Análisis de Datos y Predicción de Precios de Airbnb, realizado como parte de la asignatura Ciencia de Datos en la carrera de Ingeniería Industrial. El objetivo de este proyecto fue analizar datos de Airbnb de anuncios en Estados Unidos y desarrollar modelos para predecir el precio.

## Autores

* Juan Ignacio Gaitez Obando
* Martina Maggi

# Descripción del Dataset
El conjunto de datos utilizado se compone de 19,309 publicaciones y 29 variables, que describen características de las propiedades, como el tipo de propiedad, el tipo de habitación disponible, el barrio donde se encuentran ubicadas, la cantidad de habitaciones, el tipo de cama, y la información sobre el alquiler como la política de cancelación, las opiniones de los huéspedes, la fecha desde que el anfitrión está en Airbnb, entre otras.

A continuación, se puede observar la distribución de la variable objetivo, que en este caso es el precio de las propiedades.

# Análisis exploratorio de datos (EDA)
Durante el análisis exploratorio del conjunto de datos, se observó que las variables numéricas no eran predominantes, por lo que fue necesario realizar la conversión adecuada de las categorías en los features correspondientes. Las conversiones fueron las siguientes:

first_review, host_since, last_review → tipo fecha.
cleaning_fee, instant_bookable, host_identity_verified, host_has_profile_pic → tipo booleano.
host_response_rate → tipo float.
Además, eliminamos las columnas name y thumbnail_url ya que no eran relevantes para el análisis.

En cuanto a los tipos de propiedad, el conjunto de datos contiene 27 categorías de propiedades, como: "House", "Apartment", "Loft", "Condominium", entre otras.

Manipulación de Outliers
Se visualizó cómo se distribuyen los precios según el tipo de propiedad. El valor del percentil 97 fue $564.59, mientras que el valor del percentil 1 fue $28.99. Para analizar los outliers:

Cantidad de valores por encima del percentil 95: 966.
Cantidad de valores por debajo del percentil 1: 172.
Se calcularon los límites inferior y superior para detectar los outliers:

Límite inferior: $20.49.
Límite superior: $419.5.
Se eliminaron los outliers para evitar un sobreajuste en el modelo.

Manipulación de nulos
Las variables ‘host_response_rate’ y ‘last_review’ no fueron consideradas relevantes para el modelo, por lo que se eliminaron del análisis.

Para las variables ‘bathroom’, ‘bedroom’ y ‘beds’, se eliminaron únicamente los registros con valores nulos debido a la baja proporción de datos faltantes.

En la variable ‘host_since’, los valores nulos fueron poblados tomando como referencia la fecha de ‘first_review’. Si la fecha de ‘first_review’ era posterior a la de ‘host_since’, se intercambiaron las fechas.

La variable ‘reviews_score_rating’ fue reemplazada por su valor medio en los registros con valores nulos, y los valores nulos en ‘neighbourhood’ fueron completados según el zipcode correspondiente. Las variables sin ‘zipcode’ ni ‘neighbourhood’ fueron eliminadas.

Codificación de variables categóricas
Para la variable ‘room_type’, se utilizó una codificación secuencial, asignando un número a cada categoría. También se aplicó una codificación similar en ‘cancellation_policy_mapping’, con valores de 0 a 5, dependiendo de la política de cancelación.

La variable ‘property_type’ fue procesada con un Label Encoder, transformando las categorías en valores numéricos binarios. Para la variable ‘amenities’, se realizaron varias transformaciones, clasificando las comodidades de las propiedades en 27 categorías, y creando variables dummy para cada una de ellas.

# Análisis de correlaciones
Se generaron heatmaps y una matriz de correlaciones para visualizar cómo se relacionan las variables entre sí. De esta matriz, se observó que las variables ‘beds’, ‘bedrooms’ y ‘bathrooms’ estaban fuertemente relacionadas con el precio, mientras que la variable ‘room_type’ mostraba una relación inversa: cuanto mayor valor tenía la variable, menor era el precio.

Además, se analizó cómo las amenities influían en el precio. Variables como ‘Kids’, ‘TV’, ‘Gym’ y ‘Accessibility’ mostraron una correlación positiva con el precio.

# Materiales y métodos
Para realizar el análisis exploratorio, se utilizaron las siguientes librerías de Python:

* Pandas
* Numpy
* Seaborn
* Matplotlib
* Sklearn
* Plotly
* gdown


# Experimentos y resultados
A partir del análisis realizado, se llevó a cabo una predicción del precio de los hospedajes mediante un modelo de regresión lineal. Primero, se separaron las columnas numéricas de las categóricas y se aplicaron varias etapas de preprocesamiento de datos. Esto incluyó:

* Manejo de valores nulos: se rellenaron las variables numéricas con la media de cada columna y las categóricas con el valor más frecuente.
* Escalado de variables numéricas para asegurar que todas las características estuvieran en la misma escala.
*Codificación de variables categóricas.

Después de procesar las variables, se dividieron los datos en conjuntos de entrenamiento (80%) y prueba (20%). 

# Discusión y conclusiones

Los resultados muestran que el modelo de Random Forest superó a la regresión lineal en términos de precisión, y el uso de técnicas como PCA contribuyó a mejorar el rendimiento del modelo. A pesar de las mejoras en las métricas, el modelo sigue presentando márgenes de error que pueden ser optimizados con técnicas adicionales o datos más completos.
