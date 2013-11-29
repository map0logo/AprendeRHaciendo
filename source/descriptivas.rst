************************
Estadística descriptivas
************************

Variables individuales
======================

.. code-block:: r
   :linenos:

   summary(iris)


.. code-block:: r
   :linenos:

   quantile(iris$Sepal.Length)
   quantile(iris$Sepal.Length, c(.1, .3, .65))

.. code-block:: r
   :linenos:

   var(iris$Sepal.Length)
   hist(iris$Sepal.Length)

.. code-block:: r
   :linenos:

   plot(density(iris$Sepal.Length))

.. code-block:: r
   :linenos:

   table(iris$Species)
   pie(table(iris$Species))

.. code-block:: r
   :linenos:

   barplot(table(iris$Species))

Múltiples variables
===================

.. code-block:: r
   :linenos:

   cov(iris$Sepal.Length, iris$Petal.Length)
   cov(iris[,1:4])
   cor(iris$Sepal.Length, iris$Petal.Length)
   cor(iris[,1:4])

.. code-block:: r
   :linenos:

   aggregate(Sepal.Length ~ Species, summary, data=iris)

.. code-block:: r
   :linenos:

   boxplot(Sepal.Length~Species, data=iris)

.. code-block:: r
   :linenos:

   with(iris, plot(Sepal.Length, Sepal.Width,
                   col=Species, pch=as.numeric(Species)))

.. code-block:: r
   :linenos:

   plot(jitter(iris$Sepal.Length), jitter(iris$Sepal.Width))

.. code-block:: r
   :linenos:

   pairs(iris)

Y seguimos explorando
=====================

.. code-block:: r
   :linenos:

   library(scatterplot3d)
   scatterplot3d(iris$Petal.Width, iris$Sepal.Length, iris$Sepal.Width)

.. code-block:: r
   :linenos:

   ## library(rgl)
   ## plot3d(iris$Petal.Width, iris$Sepal.Length, iris$Sepal.Width)

.. code-block:: r
   :linenos:

   distMatrix <- as.matrix(dist(iris[,1:4]))
   heatmap(distMatrix)

.. code-block:: r
   :linenos:

   library(lattice)
   levelplot(Petal.Width~Sepal.Length*Sepal.Width, iris, cuts=9,
             col.regions=grey.colors(10)[10:1])

.. code-block:: r
   :linenos:

   filled.contour(volcano, color=terrain.colors, asp=1,
                  plot.axes=contour(volcano, add=T))

.. code-block:: r
   :linenos:

   persp(volcano, theta=25, phi=30, expand=0.5, col="lightblue")

.. code-block:: r
   :linenos:

   library(MASS)
   parcoord(iris[1:4], col=iris$Species)

.. code-block:: r
   :linenos:

   library(lattice)
   parallelplot(~iris[1:4] | Species, data=iris)


.. code-block:: r
   :linenos:

   library(ggplot2)
   qplot(Sepal.Length, Sepal.Width, data=iris, facets=Species ~.)

Guardar un gráfico en un archivo
--------------------------------

.. code-block:: r
   :linenos:

   ## # save as a PDF file
   ## pdf("myPlot.pdf")
   ## x <- 1:50
   ## plot(x, log(x))
   ## graphics.off()
   ## #
   ## # Save as a postscript file
   ## postscript("myPlot2.ps")
   ## x <- -20:20
   ## plot(x, x^2)
   ## graphics.off()
