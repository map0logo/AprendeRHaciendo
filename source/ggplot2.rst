*******
ggplot2
*******

setwd("c:/myRfolder")
load(file = "mydata100.Rdata")

# Get rid of missing values for facets
mydata100 <- na.omit(mydata100)
attach(mydata100)
library("ggplot2")

Gráficos por defecto con qplot
==============================


.. code-block:: r
   :linenos:

   # A. Bar Plot
   myPlot <- qplot(workshop)

   # B. Histogram
   myPlot <- qplot(posttest)                  # Histogram

   # C. Useless Scatter
   myPlot <- qplot(workshop, gender)

   # D. Strip Plot - Vertical
   myPlot <- qplot(workshop, posttest)

   # E. Strip Plot - Horizontal
   myPlot <- qplot(posttest, workshop)

   # F. Scatter Plot
   myPlot <- qplot(pretest, posttest)

   grid.newpage()  # Clear page.

Gráficos de barras
------------------

# Bar plot - vertical

qplot(workshop, geom = "bar")

ggplot(mydata100, aes( workshop ) ) +
  geom_bar()

# Bar plot - horizontal

qplot(workshop, geom = "bar") + coord_flip()

ggplot(mydata100, aes(workshop) ) +
  geom_bar() + coord_flip()

# Bar plot - single bar stacked

qplot(factor(""), fill = workshop,
  geom = "bar", xlab = "") +
  scale_fill_grey(start = 0, end = 1)

ggplot(mydata100,
  aes(factor(""), fill = workshop) ) +
  geom_bar() +
  scale_x_discrete("") +
  scale_fill_grey(start = 0, end = 1)

# Pie charts, same as stacked bar but polar coordinates

qplot(factor(""), fill = workshop,
  geom = "bar", xlab = "") +
  coord_polar(theta = "y") +
  scale_fill_grey(start = 0, end = 1)

ggplot(mydata100,
  aes( factor(""), fill = workshop ) ) +
  geom_bar( width = 1 ) +
  scale_x_discrete("") +
  coord_polar(theta = "y") +
  scale_fill_grey(start = 0, end = 1)

# Bar Plots - Grouped

qplot(gender, geom = "bar",
    fill = workshop, position = "stack") +
  scale_fill_grey(start = 0, end = 1)
qplot(gender, geom = "bar",
    fill = workshop, position = "fill")  +
  scale_fill_grey(start = 0, end = 1)
qplot(gender, geom = "bar",
    fill = workshop, position = "dodge") +
  scale_fill_grey(start = 0, end = 1)

ggplot(mydata100, aes(gender, fill = workshop) ) +
  geom_bar(position = "stack") +
  scale_fill_grey(start = 0, end = 1)
ggplot(mydata100, aes(gender, fill = workshop) ) +
  geom_bar(position = "fill") +
  scale_fill_grey(start = 0, end = 1)
ggplot(mydata100, aes(gender, fill = workshop ) ) +
  geom_bar(position = "dodge") +
  scale_fill_grey(start = 0, end = 1)

# Bar Plots - Faceted

qplot(workshop, geom = "bar", facets = gender ~ . )

ggplot(mydata100, aes(workshop) ) +
  geom_bar() + facet_grid(gender ~ . )

# Bar Plots - Pre-summarized data

qplot( factor( c(1, 2) ), c(40, 60), geom = "bar",
  xlab = "myGroup", ylab = "myMeasure")

myTemp <- data.frame(
  myGroup   = factor( c(1, 2) ),
  myMeasure = c(40, 60)
)
myTemp
ggplot(data = myTemp, aes(myGroup, myMeasure) ) +
  geom_bar()

Gráficos de puntos
------------------

qplot(workshop, stat = "bin",
     facets = gender ~ . , geom = "point", size = I(4) ) +
  coord_flip()

# Same thing but suppressing legend a different way
qplot(workshop, stat = "bin",
     facets = gender ~ . , geom = "point", size = 4 ) +
  opts(legend.position = "none") +
  coord_flip()

ggplot(mydata100,
   aes(workshop, ..count.. ) ) +
   geom_point(stat = "bin", size = 4) + coord_flip()+
   facet_grid( gender ~ . )

# ---Adding Titles and Labels---

