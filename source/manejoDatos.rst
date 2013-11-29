***************
Manejo de Datos
***************

Guardar y cargar datos en R
===========================

Conjuntos de datos Rdata
------------------------

Los datos en R se pueden guardar como archivos ``.Rdata`` usando la función
``save()``. Después de lo cual pueden cargarse en R mediante la función
``load()``. En el código a continuación ``rm()`` borra el objeto ``a`` de R.

.. code-block:: r
   :linenos:

   a <- 1:10
   save(a, file="./data/dumData.Rdata")
   rm(a)
   load("./data/dumData.Rdata")
   print(a)

Cada vez que se dice *cargar en R* o *borrar de R*, se refiere al espacio de
trabajo de R, donde residen los objetos a los que R tiene acceso para realizar
operaciones.

En la línea 1, se crea un vector numérico con los valores `1, 2, ... 10` usando
la notación resumida ``1:10`` y se asigna a la variable ``a``.

Se utiliza la función ``save()`` para guardarlo en un archivo con el nombre
``dumData.Rdata``, debe existir en este caso una carpeta ``data`` en el
directorio de trabajo actual de lo contrario devolverá un error.

Para verificar cual es nuestro directorio de trabajo actual podemos utilizar la
función ``getwd()``. Si en necesario lo podemos cambiar con la función
``setwd()`` tal y como se hizo en :ref:`un-primer-ejemplo`.

Importar y exportar desde archivos .CSV
---------------------------------------

Es posible crear archivos separados por comas, compatibles con las hojas de
cálculo como EXCEL o LibreOffice Calc.

.. code-block:: r
   :linenos:

   var1 <- 1:5
   var2 <- (1:5) / 10
   var3 <- c("R", "and", "Data Mining", "Examples", "Case Studies")
   df1 <- data.frame(var1, var2, var3)
   names(df1) <- c("VariableInt", "VariableReal", "VariableChar")
   write.csv(df1, "./data/dummmyData.csv", row.names = FALSE)
   df2 <- read.csv("./data/dummmyData.csv")
   print(df2)

Se crea el vector ``var1`` de forma similar al ejemplo anterior, para el
vector ``var2`` se crea un vector con los valores correlativos del 1 al 5
``1:5`` y este valor se divide entre 10, es decir, se obtiene un nuevo vector
en el que cada elemento es dividido por 10.

.. code-block:: rconsole
   :linenos:

    > (1:5) / 10
   [1] 0.1 0.2 0.3 0.4 0.5

En estos casos se dice que el operador ``/`` está *vectorizado* ya que aplica a
todo el vector. Es el comportamiento usual de los operadores aritméticos cuando
se utilizan con vectores y matrices.

El vector ``var3`` se contruye *combinando* valores distintos con la función
``c()``. Esta es una de las formas más comunes de crear vectores en R. En este
caso como los valores son cadenas de caracteres, el vector es de tipo
``character``.

Y con ``data.frame(var1, var2, var3)`` se crea un dataframe en el que cada
columna se corresponde con los vectores recién creados. Nótese que los tres
vectores en este caso tienen la misma longitud, de lo contrario se repetirían
los valores de los vectores más pequeños hasta completar un número de registros
igual al del vector más grande.

.. code-block:: rconsole
   :linenos:

   > data.frame(1:2, 1:5, 1:10)
      X1.2 X1.5 X1.10
   1     1    1     1
   2     2    2     2
   3     1    3     3
   4     2    4     4
   5     1    5     5
   6     2    1     6
   7     1    2     7
   8     2    3     8
   9     1    4     9
   10    2    5    10

La sentencia ``names(df1) <- c("VariableInt", "VariableReal", "VariableChar")``
establece los nombres de las columnas de ``df1`` cada valor del vector creado
con la función ``c()`` se corresponde con cada una de las columnas.

Al ejecutar ``write.csv(df1, "./data/dummmyData.csv", row.names=FALSE)`` se
genera un archivo separado por comas de nombre ``dummmyData.csv`` en la carpeta
``data``. La opción ``row.names=FALSE`` indica que el archivo no va a incluir
los nombres de fila (que son los números de fila por defecto) como un campo
adicional.

Finalmente, se cargan los datos del archivo recién creado en un nuevo dataframe
``df2`` con ``df2 <- read.csv("./data/dummmyData.csv")`` y se imprime su
contenido para verificar que todo ha ido bien.


.. note:: Archivos SAS, EXCEL y Bases de datos

   Es posible trabajar de la misma forma con archivos de SAS, con archivos de
   EXCEL y con bases de datos, pero estas operaciones en general dependen del
   sistema operativo y del software instalado. Por ejemplo, en el caso de
   trabajar con los archivos de SAS hay que tener instalado SAS.


Acceder a los datos
===================

El conjunto de datos iris
-------------------------

Es un conjunto incorporado a R de manera que no necesita ser cargado. Consiste
en 50 muestras de tres clases de flores de iris.

Este conjunto de datos es clásico y cuenta incluso con su propia página web
http://en.wikipedia.org/wiki/Iris_flower_data_set

Una clase de flores es linealmente separable de las otras dos, mientras que las
dos últimas no son linealmente separables la una de la otra. El conjunto cuenta
con cinco datos:

* longitud de los sépalos en cm,
* ancho de los sépalos en cm,
* longitud de los pétalos cm,
* ancho de los petalos en cm, y
* clase: Iris Setosa, Iris Versicolour, e Iris Virginica.

Revisar los datos
-----------------

.. code-block:: r
   :linenos:

   dim(iris)
   names(iris)
   str(iris)
   attributes(iris)

Con las funciones dadas se obtiene las *dimensiones* del conjunto de datos
``dim()``, los *nombres* de los campos ``names()``, una descripción compacta
de la *estructura* ``str()``, y una versión extendida de los *atributos*
``attributes()``.

.. code-block:: r
   :linenos:

   iris[1:5, ]
   head(iris)
   tail(iris)

Los dataframe se pueden ver como matrices a los que se accede por filas y
columnas de la forma ``df[fil, col]``. Así, la sentencia ``iris[1:5, ]``
devuelve todas los campos (ya que después de la columna está vacío) para los
primeros cinco registros (filas de la 1 a la 5).

Las funciones ``head()`` y ``tail()`` devuelven los primeros y los últimos
registros de un conjunto de datos, por defecto 6, aunque se puede establecer
con el parámetro ``n=``.

.. code-block:: rconsole
   :linenos:

   > iris[1:10, "Sepal.Length"]
   [1] 5.1 4.9 4.7 4.6 5.0 5.4 4.6 5.0 4.4 4.9
   > iris$Sepal.Length[1:10]
   [1] 5.1 4.9 4.7 4.6 5.0 5.4 4.6 5.0 4.4 4.9

También es posible los valores de una columna en particular, en el código
anterior se muestran dos formas alternativas de obtener los valores del campo
``Sepal.length`` en los diez primeros registros. En el primer caso utilizando
notación matricial ``iris[1:10, "Sepal.Length"]``, y en el segundo accediendo
primero al campo mediante la notación ``objeto$campo`` y luego extrayendo los
primeros diez valores mediante ``[1:10]``.


