**********************
Análisis Multivariante
**********************


.. code-block:: r
   :linenos:

   # free memory
   rm(list = ls())
   gc()

.. code-block:: r
   :linenos:

   set.seed(8953)


.. code-block:: r
   :linenos:

   iris2 <- iris
   iris2$Species <- NULL
   (kmeans.result <- kmeans(iris2, 3))

.. code-block:: r
   :linenos:

   table(iris$Species, kmeans.result$cluster)

.. code-block:: r
   :linenos:

   plot(iris2[c("Sepal.Length", "Sepal.Width")], col = kmeans.result$cluster)
   # plot cluster centers
   points(kmeans.result$centers[,c("Sepal.Length", "Sepal.Width")], col = 1:3,
          pch = 8, cex=2)

.. code-block:: r
   :linenos:

   library(fpc)
   pamk.result <- pamk(iris2)
   # number of clusters
   pamk.result$nc
   # check clustering against actual species
   table(pamk.result$pamobject$clustering, iris$Species)

.. code-block:: r
   :linenos:

   layout(matrix(c(1,2),1,2)) # 2 graphs per page
   plot(pamk.result$pamobject)
   layout(matrix(1)) # change back to one graph per page

.. code-block:: r
   :linenos:

   pam.result <- pam(iris2, 3)
   table(pam.result$clustering, iris$Species)

.. code-block:: r
   :linenos:

   layout(matrix(c(1,2),1,2)) # 2 graphs per page
   plot(pam.result)
   layout(matrix(1)) # change back to one graph per page

.. code-block:: r
   :linenos:

   set.seed(2835)

.. code-block:: r
   :linenos:

   idx <- sample(1:dim(iris)[1], 40)
   irisSample <- iris[idx,]
   irisSample$Species <- NULL
   hc <- hclust(dist(irisSample), method="ave")

.. code-block:: r
   :linenos:

   plot(hc, hang = -1, labels=iris$Species[idx])
   # cut tree into 3 clusters
   rect.hclust(hc, k=3)
   groups <- cutree(hc, k=3)

.. code-block:: r
   :linenos:

   library(fpc)
   iris2 <- iris[-5] # remove class tags
   ds <- dbscan(iris2, eps=0.42, MinPts=5)
   # compare clusters with original class labels
   table(ds$cluster, iris$Species)

.. code-block:: r
   :linenos:

   plot(ds, iris2)

.. code-block:: r
   :linenos:

   plot(ds, iris2[c(1,4)])

.. code-block:: r
   :linenos:

   plotcluster(iris2, ds$cluster)

.. code-block:: r
   :linenos:

   # create a new dataset for labeling
   set.seed(435)
   idx <- sample(1:nrow(iris), 10)
   newData <- iris[idx,-5]
   newData <- newData + matrix(runif(10*4, min=0, max=0.2), nrow=10, ncol=4)
   # label new data
   myPred <- predict(ds, iris2, newData)
   # plot result
   plot(iris2[c(1,4)], col=1+ds$cluster)
   points(newData[c(1,4)], pch="*", col=1+myPred, cex=3)
   # check cluster labels
   table(myPred, iris$Species[idx])


