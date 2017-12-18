---
title       :  "Does Money Buy Happiness?"
description : In this chapter, you will learn how to create a model using Linear Regression Modeling.




--- type:NormalExercise lang:r xp:100 skills:1 key:59972d54f4
## Get to Know Your Data

In this exercise, you will test whether there is a connection between a person's salary and their happiness level. The first step is to get to know the data we'll be using.

You will work with a small dataset called `emp_data`, which has two columns and 20 observations. The 2 columns are `earnings` (a person's salary per day) and `s_rating` (satisfaction level)

`emp_data` = Employee dataset

`earnings` = What each employee earns in dollars per day

`s_rating` = How satisfied the employee is with his/her wage


*** =instructions

The dataset `emp_data` has already been created for you and loaded into this session. Read the steps in the script.R window and follow the instructions for each step!

*** =hint
Read the instructions in the comments in the script.R window!

*** =pre_exercise_code
```{r}
library(caret)

earnings <- c(120, 100, 700, 200, 60, 20, 200, 130, 150, 160, 170, 180, 190, 210, 220, 400, 550, 670, 695, 300)

s_rating<- c(50, 60, 80, 75, 50, 70, 75, 60, 50, 65, 70, 71,80, 82, 85, 80, 88, 90, 90, 60)

emp_data  <- data.frame(earnings, s_rating)

```

*** =sample_code
```{r}

# 1. Look at the first few rows of `emp_data` dataset. On the next line below this comment, type head(emp_data)


# 2. Now look at a summary of the dataset. Type summary(emp_data) on the line below this one



```

*** =solution
```{r}

# 1. Look at the first few rows of `emp_data` dataset. On the next line below this comment, type head(emp_data)

head(emp_data)

# 2. Now look at a summary of the dataset. Type summary(emp_data) on the line below this one

summary(emp_data)

# 3. Click the Run the Code button to see results.

# 4. After examining the results, click the Submit Answer button to proceed!

```

*** =sct
```{r}

test_function("head",
              not_called_msg = "You didn't call `head()` correctly. Remember to put `emp_data` inside of head()")

test_function("summary",
              not_called_msg = "You didn't call `summary()` correctly. Remember to put `emp_data` inside of summary()")

test_error()

success_msg("Excellent!")

```

--- type:NormalExercise lang:r xp:100 skills:1 key:c4dea87c7f

## Making a prediction

From the `emp_data` dataset, we will try to predict a new employee's satisfaction rating when he is paid $200, $400, or $1200 per day.

The `earnings` variable is the **predictor**, which means it's the data that we use to make the prediction.

The `s_rating` variable is the **class** variable, or the thing we're trying to predict. 


Let's plot the data we already have to see if there is a relationship between `earnings` and `s_rating`, or an employee satisfaction.

*** =instructions
- Plot `emp_data` with earnings on the x-axis and `s_rating` on the y-axis. Follow the steps in the script.R file.

*** =hint
This exercise requires you to fill in the blanks provided in the plot() function. Set x = earnings and y = s_rating for best results!


*** =pre_exercise_code
```{r}
library(caret)
earnings <- c(120, 100, 700, 200, 60, 20, 200, 130, 150, 160, 170, 180, 190, 210, 220, 400, 550, 670, 695, 300)

s_rating<- c(50, 60, 80, 75, 50, 70, 75, 60, 50, 65, 70, 71,80, 82, 85, 80, 88, 90, 90, 60)

emp_data  <- data.frame(earnings, s_rating)

```

*** =sample_code
```{r}

# The plot function looks like this: `plot(x=____, y=_____,  col=_____, main="_______")` 
# `x` is your independent variable  
# `y` is your dependent variable  
# `col=y` means that the color of the plot is set to the y variable.  
# `main="Regression Modeling" is the title of the plot.

#1. Make a scatterplot of emp_data with earnings on the x-axis and s_rating on the y_axis:
# Fill in x= , y= and col= fields below:  

plot(x=, y=, col= , main="Regression Modeling")

#2. Click the Run the Code button to see the plot!

#3. Click the Submit your Answer button when you are satisfied with the result

```


*** =solution
```{r}

# The plot function looks like this: `plot(x=____, y=_____,  col=_____, main="_______")`  
# `x` is your independent variable  
# `y` is your dependent variable  
# `col=y` means that the color of the plot is set to the y variable.  
# `main="Regression Modeling" is the title of the plot.

#1. Make a scatterplot of emp_data with earnings on the x-axis and s_rating on the y_axis:
# Fill in x= , y= and col= fields below:  

plot(x=, y=, col= , main="Regression Modeling")

#2. Click the Run the Code button to see the plot!

#3. Click the Submit Answer button to proceed.


```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki


test_function("plot",
              not_called_msg = "You didn't call `plot()` correctly. Remember: x = earnings and y = s_rating")

test_error()

success_msg("Good work!")

```







--- type:NormalExercise lang:r xp:100 skills:1 key:a11fe162ef
## The Caret Package

R packages can be very useful because they contain functions that aren't including in the base R code. Importing packages into your R session will allow you to access the functions in those packages. We are going to import a package for machine learning called "caret". 

To learn more about a package, type `?caret` in the console and hit enter. 

Then click the Submit Answer button.

*** =instructions

*** =hint

*** =pre_exercise_code
```{r}
library(caret)

```

*** =sample_code
```{r}
?caret
```

*** =solution
```{r}
?caret
```

*** =sct
```{r}

```
--- type:NormalExercise lang:r xp:100 skills:1 key:fccca9bca2

## Create a Training Set

It is machine learning practice to partition dataset for analysis into Training and Test sets. The purpose of doing this is to be able to test the accuracy of your model before feeding in new data.

The training set is usually 60 - 70% of the entire dataset while the test set is about 30 - 40%.

The createDataPartition() function that comes with the the caret package can be used to split the data. This function is used like so:

Suppose `myData` is the name of a dataset and I want to predict `class`, which is an attribute in the dataset `myData`.  We create a data partition where y = class. In this formula, we type the class variable as `myData$class`, using a `$` between the name of the data set and the variable name we want.

inTrain <- createDataPartition(y= myData$class, p=0.7, list=FALSE)

training <- myData[inTrain, ]

test <- myData[-inTrain, ]

`p` is set to `0.7` because we need 70% of the whole data and list is set to FALSE because we don't want the function to return `inTrain` as a list.


*** =instructions

- Use createDataPartition() function in R to partition your dataset. This example may help you: `createDataPartition(y= myData$class, p=0.7, list=FALSE)`
- Your training set should be 60% of the entire dataset (p=0.6)
- Print out the training and test sets  
- Check the dimension of both datasets to know more about the data
*** =hint
- type ?createDataPartition and hit Enter in the console to know how to use the createDataPartition() function
- Make p=0.6 and set list=FALSE
- To print a variable to the console, simply type the name of the variable on a new line.
- Use the `dim()` function on training and test set for the fourth instruction

*** =pre_exercise_code
```{r}

# Loading the required package

library(caret)

# Clean up the environment

earnings <- c(120, 100, 700, 200, 60, 20, 200, 130, 150, 160, 170, 180, 190, 210, 220, 400, 550, 670, 695, 300)

s_rating<- c(50, 60, 80, 75, 50, 70, 75, 60, 50, 65, 70, 71,80, 82, 85, 80, 88, 90, 90, 60)

emp_data  <- data.frame(earnings, s_rating)

```

*** =sample_code
```{r}

# Partition `emp_data` into training and test datasets. Note: `y=emp_data$s_rating` means the `s_rating` variable of the `emp_data` dataset.

inTrain <- createDataPartition(y= emp_data$s_rating, p=  , list= )

training <- emp_data[inTrain,]

test <- emp_data[-inTrain,]

# Type the variable names `training`  and `test` to see the contents of those variables.



# Show the dimensions of the `training` and `test` sets using the dim() function.



```

*** =solution
```{r}

# Partition `emp_data` into `training` and `test` datasets. Note: `y=emp_data$s_rating` means the `s_rating` variable of the `emp_data` dataset.

inTrain <- createDataPartition(y= emp_data$s_rating, p=0.6, list=FALSE)

training <- emp_data[inTrain,]

test <- emp_data[-inTrain,]

# Type the variable names `training`  and `test` to see the contents of those variables.



# Show the dimensions of the `training` and `test` sets

dim(training)

dim(test)


```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki


test_function("createDataPartition",
              not_called_msg = "Your createDataPartition function needs some work.`")

#test_object("inTrain")
test_object("training")
test_object("test")


test_function("dim",
              not_called_msg = "You didn't call `dim()`")

test_error()

success_msg("Good work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:1d4011a3d1
## Create Model

The `lm()` function in R is an implementation of the Linear Regression algorithm. 

You will create a linear model called `reg_model` by plugging in the training set into the `lm()` function.

This model is simply a line. Regression modelling is used to find equations(lines) that fit data.

The equation is of the form:

`y = a + bx + ei`

`y` is what we want to predict and `x` includes all the predictors required to form the model above.

`a` and `b` are **coefficients** determined by the `lm()` function we’ll use shortly. `ei` stands for errors as a result of the factors we did not consider.  

The best model is one that minimizes ei the most. 

A regression model is easy to implement but it often produces low performance models. This method is useful when the variable involved can be modeled in a linear way.

For example, to show that increase in age leads to increase in weight, or an increase in age leads to decrease in the number of hairs on one's head. This cannot be used in showing increase in library visitor per day of the week, which is usually non-linear.

`lm()` function is used like this: Suppose `myData` is the name of a dataset and I want to predict `class` an attribute in the dataset `myData` using `sex` (another attribute in myData) as my predictor:

`reg_model <- lm(class, sex, data=myData)`

We can get `a` and `b` from `reg_model` using the coef function:

a <- coef(reg_model)[1]

b <- coef(reg_model)[2]

*** =instructions
- Create a linear model called `reg_model` on the training dataset
- Plot the `training` set with earnings on the x-axis and s_rating on the y-axis
- Draw a regression line on the plot above that represents the model reg_model 
- Print out the coefficients a and b 

*** =hint
- Type `?lm` to learn how to use the lm() function
- Use `abline()` function to fit a line to the plot. Put the model name inside parenthesis.
- type ?coef to know how to use the coef() function

*** =pre_exercise_code
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_4925/datasets/ml.RData"))


# Clean up the environment

```

*** =sample_code
```{r}

# Create a linear model called reg_model

reg_model <- 


# Know more about your model

summary(reg_model)

# Plot the training set

par(cex=.8)
plot(training$earnings, training$s_rating, col = s_rating, main="Regression Modelling")


# Draw a regression line that represents the model reg_model. Use the abline() function. Put the name of the model inside the parentheses of abline()


# Print out coefficient 'a'

# Print out coefficient 'b'

```

*** =solution
```{r}

# Create a linear model called reg_model

reg_model <- lm(s_rating ~ earnings, data=training)

# Know more about your model

summary(reg_model)

# Plot the training set
par(cex=.8)
plot(training$earnings, training$s_rating, col = s_rating, main="Regression Modelling")

# Draw a regression line that represents the model reg_model. Use the abline() function. Put the name of the model inside the parentheses of abline()

abline(reg_model)

# Print out coefficient 'a'

a <- coef(reg_model)[1]

# Print out coefficient 'b'

b <- coef(reg_model)[2]

a

b

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_object("reg_model")


test_function("abline",
              not_called_msg = "You didn't call `abline()`")

test_object("a")
test_object("b")

test_error()

success_msg("Good work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:6ae37a587e
## Test Model

Here, you will create a function called `predict_happiness` to test your model. 

You are to get coefficients `a` and `b` from `reg_model` and predict satisfaction when employee is paid `$200`, `$400`, and `$1200` using `predict_hapiness` function.

predict_happiness <- function(x){
  
  a = 
  
  b =
  
  Result<- a + (b * x) 
 
  percent<- "%"
  
  cat(sprintf("The employee should be %s%s satisfied", Result, percent))
  
  }

*** =instructions
- Complete the predict_happiness function 
- Insert $200, $400 and then $1200
- Instead of using `predict_happiness` function, you can also use the built-in `predict` funtion provided by caret package.The predict function takes in the model and the test dataset like this
`predict(red_model, test)`. Put all your predicted values in a variable called `pred_rating` as in `pred_rating <- predicted(reg_model, test)`
- Compare pred_rating with the s_rating column in the test data. What do you observe? Are the predicted ratings close to the actual?

*** =hint
- Get coefficents `a` and `b` from  `reg_model` using the `coef()` function as in previous exercises.
- Use the data.frame() function to create a table with two variables pred_rating and test$s_rating.

*** =pre_exercise_code
```{r}
# load(url(""))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/ml1.RData"))
```

*** =sample_code
```{r}

# Create predict_happiness() function
# Get coefficients a and b from reg_model

predict_happiness <- function(x){

  a = 
  b = 
  Result<- a + (b * x) 
  percent<- "%"
  cat(sprintf("The employee should be %s%s satisfied", Result, percent))
}

# Predict satisfaction when employee is paid $200, $400, and $1200 

predict_happiness(200)




# pred_rating - Predicted satisfaction rating for test set

pred_rating <- 

# Compare test set s_rating with predicted s_rating for the test set



```

*** =solution
```{r}

# Create predict_happiness() function
# Get coefficients a and b from reg_model

predict_happiness <- function(x){

  a = coef(reg_model)[1]
  b = coef(reg_model)[2]
  Result<- a + (b * x) 
  percent<- "%"
  cat(sprintf("The employee should be %s%s satisfied", Result, percent))
}

# Predict satisfaction when employee is paid $200, $400, and $1200 

predict_happiness(200)





# pred_rating - Predicted satisfaction rating for test set

pred_rating <- predict(reg_model, test)

# Compare test set s_rating with predicted s_rating for the test set
data.frame(pred_rating, test$s_rating)


```

*** =sct
```{r}

test_object("predict_happiness")
test_object("pred_rating")


test_error()

success_msg("Good work!")

```

--- type:NormalExercise lang:r xp:100 skills:1 key:75c935d749
## Check Accuracy

There a number of ways to evaluate your model. For this exercise, you will use the root-mean-square error (RMSE). 
RMSE is gotten by calculating mean squared errors. This is simply a measures of deviation of predicted points from the original value.


The formula is:

  rmse  = ![](http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/rmse.png)


Where:

 * f = predicted values 
 * o = true values 
The bar above the squared differences means find the mean of the squared difference.


*** =instructions
- You can find the rmse of the test dataset by running the code below in the console:

    `sqrt(sum((pred_rating - test$s_rating)^2))`

*** =hint


*** =pre_exercise_code
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/ml2.RData"))
```

*** =sample_code
```{r}
# Check accuracy by calculating the RMSE 



```

*** =solution
```{r}

# Check accuracy by calculating the RMSE 

check_accuracy <- sqrt(sum((pred_rating - test$s_rating)^2))


```

*** =sct
```{r}
test_object("check_accuracy")


test_error()

success_msg("Good work! At this point, you can accept your model and present your work or seek to improve your model.")


```