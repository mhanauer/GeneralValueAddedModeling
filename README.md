---
title: "General Value Added Modeling"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Here is an example using a fake data set on the basics for value added modeling for measuring teacher impact.  Below is the code for generating the fake data.  There are three covariates, income, gender, and ethnicity.  PreYear is a score on some standardized assessment that is provided to the teacher’s classroom.  PostYear is the same assessment provided to that same classroom one year later, which will be compared to the predicted values of preYear after accounting for the covariates impact.  For the purposes of the example, postYear is just 10 units added on to each of the preYear scores.
```{r}
set.seed(12345)
preYear = c(0:100)
preYear = sample(preYear, 100, replace = TRUE); head(preYear)

income = c(0:100000)
income = sample(income, 100, replace = TRUE)

gender = c("Male", "Female")
gender = sample(gender, 100, replace = TRUE)
gender = as.numeric(factor(gender))

ethnicity = c("White", "African_American", "Mixed_Ethnicity", "Other_Ethnicity")
ethnicity = sample(ethnicity, 100, replace = TRUE)
ethnicity = as.numeric(factor(ethnicity))

postYear = preYear + 10

data = cbind(preYear, income, gender, ethnicity, postYear)
data = as.data.frame(data)

```
Now we need to get the predicted scores for the preYear variable, so we can see how much of the variation in student's progress is accounted for by their general demographics.  This can be done by creating a linear regression model with income, gender, and ethnicity predicting preYear scores.  Then the predict function is used to generate predicted values for preYear from the model. 

Then we can run a simple t-test on the predicated values and the postYear scores to evaluate what "value" or increase in scores can be attributed to the teacher.

```{r}
model = lm(preYear ~ income + gender + ethnicity, data = data)
predPreYear = predict(model, data)
t.test(postYear, predPreYear)
```