qplot(workshop, geom = "bar",
  main = "Workshop Attendance",
  xlab = "Statistics Package \nWorkshops")

ggplot(mydata100, aes(workshop, ..count..)) +
  geom_bar() +
  opts( title = "Workshop Attendance" ) +
  scale_x_discrete("Statistics Package \nWorkshops")

# Example not in text: labels of continuous scales.
ggplot(mydata100, aes(pretest,posttest ) ) +
  geom_point() +
  scale_x_continuous("Test Score Before Training") +
  scale_y_continuous("Test Score After Training")  +
  opts(title = "The Relationship is Linear")

Histogramas y gráficos de densidad
----------------------------------

# Simle Histogram
qplot(posttest, geom = "histogram")
qplot(posttest, geom = c("histogram", "rug") ) #not shown

ggplot(mydata100, aes(posttest) ) +
  geom_histogram() + geom_rug() # not shown in text

# Histogram with more bars.
qplot(posttest, geom = "histogram", binwidth = 0.5)

ggplot(mydata100, aes(posttest) ) +
  geom_histogram(binwidth = 0.5)

# Density plot
qplot(posttest, geom = "density")

ggplot(mydata100, aes(posttest)) +
  geom_density()

# Histogram with density

qplot(data = mydata100, posttest, ..density..,
  geom = c("histogram", "density") )

ggplot(data=mydata100) +
  geom_histogram( aes(posttest, ..density..) ) +
  geom_density(   aes(posttest, ..density..) ) +
  geom_rug( aes(posttest) )

# Histogram - separate plots by group

qplot(posttest, geom = "histogram", facets = gender ~ . )

ggplot(mydata100, aes(posttest) ) +
  geom_histogram() + facet_grid( gender ~ . )

# Histogram with Stacked Bars

qplot(posttest, geom = "histogram", fill = gender) +
  scale_fill_grey(start = 0, end = 1)

ggplot(mydata100, aes(posttest, fill = gender) ) +
  geom_bar() +
  scale_fill_grey(start = 0, end = 1)


Gráficos QQ
-----------

qplot(sample = posttest, stat = "qq")

ggplot(mydata100, aes(sample = posttest) ) +
  stat_qq()


Gráficos de tiras
-----------------

# Simple, but jitter too wide for our small data

qplot( factor(""), posttest, geom = "jitter", xlab = "")

ggplot(mydata100, aes(factor(""), posttest) ) +
  geom_jitter() +
  scale_x_discrete("")

# Again, with more narrow jitter

qplot( factor(""), posttest, data = mydata100, xlab = "",
  position = position_jitter(width = .02))

ggplot(mydata100, aes(factor(""), posttest) ) +
 geom_jitter(position = position_jitter(width = .02)) +
 scale_x_discrete("")

# Strip plot by group.
# First, the easy way, with too much jitter for our data:

qplot(workshop, posttest, geom = "jitter")

ggplot(mydata100, aes(workshop, posttest) ) +
  geom_jitter()

# Again, limiting the jitter for our small data set:

qplot(workshop, posttest, data = mydata100, xlab = "",
  position = position_jitter(width = .08) )

ggplot(mydata100, aes(workshop, posttest) ) +
  geom_jitter(position = position_jitter(width = .08) ) +
  scale_x_discrete("")


Gráficos de dispersión
----------------------

# Simple scatter Plot

qplot(pretest, posttest)
qplot(pretest, posttest, geom = "point")

ggplot(mydata100, aes(pretest, posttest) ) +
  geom_point()

# Scatter plot connecting points sorted on x.

qplot(pretest, posttest, geom = "line")

ggplot(mydata100, aes(pretest, posttest) ) +
  geom_line()

# Scatter plot connecting points in data set order.

qplot(pretest, posttest, geom = "path")

ggplot(mydata100, aes(pretest, posttest) ) +
  geom_path()

# Scatter plot with skinny histogram-like bars to X axis.

qplot(pretest,posttest,
  xend = pretest, yend = 50,
  geom = "segment")

ggplot(mydata100, aes(pretest, posttest) ) +
  geom_segment( aes(  pretest, posttest,
                 xend = pretest, yend = 50) )

# Scatter plot with jitter

