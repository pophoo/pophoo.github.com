---
layout: post
title: "caret包"
description: ""
category: R
tags: [caret, R]
---
{% include JB/setup %}

# [caret包](http://caret.r-forge.r-project.org/)

## [Data Sets](http://caret.r-forge.r-project.org/datasets.html#)

## [Visualizations](http://caret.r-forge.r-project.org/visualizations.html)

### Scatterplot Matrix


{% highlight r %}
library(AppliedPredictiveModeling)
transparentTheme(trans = 0.4)

library(caret)
featurePlot(x = iris[, 1:4], y = iris$Species, plot = "pairs", auto.key = list(columns = 3))
{% endhighlight %}

![center](./img/posts/2014-05-23-caret-package/fig1.png) 


### Scatterplot Matrix with Ellipses


{% highlight r %}
library(AppliedPredictiveModeling)
transparentTheme(trans = 0.4)
library(caret)
featurePlot(x = iris[, 1:4], y = iris$Species, plot = "ellipse", auto.key = list(columns = 3))
{% endhighlight %}

![center](./img/posts/2014-05-23-caret-package/fig2.png) 


### Overlayed Density Plots


{% highlight r %}
library(AppliedPredictiveModeling)
library(caret)
transparentTheme(trans = 0.9)
featurePlot(x = iris[, 1:4], y = iris$Species, plot = "density", scales = list(x = list(relation = "free"), 
    y = list(relation = "free")), adjust = 1.5, pch = "|", layout = c(4, 1), 
    auto.key = list(columns = 3))
{% endhighlight %}

![center](./img/posts/2014-05-23-caret-package/fig3.png) 


### Box Plots


{% highlight r %}
library(AppliedPredictiveModeling)
library(caret)
transparentTheme(trans = .9)
featurePlot(x = iris[, 1:4],
                  y = iris$Species,
                  plot = "box",
                  ## Pass in options to bwplot() 
                  scales = list(y = list(relation="free"),
                                x = list(rot = 90)),
                  layout = c(4,1 ),
                  auto.key = list(columns = 2))
{% endhighlight %}

![center](./img/posts/2014-05-23-caret-package/fig4.png) 


## Scatter Plots


{% highlight r %}
library(mlbench)
data(BostonHousing)
regVar <- c("age", "lstat", "tax")
str(BostonHousing[, regVar])
{% endhighlight %}



{% highlight text %}
## 'data.frame':	506 obs. of  3 variables:
##  $ age  : num  65.2 78.9 61.1 45.8 54.2 58.7 66.6 96.1 100 85.9 ...
##  $ lstat: num  4.98 9.14 4.03 2.94 5.33 ...
##  $ tax  : num  296 242 242 222 222 222 311 311 311 311 ...
{% endhighlight %}



{% highlight r %}

library(AppliedPredictiveModeling)
library(caret)
transparentTheme(trans = 0.9)
theme1 <- trellis.par.get()
theme1$plot.symbol$col = rgb(0.2, 0.2, 0.2, 0.4)
theme1$plot.symbol$pch = 16
theme1$plot.line$col = rgb(1, 0, 0, 0.7)
theme1$plot.line$lwd <- 2
trellis.par.set(theme1)
featurePlot(x = BostonHousing[, regVar], y = BostonHousing$medv, plot = "scatter", 
    layout = c(3, 1))
{% endhighlight %}

![center](./img/posts/2014-05-23-caret-package/fig51.png) 

{% highlight r %}
featurePlot(x = BostonHousing[, regVar], y = BostonHousing$medv, plot = "scatter", 
    type = c("p", "smooth"), span = 0.5, layout = c(3, 1))
{% endhighlight %}

![center](./img/posts/2014-05-23-caret-package/fig52.png) 

## 引用

1. [Applied Predictive Modeling](http://appliedpredictivemodeling.com/)
1. [Building Predictive Models in R Using the caret Package
](http://www.jstatsoft.org/v28/i05)





