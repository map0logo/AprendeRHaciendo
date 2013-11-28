**********
Motivación
**********

Hay un mito en la tecnociencia según la cual las herramientas "no son buenas
ni malas, sino dependen de como se utilicen". Sin embargo, las herramientas en
efecto condicionan el quehacer, e incluso el sentido de la investigación
científica. Este curso pretende enriquecer el abanico de las alternativas
disponibles.

Se podría intentar ser políticamente correcto y decir que queda a juicio de
cada quién decir si R es mejor o peor que otras herramientas estadísticas. Sin
embargo, desde el punto de vista de cualquier investigador riguroso el uso de R
mejora con creces las funcionalidades que ofrece una hoja de cálculo, y en
términos éticos y prácticos trabajar con software libre y de código abierto,
basado en estándares abiertos, es sin duda una opción superior.

Muchos profesionales de la informática una vez graduados evaden las tareas de
programación, de manera similar a como muchas personas evaden las matemáticas
tanto como pueden. Esto se debe a que tanto una como la otra son, por lo
general, muy mal enseñadas. En la actualidad, la programación es una destreza
básica y fundamental al alcance de cualquier persona.

Estas notas buscan son una presentación de R basada en ejemplos, en lugar de
hacer repaso pormenorizado de todos los conceptos y elementos del entorno R, se
trabajará en base a demostraciones del flujo de trabajo usual para muchos
usuarios de R con lo cuál se espera que cada persona gane comprensión de los
retos y oportunidades que ofrece el uso de una herramienta de este tipo.

¿Qué es R?
==========

R es un lenguaje de programación, que se ejecuta sobre un entorno que ofrece
capacidades de visualización y una gran cantidad de funciones y métodos de
estadística computacional, y mecanismos para extender sus funcionalidades.
Por lo tanto, el correcto manejo de R implica desarrollar destrezas de
programación.

R cuenta con el conjunto más extenso de métodos estadísticos disponibles en
cualquier software estadístico, ya sea libre o privativo, además de potentes y
flexibles capacidades de graficación. Sin embargo, el diseño de R en tanto que
lenguaje de programación, presenta debilidades que han motivado críticas
incluso por sus usuarios más fieles, un ejemplo de esto es el libro
`The R inferno`_.

Descarga e instalación
======================

Para Windows
------------

La versión de R para Windows se puede conseguir desde:
http://cran.r-project.org/bin/windows/base/

Descargar e instalar el archivo ``R-X.X.X-win.exe`` desde el enlace donde dice:
*Download R X.X.X for Windows*, donde X.X.X es la versión de R más reciente.

Para Linux
----------

Generalmente la versión disponible en los repositorios de las distintas
distribuciones está algo desactualizada, esto no es conveniente porque se
pueden tener incompatibilidad con los paquetes propios de R.

Para resolver esto se configuran los repositorios según la información que
aparece en: http://cran.r-project.org/bin/linux/

Se generan paquetes de las últimas versiones de R para Debian, Redhat, SUSE y
Ubuntu, si utiliza una distribución que no es compatible con ninguno
de estos repositorios, puede compilar la última versión de R desde las fuentes
http://cran.r-project.org/sources.html

R También está empaquetado para MacOSX Snow Leonard y superior

RStudio
=======

RStudio es un entorno de desarrollo integrado para R, disponible para Linux
(Debian/Ubuntu/Fedora/OpenSUSE), Windows y MacOSX.

Es un entorno diseñado para programación y en este sentido es lo mejor
disponible para R, aparte de ser de código abierto por lo que está siendo
continuamente mejorado.

Existen otros editores orientados a usuarios que quieren aplicar técnicas
estadísticas a datos, este enfoque termina siendo limitado porque con mucha
frecuencia se requiere modificar la estructura de los datos,
experimentar con las técnicas, aplicar las técnicas de manera iterativa,
generar reportes automáticos o configurar en detalle los graficos,
en cualquiera de estos casos es preferible un entorno de programación como
RStudio.

Desde el sitio: http://rstudio.org/download/desktop
Descargar e instalar la versión más reciente

La Interfaz de Rstudio
----------------------

Ofrece cuatro zonas personalizables: *Editor*, *Consola*, *Datos* y *Ayuda*.


Ilustración 1: Interfaz de RStudio

La primera vez que se ejecuta el programa la zona del Editor aparece
desactivada, se activará en el momento que comience a editar un script de R.

Modos de trabajo
----------------

Se comienza con el modo interactivo (en la consola) haciendo pruebas y
utilizándolo como manual de ayuda.

La serie de comandos que devuelven los resultados esperados se guardan y
modifican (en el editor) como scripts para crear rutinas reproducibles y
automatizables.

En el espacio Datos aparecen los objetos del espacio de trabajo actual, y
el histórico de comandos utilizados.

En el espacio Ayuda se encuentran por defecto el explorador de archivos, el
gestor de gráficos, el gestor de paquetes, y la interfaz de ayuda.

Todos los espacios están conectados y los cambios realizados en un espacio con
frecuencia afectan a los demás.

Estructura de un proyecto
-------------------------

Se recomienda que cada proyecto tenga una estructura de archivos con las
carpetas: (puede traducir los nombres si lo desea): ``data``, ``documents``,
``graphics`` , ``images``, ``notes``, ``code``. También puede ser otra
estructura adaptada a las preferencias del investigador, cualquiera es mejor que
tener todos los archivos sueltos en una misma carpeta.

Ilustración 2: Estructura de un proyecto de análisis de datos

También es recomendable, si se utiliza RStudio, utilizar *proyectos* con el fin
de gestionar los entornos de trabajo de manera que cada uno esté asociado a
un espacio de trabajo, un historial, y un código bien diferenciado.

Un primer ejemplo
=================

.. code-block:: r

   setwd("[ruta a]/myRfolder/")
   mydata <- read.csv("mydata.csv")
   mydata

   mydata$workshop <- factor(mydata$workshop)
   summary(mydata)

   plot(mydata$q1, mydata$q4)

   myModel <- lm(q4 ~ q1 + q2 + q3, data=mydata)
   summary(myModel)
   anova(myModel)
   plot(myModel)


.. _The R inferno: http://www.burns-stat.com/pages/Tutor/R_inferno.pdf‎