# qplot without:
qplot(q1, q4)

# qplot with:
qplot(q1, q4, position =
  position_jitter(width = .3, height = .3) )

# ggplot without:
ggplot(mydata100, aes(x = q1, y = q2) ) +
 geom_point()

# ggplot with:
ggplot(mydata100, aes(x = q1, y = q2) ) +
  geom_point(position =
  position_jitter(width = .3,height = .3) )

# Scatter plot on large data sets

pretest2  <- round( rnorm( n = 5000, mean = 80, sd = 5) )
posttest2 <- round( pretest2 +
  rnorm( n = 5000, mean = 3, sd = 3) )
pretest2[pretest2   > 100] <- 100
posttest2[posttest2 > 100] <- 100
temp <- data.frame(pretest2, posttest2)

# Small, jittered, transparent points.

qplot(pretest2, posttest2, data = temp,
  geom = "jitter", size = I(2), alpha = I(0.15),
  position = position_jitter(width = 2) )

ggplot(temp, aes(pretest2, posttest2),
  size = 2, position = position_jitter(x = 2, y = 2) ) +
  geom_jitter(colour = alpha("black", 0.15) )

# Hexbin plots

# In qplot using default colors.
qplot(pretest2, posttest2, geom = "hex", bins = 30)

# This works too:
ggplot(temp, aes(pretest2, posttest2) )  +
  stat_binhex(bins = 30) +

# In ggplot, switching to greyscale.
ggplot(temp, aes(pretest2, posttest2) )  +
  geom_hex( bins = 30 ) +
  scale_fill_continuous(
    low = "grey80", high = "black")

# Using density contours and small points.

qplot(pretest2, posttest2, data = temp, size = I(1),
  geom = c("point","density2d"))

ggplot(temp, aes( x = pretest2, y = posttest2) ) +
 geom_point(size = 1) + geom_density2d()

# Density shading
ggplot(temp, aes( x = pretest2, y = posttest2) ) +
  stat_density2d(geom = "tile",
    aes(fill = ..density..), contour = FALSE) +
  scale_fill_continuous(
    low = "grey80", high = "black")

rm(pretest2,posttest2,temp)

# Scatter plot with regression line, 95% confidence intervals.

qplot(pretest, posttest,
  geom = c("point", "smooth"), method = lm )

ggplot(mydata100, aes(pretest, posttest) ) +
  geom_point() + geom_smooth(method = lm)

# Scatter plot with regression line but NO confidence intervals.

qplot(pretest, posttest,
  geom = c("point", "smooth"),
  method = lm, se = FALSE )

ggplot(mydata100, aes(pretest, posttest) ) +
  geom_point() +
  geom_smooth(method = lm, se = FALSE)

# Scatter with x = y line

qplot(pretest, posttest,
  geom = c("point", "abline"),
  intercept = 0, slope = 1 )

ggplot(mydata100, aes(pretest, posttest) ) +
  geom_point() +
  geom_abline(intercept = 0, slope = 1)

# Scatter plot with different point shapes for each group.

qplot(pretest, posttest, shape = gender)

ggplot(mydata100, aes(pretest, posttest) ) +
  geom_point( aes(shape = gender ) )

# Scatter plot with regressions fit for each group.

qplot(pretest, posttest,
  geom   = c("smooth", "point"),
  method = "lm", shape = gender,
  linetype  = gender)

ggplot(mydata100,
  aes(pretest, posttest, shape = gender,
  linetype = gender) ) +
  geom_smooth(method = "lm") +
  geom_point()

# Scatter plot faceted for groups

qplot(pretest, posttest,
  geom   = c("smooth", "point"),
  method = "lm", shape = gender,
  facets = workshop ~ gender)

ggplot(mydata100,
  aes(pretest, posttest, shape = gender) ) +
  geom_smooth(method = "lm") + geom_point() +
  facet_grid(workshop ~ gender)

# Scatter plot with vertical or horizontal lines

qplot(pretest, posttest,
 geom = c("point", "vline", "hline"),
 xintercept = 75, yintercept = 75)

ggplot(mydata100, aes(pretest, posttest)) +
  geom_point() +
  geom_vline(intercept = 75) +
  geom_hline(intercept = 75)

# Scatter plot with a set of vertical lines

