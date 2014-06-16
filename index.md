---
title       : ExtrapolatePetalLength 
subtitle    : A tiny app to extrapolate petal length from Iris data
author      : 
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---
## Introduction
============
This slide deck has been created using Slidify for the data products class.
This deck goes along with the project for the data products class which is to create a Shiny app.
The Shiny app is called ExtrapolatePetalLength.

I was thinking about what to do for the app and wanted to keep it simple. I wanted to use a built-in dataset from the base package as this was a project requirement. The Iris dataset was good enough since it had a decent number of observations.

--- .class #id 

## App Usage
================
* The app plots the dependence of Petal Length given Sepal Length. The data in the plot is split by Species although they're plotted in the same plot to add perspective.

* The user can then choose to play around with different Sepal Lengths for a given species. The app will reactively calculate (extrapolate) the new Petal Length based on a simple lm model. 

* Lines are also fitted through the plot to give the user a perspective of the where the extraploted values will fit.

---

## R calculations
=================
The main calculation for the app is to calculate x and y coordinates for the new value. 
This is done by finding the slope and intercept for the line for a given species.
An example calculation is shown here.

Assuming the user selects a Sepal Length of 6 and the species 'setosa' (1)

```r
data(iris)
x <- 6
setosa <- 1
fitList <- lapply(split(iris,iris$Species), lm, formula=Petal.Length~Sepal.Length)
y <- summary(fitList[[setosa]])$coef[1,1] + x * summary(fitList[[setosa]])$coef[2,1]
y
```

```
## [1] 1.593
```

Thus the new x,y coordinates for the plot are {6, 1.5928}


---

## Conclusion
=================
The app itself is here http://asangoi.shinyapps.io/ExtrapolatePetalLength

The code for the app is on github https://github.com/asangoi/ExtrapolatePetalLength

Go check it out!



