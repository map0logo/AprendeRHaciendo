*********
Regresión
*********


.. code-block:: r
   :linenos:

   # free memory
   rm(list = ls())
   gc()

.. code-block:: r
   :linenos:

   year <- rep(2008:2010, each=4)
   quarter <- rep(1:4, 3)
   cpi <- c(162.2, 164.6, 166.5, 166.0,
            166.2, 167.0, 168.6, 169.5,
            171.0, 172.1, 173.3, 174.0)
   plot(cpi, xaxt="n", ylab="CPI", xlab="")
   # draw x-axis
   axis(1, labels=paste(year,quarter,sep="Q"), at=1:12, las=3)

.. code-block:: r
   :linenos:

   cor(year,cpi)
   cor(quarter,cpi)

.. code-block:: r
   :linenos:

   fit <- lm(cpi ~ year + quarter)
   fit

.. code-block:: r
   :linenos:

   (cpi2011 <- fit$coefficients[[1]] + fit$coefficients[[2]]*2011 +
            fit$coefficients[[3]]*(1:4))


.. code-block:: r
   :linenos:

   attributes(fit)
   fit$coefficients

.. code-block:: r
   :linenos:

   # differences between observed values and fitted values
   residuals(fit)
   summary(fit)

.. code-block:: r
   :linenos:

   ## plot(fit)

.. code-block:: r
   :linenos:

   ## The chunk above simply output code to document, and the results are produced by the chunk below.
   layout(matrix(c(1,2,3,4),2,2)) # 4 graphs per page
   plot(fit)
   layout(matrix(1)) # change back to one graph per page

.. code-block:: r
   :linenos:

   library(scatterplot3d)
   s3d <- scatterplot3d(year, quarter, cpi, highlight.3d=T, type="h", lab=c(2,3))
   s3d$plane3d(fit)

.. code-block:: r
   :linenos:

   data2011 <- data.frame(year=2011, quarter=1:4)
   cpi2011 <- predict(fit, newdata=data2011)
   style <- c(rep(1,12), rep(2,4))
   plot(c(cpi, cpi2011), xaxt="n", ylab="CPI", xlab="", pch=style, col=style)
   axis(1, at=1:16, las=3,
        labels=c(paste(year,quarter,sep="Q"), "2011Q1", "2011Q2", "2011Q3", "2011Q4"))

.. code-block:: r
   :linenos:

   data("bodyfat", package="mboost")
   myFormula <- DEXfat ~ age + waistcirc + hipcirc + elbowbreadth + kneebreadth
   bodyfat.glm <- glm(myFormula, family = gaussian("log"), data = bodyfat)
   summary(bodyfat.glm)
   pred <- predict(bodyfat.glm, type="response")

.. code-block:: r
   :linenos:

   plot(bodyfat$DEXfat, pred, xlab="Observed Values", ylab="Predicted Values")
   abline(a=0, b=1)