qplot(pretest, posttest, type = "point") +
  geom_vline(xintercept = seq(from = 70,to = 80,by = 2) )

ggplot(mydata100, aes(pretest, posttest)) +
  geom_point() +
  geom_vline(xintercept = seq(from = 70,to = 80,by = 2) )

ggplot(mydata100, aes(pretest, posttest)) +
  geom_point() +
  geom_vline(xintercept = 70:80)

# Scatter plotting text labels

qplot(pretest, posttest, geom = "text",
  label = rownames(mydata100) )

ggplot(mydata100,
  aes(pretest, posttest,
  label = rownames(mydata100) ) ) +
  geom_text()

# Scatter plot matrix

plotmatrix( mydata100[3:8] )

# Small points & lowess fit.
plotmatrix( mydata100[3:8], aes( size = 1 ) ) +
  geom_smooth()

# Shape and gender fits.
plotmatrix( mydata100[3:8],
  aes( shape = gender ) ) +
  geom_smooth(method = lm)

Diagramas de cajas
------------------

# Box plot of one variable

qplot(factor(""), posttest,
  geom = "boxplot", xlab = "")

ggplot(mydata100,
  aes(factor(""), posttest) ) +
  geom_boxplot() +
  scale_x_discrete("")

# Box plot by group

qplot(workshop, posttest, geom = "boxplot" )

ggplot(mydata100,
  aes(workshop, posttest) ) +
  geom_boxplot()

# Box plot by group with jitter

# Wide jitter

qplot(workshop, posttest,
  geom = c("boxplot", "jitter") )

ggplot(mydata100,
  aes(workshop, posttest )) +
  geom_boxplot() + geom_jitter()

# Narrow jitter

ggplot(mydata100,
 aes(workshop, posttest )) +
 geom_boxplot() +
 geom_jitter(position = position_jitter(width = .1))

# Box plot for two-way interaction.

qplot(workshop, posttest,
  geom = "boxplot", fill = gender ) +
  scale_fill_grey(start = 0, end = 1)

ggplot(mydata100,
  aes(workshop, posttest) ) +
  geom_boxplot( aes(fill = gender), colour = "grey50") +
  scale_fill_grey(start = 0, end = 1)

# Error bar plot

ggplot(mydata100,
  aes( as.numeric(workshop), posttest ) ) +
  geom_jitter(size = 1,
    position = position_jitter(width = .1) )  +
  stat_summary(fun.y = "mean",
    geom = "smooth", se = FALSE) +
  stat_summary(fun.data = "mean_cl_normal",
    geom = "errorbar", width = .2, size = 1)


Mapas geográficos
-----------------

library("maps")
library("ggplot2")
myStates <- map_data("state")
head(myStates)
myStates[ myStates$region == "new york", ]

qplot(long, lat, data = myStates, group = group,
  geom = "path", asp = 1)

ggplot(data = myStates, aes(long, lat, group = group) )+
  geom_path() +
  coord_map()

myArrests <- USArrests
head(myArrests)

myArrests$region <- tolower( rownames(USArrests) )
head(myArrests)

myBoth <- merge(
  myStates,
  myArrests, by = "region")
myBoth[1:4, c(1:5,8)]

myBoth <- myBoth[order(myBoth$order), ]
myBoth[1:4, c(1:5,8)]

qplot(long, lat, data = myBoth, group = group,
  fill = Assault, geom = "polygon", asp = 1) +
  scale_fill_continuous(low = "grey80", high = "black")

ggplot(data = myBoth,
    aes(long, lat, fill = Assault, group = group) )+
  geom_polygon() +
  coord_map() +
  scale_fill_continuous(low = "grey80", high = "black")


Ejes logarítmicos
-----------------

# Change the variables
qplot( log(pretest), log(posttest) )

ggplot(mydata100,
  aes( log(pretest), log(posttest) ) ) +
  geom_point()

# Change axis labels

qplot(pretest, posttest, log = "xy")

ggplot(mydata100, aes( x = pretest, y = posttest) ) +
  geom_point() + scale_x_log10() + scale_y_log10()

# Change axis scaling

qplot(pretest, posttest, data = mydata100)  +
  coord_trans(x = "log10", y = "log10")

