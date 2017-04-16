---
title: "General Value Added Modeling"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

Here we create the following variables so we need to create one model with pre year test scores and the create a model that produces predicted values.  We then have the actual values of those test scores (just assume those values are two points higher).  We can then compare, via a t-test if those values to see what the improvement is.

Variables we need are: Pre-year scores, income, gender, ethnicity, post test scores.
```{r}
set.seed(12345)
preYear = c(0:100)
preYear = sample(preYear, 100, replace = TRUE); head(preYear)

income = c(0:100000)
income = sample(income, 100, replace = TRUE)

gender = c("Male", "Female")
gender = sample(gender, 100, replace = TRUE)

ethnicity = c("White", "African_American", "Mixed_Ethnicity", "Other_Ethnicity")
ethnicity = sample(ethnicity, 100, replace = TRUE)

postYear = preYear + 5

data = cbind(preYear, income, gender, ethnicity, postYear)

```
Now we need to get the predicted scores for the preYear, so we can see how much of the variation in student's progress is accounted for by their general demographics.


