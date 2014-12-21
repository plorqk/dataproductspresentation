---
title       : Simple Shiny MPG Predictor
subtitle    : 
author      : Kevin Moore
job         : Data Scientist
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [shiny]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Design

Uses the mtcars dataset from the dataset library in R

Predicts miles per gallon based on a car's horse power or weight

Uses simple linear models
* mpg ~ hp
* mpg ~ wt

No they're not the most accurate but they were simple to implement for the assignment

Making it easier for the user
The data set stored car weights in lbs/1000.  This app allows you to enter the full weight.
* User enters 2500 lbs, app changes it to fit the measuring like the data set 2.5 (lbs/1000)

---

## Limitations

Limited to max of 440 HP as the model breaks down and starts predicting negative values beyond that.

The application takes that into consideration
* If the prediction is negative it returns 0 (you can't have negative mpg!)

The choice of 7000 pounds was somewhat abitrary.  The maximum weight in the dataset is around 5450 pounds.



---

## The App Code (mostly)


```r
library(datasets)
data(mtcars)
hpfit <- lm(mpg ~ hp,data=mtcars)
wtfit <- lm(mpg ~ wt,data=mtcars)
hptest <- 140
wttest <- 1500
hppred <- predict(hpfit,data.frame(hp=hptest))
wtpred <- predict(wtfit,data.frame(wt=wttest/1000))
print(paste("Predicted test HP value:",round(hppred,1)))
```

```
## [1] "Predicted test HP value: 20.5"
```

```r
print(paste("Predicted test Weight value:",round(wtpred,1)))
```

```
## [1] "Predicted test Weight value: 29.3"
```

---

## References and More Information

Link to the app
* [Simple Shiny MPG Predictor](https://plorqk.shinyapps.io/project)

The dataset 
* [mtcars](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/mtcars.html) 

Libraries 
* [Shiny](http://shiny.rstudio.com/) 
* [Slidify](http://ramnathv.github.io/slidify/) 