ggplot(mydata100, aes( x = pretest, y = posttest) ) +
  geom_point() + coord_trans(x = "log10", y = "log10")

Relación de aspecto
-------------------

# This forces x and y to be equal.
qplot(pretest, posttest) + coord_equal()

# This sets aspect ratio to height/width.
qplot(pretest, posttest) + coord_equal(ratio = 1/4)

Gráfico de barras multicuadro
-----------------------------

grid.newpage()  # clear page

# Sets up a 2 by 2 grid to plot into.
pushViewport( viewport(layout = grid.layout(2, 2) ) )

# Bar plot dodged in row 1, column 1.
myPlot <- ggplot(mydata100,
    aes(gender, fill = workshop) ) +
  geom_bar(position = "stack") +
  scale_fill_grey(start = 0, end = 1) +
  opts( title = "position = stack " )
print(myPlot, vp = viewport(
  layout.pos.row = 1,
  layout.pos.col = 1) )

# Bar plot stacked, in row 1, column 2.
myPlot <- ggplot(mydata100,
    aes(gender, fill = workshop) ) +
  geom_bar(position = "fill") +
  scale_fill_grey(start = 0, end = 1) +
  opts( title = "position = fill" )
print(myPlot, vp = viewport(
  layout.pos.row = 1,
  layout.pos.col = 2) )

# Bar plot dodged, given frames,
# in row 2, columns 1 and 2.
myPlot <- ggplot(mydata100,
    aes(gender, fill = workshop) ) +
  geom_bar(position = "dodge")  +
  scale_fill_grey(start = 0, end = 1) +
  opts( title = "position = dodge" )
print(myPlot, vp = viewport(
  layout.pos.row = 2,
  layout.pos.col = 1:2) )

Gráfico de dispersión multicuadro
---------------------------------

# Clears the page
grid.newpage()

# Sets up a 2 by 2 grid to plot into.
pushViewport( viewport(layout = grid.layout(2,2) ) )

# Scatter plot of points
myPlot <- qplot(pretest, posttest,main = "geom = point")
print(myPlot, vp = viewport(
  layout.pos.row = 1,
  layout.pos.col = 1) )

myPlot <- qplot( pretest, posttest,
          geom = "line", main = "geom = line" )
print(myPlot, vp = viewport(
  layout.pos.row = 1,
  layout.pos.col = 2) )

myPlot <- qplot( pretest, posttest,
          geom = "path", main = "geom = path" )
print(myPlot, vp = viewport(
  layout.pos.row = 2,
  layout.pos.col = 1) )

myPlot <- ggplot( mydata100, aes(pretest, posttest) ) +
          geom_segment( aes(x = pretest, y = posttest,
                         xend = pretest, yend = 58) ) +
          opts( title = "geom_segment example" )

print(myPlot,
  vp = viewport(layout.pos.row = 2, layout.pos.col = 2) )

Gráfico de dispersión para fluctuación (jitter) multicuadro
-----------------------------------------------------------

grid.newpage()
pushViewport( viewport(layout = grid.layout(1, 2) ) )

# Scatterplot without
myPlot <- qplot(q1, q4,
          main = "Likert Scale Without Jitter")
print(myPlot, vp = viewport(
  layout.pos.row = 1,
  layout.pos.col = 1) )

myPlot <- qplot(q1, q4,
  position = position_jitter(width = .3, height = .3),
  main = "Likert Scale With Jitter")
print(myPlot, vp = viewport(
  layout.pos.row = 1,
  layout.pos.col = 2) )

Comparación detallada qplot vs ggplot
=====================================

qplot(pretest, posttest,
  geom = c("point", "smooth"), method = "lm" )

# Or ggplot with default settings:

ggplot(mydata100, aes(x = pretest, y = posttest) ) +
  geom_point() +
  geom_smooth(method = "lm")

# Or with all the defaults displayed:
ggplot() +
layer(
  data    = mydata100,
  mapping = aes(x = pretest, y = posttest),
  geom    = "point",
  stat    = "identity"
) +
layer(
  data    = mydata100,
  mapping = aes(x = pretest, y = posttest),
  geom    = "smooth",
  stat    = "smooth",
  method  = "lm"
) +
coord_cartesian()