---
title       : "Machine Learning: Opening up the Black Box"
description : This chapter provides an introduction to machine learning and hands-on practice developing two common machine learning models - linear regression and random forests.
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf
---


## The Buzzword
```yaml
type: PureMultipleChoiceExercise
lang: r
xp: 50
skills: 1
key: 53d9ea348c
```

According to Wikipedia, Arthur Samuel in 1959 defined Machine Learning as the subfield of computer science that gives computers the ability to learn without being explicitly programmed. This means that machines will be given the ability to make inferences and observation by learning from data. In other words, **machine learning is the science of teaching the machine to identify trends and patterns in data that cannot easily be detected by humans.**

### `CLASS ACTIVITY:`
From the above definition, which of the following is not a Machine Learning Task?

`@possible_answers`
- Self driving cars
- A program that prints the next 20 leap years
- A program that categorizes emails into spam and non-spam
- A program predicting where galaxies might be located

`@hint`
Take a look at the options. Which task requires explicitly programming the computer?

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Oops! Try again."
msg_success <- "Exactly! Even I can calculate the next 50 leap years and I'm only human."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))

```
---

## Machine Learning Process

```yaml
type: PureMultipleChoiceExercise
lang: r
xp: 25
skills: 1
key: 40173c5d8e
```

A human can learn the voices of 10 (or perhaps 100) co-workers and be able to identify them without looking. A machine, however, can learn the voices of over 10,000 people and be able to predict whose voice it is. This is possible with machine learning.

The steps involved in Machine Learning include the following:

- Getting data
- Pre-processing the data (Clean, Prepare, Manipulate Data and Exploratory Data Analysis)
- Training the Model
- Testing the Model
- Post-Processing the data (Visualize, Evaluate, Improve the Model & Presentation)

The first two steps are typical for any analysis involving data, but **creating a model is a critical part of machine learning.**

### `CLASS ACTIVITY:`

If machines can learn 10,000 voices and humans can only learn between 10 and 100, does that make computers smarter than humans?

`@possible_answers`
- Definitely
- No
- Maybe

`@hint`
Trust your instinct on this one!

`@sct`
```{r}

msg_def <- "Computers are getting smarter every day. But humans still have certain advantages, like common sense and instinct."
msg_success <- "It's a debatable point, but humans are still pretty smart."
msg_maybe <- "You have a right to wonder. Some experts say that in the near future, computers will be smarter than humans. We shall see!"
test_mc(correct = 2, feedback_msgs = c(msg_def, msg_success, msg_maybe))

```

---

## The Model: the Secret Weapon in Machine Learning

```yaml
type: PureMultipleChoiceExercise
lang: r
xp: 100
skills: 1
key: 06d44465f4
```


A model is an artifact or a formula created by the process of learning from previous data. When you plug in historical data into a machine learning algorithm, you get a model.

In voice recognition, the machine uses a model that takes in an input (a human voice), does some processing and predicts the name of the person as the output.

### `CLASS ACTIVITY:`

A good machine learning model depends on which of the following?

`@possible_answers`
- Type of the data and software or statistical tool used for analysis
- Type of machine learning algorithm used and software or statistical tool used for analysis
- The quality of the dataset and type of machine learning algorithm used

`@hint`
Clean historical data + good machine learning algorithm = Great Model!
`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}

```

`@solution`
```{r}

```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Try again. There is a better answer!"
msg_success <- "Exactly!"
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_success))
```

---
## Examining Your Data
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 59972d54f4
```
In this exercise, you will test whether there is a connection between a person's salary and their happiness level. The first step is to get to know the data we'll be using.

You will work with a small dataset called `emp_data`, which has two columns and 20 observations. The 2 columns are `earnings` (a person's salary per day) and `s_rating` (satisfaction level)

`emp_data` = Employee dataset

`earnings` = What each employee earns in dollars per day

`s_rating` = How satisfied the employee is with his/her wage


`@possible_answers`

The dataset `emp_data` has already been created for you and loaded into this session. Read the steps in the script.R window and follow the instructions for each step!

`@hint`
Read the instructions in the comments in the script.R window!

`@pre_exercise_code`
```{r}
library(caret)

earnings <- c(120, 100, 700, 200, 60, 20, 200, 130, 150, 160, 170, 180, 190, 210, 220, 400, 550, 670, 695, 300)

s_rating<- c(50, 60, 80, 75, 50, 70, 75, 60, 50, 65, 70, 71,80, 82, 85, 80, 88, 90, 90, 60)

emp_data  <- data.frame(earnings, s_rating)

```

`@sample_code`
```{r}

# 1. Look at the first few rows of `emp_data` dataset. On the next line below this comment, type head(emp_data)


# 2. Now look at a summary of the dataset. Type summary(emp_data) on the line below this one


# 3. Click the Run the Code button to see results.


# 4. After examining the results, click the Submit Answer button to proceed!

```

`@solution`
```{r}

# 1. Look at the first few rows of `emp_data` dataset. On the next line below this comment, type head(emp_data)

head(emp_data)

# 2. Now look at a summary of the dataset. Type summary(emp_data) on the line below this one

summary(emp_data)

# 3. Click the Run the Code button to see results.

# 4. After examining the results, click the Submit Answer button to proceed!

```

`@sct`
```{r}

test_function("head",
              not_called_msg = "You didn't call `head()` correctly. Remember to put `emp_data` inside of head()")

test_function("summary",
              not_called_msg = "You didn't call `summary()` correctly. Remember to put `emp_data` inside of summary()")

test_error()

success_msg("Excellent!")

```
---


## Understanding the Model Variables
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: c4dea87c7f
```

From the `emp_data` dataset, we will try to predict a new employee's satisfaction rating when he is paid $200, $400, or $1200 per day.

The `earnings` variable is the **predictor**, which means it's the data that we use to make the prediction.

The `s_rating` variable is the **class** variable, or the thing we're trying to predict.


Let's plot the data we already have to see if there is a relationship between `earnings` and `s_rating`, or an employee satisfaction.

`@possible_answers`
- Plot `emp_data` with earnings on the x-axis and `s_rating` on the y-axis. Follow the steps in the script.R file.

`@hint`
This exercise requires you to fill in the blanks provided in the plot() function. Set x = earnings and y = s_rating for best results!


`@pre_exercise_code`
```{r}
library(caret)
earnings <- c(120, 100, 700, 200, 60, 20, 200, 130, 150, 160, 170, 180, 190, 210, 220, 400, 550, 670, 695, 300)

s_rating<- c(50, 60, 80, 75, 50, 70, 75, 60, 50, 65, 70, 71,80, 82, 85, 80, 88, 90, 90, 60)

emp_data  <- data.frame(earnings, s_rating)

```

`@sample_code`
```{r}

#1. Make a scatterplot of emp_data with earnings on the x-axis and s_rating on the y_axis. But first, read about how a plot function is constructed:
# The plot function looks like this: `plot(x=____, y=_____,  col=_____, main="_______")`
# `x` is your independent variable  
# `y` is your dependent variable  
# `col=y` means that the color of the plot is set to the y variable.  
# `main="Regression Modeling" is the title of the plot.

# Now fill in the blanks:
plot(x= , y= , col= , main="Regression Modeling")

#2. Click the Run the Code button to see the plot!

#3. Click the Submit your Answer button when you are satisfied with the result

```


`@solution`
```{r}

#1. In this exercise, you will make a scatterplot of emp_data with earnings on the x-axis and s_rating on the y_axis. But first, read about how a plot function is constructed:
# The plot function looks like this: `plot(x=____, y=_____,  col=_____, main="_______")`
# `x` is your independent variable  
# `y` is your dependent variable  
# `col=y` means that the color of the plot is set to the y variable.  
# `main="Regression Modeling" is the title of the plot.

# Now fill in the blanks:
plot(x=earnings, y=s_rating, col=s_rating, main="Regression Modeling")

#2. Click the Run the Code button to see the plot!

#3. Click the Submit your Answer button when you are satisfied with the result

```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki


test_function("plot",
              not_called_msg = "You didn't call `plot()` correctly. Remember: x = earnings and y = s_rating")

test_error()

success_msg("Good work!")

```


---

## The Caret Package
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: a11fe162ef
```

R packages can be very useful because they contain functions that aren't included in the base R code. Importing packages into your R session will allow you to access the functions in those packages. We are going to import a package for machine learning called "caret".

It is common practice in machine learning to partition a dataset for analysis into Training and Test sets in order to test the accuracy of your model before feeding in new data. To do this, we will use a function called `createDataPartition()` from the caret package.

To learn more about this function, type `?caret::createDataPartition` in the console or the script.R window. Since it's already typed in for you, click Run Code to see more information about this function from r-documentation.org

When you are finished reading, click Submit Answer.



`@possible_answers`
?caret::createDataPartition is already typed for you in the code. Click Run Code to see the results.

`@hint`

`@pre_exercise_code`
```{r}
library(caret)

```

`@sample_code`
```{r}
# Click the Run Code button to see the documentation open in a new tab. Return to this tab and click Submit Answer when you're ready to proceed!

?caret::createDataPartition
```

`@solution`
```{r}
?caret::createDataPartition
```

`@sct`
```{r}

```
---

## Create a Training Set
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: fccca9bca2
```
Both training and test data sets come from the original data. A training set is usually 60 - 70% of the entire dataset while the test set is about 30 - 40%.

The createDataPartition() function can be used to split the data into training and test sets. This function is used like so:

Suppose you want to predict what age group is more likely to purchase a certain product and `age_group` is a variable in your dataset, `myData`. Since `age_group` is what you want to predict, it is your dependent variable, or target variable.

Create a data partition where `y = age_group`. In this formula, we type the `age_group` variable as `myData$age_group`, using a `$` between the name of the data set and the variable name we want.

```{r}
inTrain <- createDataPartition(y= myData$age_group, p=0.7, list=FALSE)

training <- myData[inTrain, ]

test <- myData[-inTrain, ]

[inTrain, ] means included in the inTrain data
[-intrain, ] means not included in the inTrain data

p is set to 0.7 because we need 70% of the whole data

list = FALSE because we do not want the function to return inTrain as a list.
```

`@possible_answers`

- Use createDataPartition() function in R to partition your dataset. This example may help you: `createDataPartition(y= myData$age_group, p=0.7, list=FALSE)`
- Your training set should be 60% of the entire dataset (p=0.6)
- Print out the training and test sets  
- Check the dimension of both datasets to know more about the data

`@hint`

- Make p=0.6 and set list=FALSE
- Use the `dim()` function on training and test set for the fourth instruction

`@pre_exercise_code`

```{r}

# Loading the required package

library(caret)

# Create the dataset

earnings <- c(120, 100, 700, 200, 60, 20, 200, 130, 150, 160, 170, 180, 190, 210, 220, 400, 550, 670, 695, 300)

s_rating<- c(50, 60, 80, 75, 50, 70, 75, 60, 50, 65, 70, 71,80, 82, 85, 80, 88, 90, 90, 60)

emp_data  <- data.frame(earnings, s_rating)

```

`@sample_code`
```{r}

# 1. Create the inTrain dataset. Set y = to emp_data$s_rating, p= 0.6, and list=FALSE

inTrain <- createDataPartition(y= , p=  , list= )

# 2. Partition the inTrain dataset into training and test sets. Follow the example in the block on the left side of the page and fill in the brackets with the correct code.

training <- emp_data[ ]

test <- emp_data[ ]

# 3. Type the variable names `training`  and `test` to see the contents of those variables when you run the code.


# 4. Show the dimensions of the `training` and `test` sets using the dim() function. Type dim(training) and dim(test)


# 5. Run the code before you submit your answer!


# 6. Submit your answer to proceeed

```

`@solution`
```{r}

# 1. Create the inTrain dataset. Set y = to emp_data$s_rating, p= 0.6, and list=FALSE

inTrain <- createDataPartition(y=emp_data$s_rating , p=0.6 , list=FALSE)

# 2. Partition the inTrain dataset into training and test sets. Follow the example in the block on the left side of the page and fill in the brackets with the correct code.
training <- emp_data[inTrain, ]
test <- emp_data[-inTrain, ]

# 3. Type the variable names `training`  and `test` to see the contents of those variables.
training
test


# 4. Show the dimensions of the `training` and `test` sets using the dim() function. Type dim(training) and dim(test)
dim(training)
dim(test)
# 5. Run the code before you submit your answer!

# 6. Submit your answer to proceeed!

```

`@sct`
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

success_msg("Fantastic!")
```



```yaml
type: PureMultipleChoiceExercise
lang: r
xp: 50
skills: 1
key: fd5f3c1098
```
## Linear Regression

The `lm()` function in R is an implementation of the Linear Regression algorithm. Linear regression is a method for modeling the relationship between two variables. The goal is to find an equation that fits the data.

You will create a linear model called `reg_model` by plugging in the training set into the `lm()` function.

The equation is of the form:

`y = a + bx + ei`

`y` is what we want to predict and `x` includes all the predictors required to form the model above.

`a` and `b` are **coefficients** determined by the `lm()` function.

`ei` stands for errors as a result of the factors we did not consider.  


Given the meaning of `ei`, what type of model is best?


`@possible_answers`
-  A model that minimizes `ei` the most.
-  A model that maximizes `ei` the most.
-  Neither model

`@hint`
Remember that `ei` stands for errors. Is it better to maximize or minimize errors?

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}

msg_bad <- "Sorry, try again"
msg_success <- "Yes!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad, msg_bad))

```




## Create Your Linear Model
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 1d4011a3d1
```
A regression model is easy to implement but it often produces low performance models. This method is useful when the variable involved can be modeled in a linear way, for example, so show that an increase in age leads to increase in weight.

`lm()` function is used like this:

`reg_model <- lm(target ~ predictor, data=dataset)`

`predictor` = the variable that helps us predict an outcome or output (independent variable)
`target` = the variable we are trying to model or predict (independent variable)
`dataset` = the name of the dataset you want to use


`@possible_answers`
- Create a linear model called `reg_model` on the training dataset
- Plot the `training` set with earnings as the predictor (x) variable and s_rating as the target (y)
- Draw a regression line on the plot above that represents the model reg_model using abline()


`@hint`
- Type `?lm` to learn how to use the lm() function
- Use `abline()` function to fit a line to the plot. Put the model name inside the parentheses.
- type ?coef to know how to use the coef() function

`@pre_exercise_code`
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code

load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_4925/datasets/ml.RData"))

# Clean up the environment

```

`@sample_code`
```{r}

# 1. Create a linear model called reg_model. Use earnings as your predictor variable (x). Use s_rating as your target variable (y). Use training as your data.

reg_model <- lm(  ~ , data=  )


# 2. Examine a summary of your model. Type summary(reg_model)

summary(reg_model)

# 3. Plot the training set x and y variables in a scatter plot.

plot(x=earnings, y=s_rating, col = s_rating, main="Regression Modeling")


# 4. Draw a regression line that represents the model reg_model. Type abline(reg_model) in the line below this one.

```
`@solution`
```{r}

# 1. Create a linear model called reg_model. Use earnings as your predictor variable (x). Use s_rating as your target variable (y). Use training as your data.

reg_model <- lm(s_rating ~ earnings, data=training)

# 2. Examine a summary of your model. Type summary(reg_model)

summary(reg_model)

# 3. Plot the training set x and y variables in a scatter plot.

plot(x=earnings, y=s_rating, col = s_rating, main="Regression Modeling")

#plot(x=training$earnings, y=training$s_rating, col = training$s_rating, main="Regression Modeling")

# 4. Draw a regression line that represents the model reg_model. Type abline(reg_model) in the line below this one.

abline(reg_model)


```

`@sct`

```{r}

# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_object("reg_model")
test_function("summary", not_called_msg = "Don't forget to call `summary()`")

test_function("plot", not_called_msg = "Don't forget to call `plot()`")

test_function("abline", not_called_msg = "You didn't call `abline()`")

test_error()

success_msg("You are doing really well!")

```


## Coefficients in a Linear Model

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 84a2fa109d
```

Remember that the equation for a linear model is `y = a + bx + ei`

We can get the coefficients `a` and `b` from `reg_model` using the coef() function:

```{r}
a <- coef(reg_model)[1]
b <- coef(reg_model)[2]
```


`@possible_answers`
Find coefficients a and b using the example provided above. What are the values of the coefficients?

`@hint`
Follow the coef(reg_model)[1] syntax in your answers.

`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_4925/datasets/ml.RData"))
reg_model <- lm(s_rating ~ earnings, data=training)
```

`@sample_code`
```{r}
# 1. Create a variable 'a' for coefficient 'a'

a <- coef(  )[ ]

# 2. Print out 'a' by typing 'a' on the next line
a

# 3. Create a variable 'b' for coefficient 'b'

b <- coef( )[ ]

# 4. Print out 'b' by typing 'b' on the next line.
b

```

`@solution`
```{r}
# 1. Create a variable 'a' for coefficient 'a'

a <- coef(reg_model)[1]

# 2. Print out 'a' by typing 'a' on the next line
a

# 3. Create a variable 'b' for coefficient 'b'

b <- coef(reg_model)[2]

# 4. Print out 'b' by typing 'b' on the next line.
b

```

`@sct`
```{r}
test_object("a")

test_object("b")

test_error()

success_msg("Super!")

```

## Test Your Happiness Prediction Model
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 6ae37a587e
```

Here, you will create a function called `predict_happiness` to test your model.

You are to get coefficients `a` and `b` from `reg_model` and predict satisfaction when employee is paid `$200`, `$400`, and `$1200` using `predict_hapiness` function.

```
predict_happiness <- function(x){
  a <- coef(reg_model)[1]
  b <- coef(reg_model)[2]
  Result <- a + (b * x)
  percent <- "%"
  cat(sprintf("The employee should be %s%s
        satisfied", Result, percent))
  }
```

`@possible_answers`
- Complete the predict_happiness function
- Follow instructions listed for each step.

`@hint`
- Get coefficents `a` and `b` from  `reg_model` using the `coef()` function as in previous exercises.
- Use the data.frame() function to create a table with two variables pred_rating and test$s_rating.

`@pre_exercise_code`
```{r}
# load(url(""))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/ml1.RData"))
reg_model <- lm(s_rating ~ earnings, data=training)
```

`@sample_code`
```{r}

# 1. Create a function called predict_happiness that will take in any daily salary and output a happiness satisfaction rating. Fill in the brackets to get the correct coefficients a and b from the model.

predict_happiness <- function(x){

  a = coef(reg_model)[ ]
  b = coef(reg_model)[ ]
  Result <- a + (b * x)
  percent<- "%"
  cat(sprintf("The employee should be %s%s satisfied", Result, percent))
}

# 2. Predict satisfaction when employee is paid $200/day.

predict_happiness(200)

# 3. Now predict the satisfaction rating when an employee is paid $400/day. Use the predict_happiness() function.

# 4. How about $1200? Will the employee be extremely happy? Use the predict_happiness() function to see a prediction.

```

`@solution`
```{r}

# 1. Create a function called predict_happiness that will take in any daily salary and output a happiness satisfaction rating.

predict_happiness <- function(x){

  a = coef(reg_model)[1]
  b = coef(reg_model)[2]
  Result<- a + (b * x)
  percent<- "%"
  cat(sprintf("The employee should be %s%s satisfied", Result, percent))
}

# 2. Predict satisfaction when employee is paid $200/day

predict_happiness(200)

# 3. Now predict the satisfaction rating when an employee is paid $400/day
predict_happiness(400)

# 4. How about $1200? Will the employee be extremely happy? Use the predict_happiness() function to see a prediction.
predict_happiness(1200)
```

`@sct`
```{r}

test_object("predict_happiness")

test_error()

success_msg("Perfect!")

```



## Using the predict() Function as an Alternative Approach

```yaml
type: NormalExercise
lang: r xp: 100 skills: 1 key: 4f8a44fee2
```

`@possible_answers`
Instead of using `predict_happiness` function, you can also use the built-in `predict` function provided by caret package. The predict function takes in the model and the test dataset like this:

`predict(reg_model, test)`

Put all your predicted values in a variable called `pred_rating` as in `pred_rating <- predicted(reg_model, test)`

Compare `pred_rating` with the `s_rating` column in the test data. What do you observe? Are the predicted ratings close to the actual?


`@hint`

`@pre_exercise_code`
```{r}
# load(url(""))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/ml1.RData"))
reg_model <- lm(s_rating ~ earnings, data=training)

```

`@sample_code`
```{r}

# 1. Create a variable called pred_rating, which is the predicted satisfaction ratings for test set. Put reg_model in parentheses before test.

pred_rating <- predict(   , test)

# 2. Compare test set s_rating with predicted s_rating for the test set. A data frame has been created for you.

data.frame(pred_rating, test$s_rating)

# 3. Click run code to see the output

# 4. What do you observe? Are the predicted ratings close to the actual? No need to type anything here.

```

`@solution`
```{r}
# 1. Create a variable called pred_rating, which is the predicted satisfaction ratings for test set. Put reg_model in parentheses before test.

pred_rating <- predict(reg_model, test)

# 2. Compare test set s_rating with predicted s_rating for the test set. A data frame has been created for you.

data.frame(pred_rating, test$s_rating)

# 3. Click run code to see the output

# 4. What do you observe? Are the predicted ratings close to the actual? No need to type anything here.

```

`@sct`
```{r}
test_object("pred_rating")

test_error()

success_msg("Great job!")


```
```yaml type: NormalExercise lang: r xp: 100 skills: 1 key: 75c935d749
## Check the Accuracy of Your Model

There a number of ways to evaluate your model. For this exercise, you will use the root-mean-square error (RMSE).
RMSE is gotten by calculating mean squared errors. This is simply a measures of deviation of predicted points from the original value.


The formula is:

  rmse  = ![](http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/rmse.png)


Where:

 * f = predicted values
 * o = true values
The bar above the squared differences means find the *mean* of the squared difference.


`@possible_answers`

- You can find the rmse of the test dataset by running the code below in the console:

    `sqrt(sum((pred_rating - test$s_rating)^2) / n)`

`@hint`


`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/ml2.RData"))
```

`@sample_code`
```{r}
# 1. Check the accuracy of your model by calculating the RMSE for pred_rating and test$s_rating

n = 20 # n is the number of observations predicted

check_accuracy <- sqrt(sum(( - )^2) / n)

# 2. Print 'check_accuracy' to see your results

```

`@solution`
```{r}

# 1. Check the accuracy of your model by calculating the RMSE for pred_rating and test$s_rating

n = 20 # n is the number of observations predicted

check_accuracy <- sqrt(sum((pred_rating - test$s_rating)^2)/n)


# 2. Print 'check_accuracy' to see your results
check_accuracy

```

`@sct`
```{r}
test_object("check_accuracy")

test_error()

success_msg("Great! At this point, you can either accept your model or go back and improve it.")

```



## Decision Tree Algorithm
```yaml
type: PureMultipleChoiceExercise
lang: r
xp: 100
skills: 1
key: e4a7c1750f
```

Decision trees are a type of `supervised learning` algorithm and are mostly used in `classification` problems. **The decision tree algorithm involves splitting the population or sample into two or more sub-populations based on the most significant input variables.**

Here is an example:

Suppose we have a sample of `30 students` with two input variables `Gender` and `Height` (5 to 6 ft). 15 out of these 30 play `Basketball` in their free time.

We want to create a model to predict who will play basketball during their free time. Basically, we want to separate students who play basketball in their free time based on highly significant input variables among the variables in the dataset. Significant input variables are called `predictors`.

A decision tree is useful here in that it will segregate the students based on all values of the two variables. The variable that creates the best similar sets of students (i.e. sets which are dissimilar to each other).

![](http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/dtree.png)

In the figure above, you can see that variable `Gender` is able to identify best sub-population sets compared to the variable `Height`.

The `Random Forest` algorithm is a variant of decision tree algorithm. The algorithm involves constructing a multitude of decision trees at training time and outputting a result that is the `mode class` or `mean prediction` of the individual trees. This makes random forest `very accurate` and popular among data people.


### `CLASS ACTIVITY:`
Which of the following types of questions might you try to answer with a Random Forests model?

`@possible_answers`
- If you make more money, will you be happier?
- What is a new customer to a web store likely to purchase?
- Is it true that what goes up must come down?

`@hint`
- Random forests are useful for finding relationships that can't be predicted linearly.

`@pre_exercise_code`
```{r}
```
`@sct`
```{r}

# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "Sorry. Try again!"
msg_success <- "Great!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad))

```


## Getting to Know the Wage Dataset
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 47b0bc653f
```
The first step in Machine Learning is getting your data. This step involves finding the raw data in whatever format they are. They may be structured, unstructured, semi structured, whether flat files, tables, JSON format or in a database, video, audio, text etc.

Let’s see an example using the Wage dataset provided by the `ISLR` package.

`@possible_answers`
- Know more about the Wage dataset. Use str() and dim() on the Wage dataset. Can you interpret the results?
- Call head() and tail() on your dataset to reveal the first and last 6 observations.
- Finally, call the summary() function to generate a summary of the dataset. What does the printout tell you?

`@hint`
- The str() function gives you an overview of the different variables of the data.
- The dim() function tells you the number of observations and variables respectively.
- The summary() function returns several measures for each variable. Such as the maximum observed value, the mean and many more!

`@pre_exercise_code`
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code

Wage <- read.csv('http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/wage.csv', stringsAsFactors = FALSE)

```

`@sample_code`
```{r}
# 1. Take a look at the Wage dataset variables using the str() function. Put Wage inside of str().


# 2. Learn more about the Wage dataset. Type dim(Wage) to see more.


# 3. Examine the first few observations with the head() function. Type head(Wage) below.


# 4. Get a summary of the dataset by typing summary(Wage)



```

`@solution`
```{r}

# 1. Take a look at the Wage dataset by printing it out.

str(Wage)

# 2. Learn more about the Wage dataset. Type dim(Wage) to see more.

dim(Wage)

# 3. Examine the first few observations with the head() function. Type head(Wage) below.

head(Wage)

# 4. Get a summary of the dataset by typing summary(Wage)

summary(Wage)

```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str",
              not_called_msg = "You didn't call `str()`")

test_function("dim",
              not_called_msg = "You didn't call `dim()`")

test_function("head",
              not_called_msg = "You didn't call `head()`")

test_function("summary",
              not_called_msg = "You didn't call `summary()`")

test_error()

success_msg("Good work!")
```


---
## Data Preprocessing

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 4b8748fe97
```

Data preprocessing involves transforming data into a basic form that makes it easy to work with. One characteristic of a tidy dataset is a dataset having **one observation per row and one variable per column**. The Wage dataset is an example of a tidy dataset.

Activities done in this step also includes detecting the presence of missing (NA) values, noise and outliers, or duplicate data.
```
1: Check for missing values
        sum(is.na(Wage))

2: Do some exploratory data analysis

        qplot(age, wage, data=Wage, color = race)

3: We do not need the variable “logwage” for our analysis, so we remove it.

        Wage<- subset(Wage, select=- c(logwage))

```

As we saw from the example on satisfaction ratings, predicting continuous variables gives results that are not exactly precise. So for this example, we will present our results in terms of categories.

We will divide the `wage` column into 12 categories and add another column called `wage_range` to the Wage dataset. Each observed wage will therefore fall under one of these 12 categories.

```{r}
        wage_range <- cut(Wage$wage, b = 12)

        Wage$wage_range <- wage_range
```

`@possible_answers`
- Plot age against wage but this time make the color based on education.
- Remove other variables not necessary for this analysis such as health, health_ins, region, race, year, sex, and maritl.
- Call head() on Wage to check that our new column has been added. Observe that each wage falls within the corresponding wage_range.


`@hint`
- Use subset() function to remove these variables as in  `Wage<- subset(Wage, select=- c(logwage, health...`

`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/ml3.RData"))

```

`@sample_code`
```{r}
library(ggplot2)

# 1. Check for missing values in the Wage dataset. Use the sum(is.na(()) function.
sum(is.na(   ))

# 2. Do some exploratory data visualization using the qplot function) Set x=age, y=wage, data=Wage, color=education)

qplot(x= , y= , data= , color =  )

# 3. Remove the following unnecessary variables using the subset() function: health, health_ins, region, race, year, sex, maritl. Put the variables inside the c( )

Wage <- subset(Wage, select=- c(  ))

# 4. Add wage_range variable to the Wage datasets. Put Wage$wage inside of cut() and b=12.
 wage_range <- cut(  ,  )

 Wage$wage_range <- wage_range

#5. Call head() on Wage to check that our new column has been added. Observe that each wage falls within the corresponding wage_range.

```

`@solution`
```{r}
library(ggplot2)

# 1. Check for missing values in the Wage dataset. Use the sum(is.na(()) function.
sum(is.na(Wage))

# 2. Do some exploratory data visualization using the qplot function) Set x=age, y=wage, data=Wage, color=education)

qplot(age, wage, data=Wage, color = education)

# 3. Remove the following unnecessary variables using the subset() function: health, health_ins, region, race, year, sex, maritl. Put the variables inside the c( )

Wage<- subset(Wage, select=- c(health, health_ins, region, race, year, sex, maritl))

# 4. Add wage_range variable to the Wage datasets. Put Wage$wage inside of cut() and b=12.

wage_range <- cut(Wage$wage, b = 12)
Wage$wage_range <- wage_range

# 5. Call head() on Wage to check that our new column has been added. Observe that each wage falls within the corresponding wage_range.
head(Wage)
```

`@sct`
```{r}

test_function("qplot",
              not_called_msg = "You need to call `qplot()`")
test_object("Wage")

test_object("wage_range")

test_error()

success_msg("You did it!")
```

---
## Forest of Trees
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 2099ae7c71
```
In this step, you will:

* Partition the data into `training` and `test` sets.
* Create a random forest model called `rf_model` to predict `wage` based on three input variables - `age`, `education` and `job class`.The function randomForest() is used to create a random forest model like this:

    `rf_model <- randomForest(wage_range ~ age + jobclass + education, data = training, importance = TRUE, ntree=500)`


`@possible_answers`
- Use createDataPartition() function to partition your dataset. Your training set should be 70% of the entire dataset
- Print out the first few observations of training and test sets and check the dimension of both datasets to know more about the data
- Now plot the training dataset with age on the x-axis, wage on the y-axis and make the colour based on education. What do you notice?
- Create you own `rf_model`, but this time grow 800 trees. Print `rf_model` to console.


print(rf_model)
`@hint`
- type ?createDataPartition to know how to use the createDataPartition() function
- Make p=0.7 and set list=FALSE
- To print a variable to the console, simply type the name of the variable on a new line.
- Use `qplot()` for the third instruction. Just as you did in the previous exercise.
- Do you notice that the plot created from the training set is similar to the plot done on the whole Wage dataset? This is because the createDataPartition function splits the data evenly into training and test sets.
- For the last instruction, set `ntree` to 800. Print rf_model to console.
- Use head() function for the third instruction. To print a variable to the console, simply type the name of the variable on a new line.

`@pre_exercise_code`
```{r}
library(caret)
library(randomForest)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/ml4.RData"))
wage_range <- Wage$wage_range

```

`@sample_code`
```{r}

# 1. Create a dataset partition called inTrain. Set y = to wage_range, p=0.7 and list=FALSE.

inTrain <- createDataPartition(y= , p= , list=FALSE)

# 2. Divide inTrain into training and test datasets. Example: Wage[inTrain, ] versus Wage[-inTrain, ]

training <- Wage[  ]

test <- Wage[ ]

# 3. Print out training and test sets and show the dimensions of each set
# Hint: use the head() and dim() functions!


# 4. Make a scatter plot of training set variables x=age and y=wage, with color=education.
qplot(x= , y= wage, data=training, color=education)


# 5. Now create your randomForest model. Your target variable (y) is wage_range. Your predictor variable (x) is age. Jobclass and education have been added to the model as well. Set data = training and ntree=800.
rf_model <- randomForest(x=    ~ y=   + jobclass + education, data =  , importance = TRUE, ntree=  )


# Print `rf_model` to the console
rf_model

```

`@solution`
```{r}

# 1. Create a dataset partition called inTrain. Set y = to wage_range, p=0.7 and list=FALSE.

inTrain <- createDataPartition(y=wage_range , p=0.7, list=FALSE)

# 2. Divide inTrain into training and test datasets. Example: Wage[inTrain, ] versus Wage[-inTrain, ]

training <- Wage[inTrain, ]

test <- Wage[-inTrain, ]

# 3. Print out first few observations of the training and test sets and show the dimensions of each set
# Hint: use the head() and dim() functions!

head(training)

head(test)

dim(training)

dim(test)

# 4. Make a scatter plot of training set variables age and wage, with color = to education.
qplot(age, wage, data=training, color=education)

#5. Now create your randomForest model. Your target variable (y) is wage_range. Your predictor variable (x) is age. Jobclass and education have been added to the model as well. Set data = training and ntree=800.

rf_model <- randomForest(wage_range ~ age + jobclass + education, data = training, importance = TRUE, ntree=800)

# 6. Print `rf_model` to the console.
rf_model

```

`@sct`
```{r}

test_object("training")
test_object("test")


test_function("dim",
              not_called_msg = "You need to call `dim()` twice for `training` and `test`")

test_function("head", not_called_msg = "You need to call `head()` twice for `training` and `test`")

test_function("randomForest",
              not_called_msg = "You need to call `randomForest()`")

test_error()

success_msg("Wow! You are amazing!")

```
---

## Check the Accuracy of your Random Forests Model
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 2099ae7c71
```

Test your `rf_model` by using the predict function like this:

`pred_wage <- predict(model_name, test_data)`

To check accuracy of your model, calculate RMSE using postResample() function like this:

`postResample(actual_wage, pred_wage)`

`@possible_answers`
- Now, test your `rf_model` by using the `predict()` function. Store the predicted wages in a variable called `pred_wage`.
- Compare predicted wage to original wage of test dataset by creating a table called `compare_result`with data.frame() function having two columns testing$wage and pred_wage
- Print out the first few observation of `compare_result`


`@hint`
- Use head() for the third instruction.

`@pre_exercise_code`
```{r}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/ml5.RData"))
library(randomForest)
library(ggplot2)
library(caret)

rf_model <- randomForest(wage_range ~ age + jobclass + education, data = training, importance = TRUE, ntree=800)
```

`@sample_code`
```{r}

# 1. Test your `rf_model` by using the predict() function. Ex: predict(model_name, test_data)`

pred_wage_range <-

# 2. Compare predicted wage to original wage of test dataset. This creates a data set with one column having the actual data, and one column having the predicted data.

compare_result <- data.frame(test$wage_range, pred_wage_range)

# 3. Print out the first few observation of compare_result using the head() function


# 4. Check the accuracy of your model by calculating the RMSE. Use the postResample() function!
#Example: postResample(actual_wage, pred_wage_range)

postResample(test$wage_range, )

```

`@solution`
```{r}

# 1. Test your `rf_model` by using the predict() function for rf_model and your test data (test). Ex: predict(model_name, test)`

pred_wage_range <- predict(rf_model, test)

# 2. Compare predicted wage to original wage of test dataset. This creates a data set with one column having the actual data, and one column having the predicted data.

compare_result <- data.frame(test$wage_range, pred_wage_range)

# 3. Print out the first few observation of compare_result using the head() function

head(compare_result)

# 4. Check the accuracy of your model by calculating the RMSE. Use the postResample() function!
#Example: postResample(actual_wage, pred_wage_range)

postResample(test$wage_range, pred_wage_range)


```

`@sct`
```{r}

test_function("predict",
              not_called_msg = "You need to call `predict()`")

test_function("data.frame",
              not_called_msg = "You need to call `data.frame()`")

test_function("head",
              not_called_msg = "You need to call the `head() function`")

test_function("postResample",
              not_called_msg = "You need to call `postResample()`")

test_error()

success_msg("Good work! At this point, you can accept your model and present your work or seek to improve your model.")

```
---

## Improving Your Model
```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 61976945d8
```

Your model depends on the quality of your dataset and the type of Machine Learning algorithm used. Therefore, to improve the accuracy of your model, you should:

* Check what attributes affect our model the most and what variables to leave out in future analysis
* Find out what other attributes may affect wages and use these factors as predictors in future analysis
* Tweak the algorithm (e.g. change the ntree value)
* Use a different machine learning algorithm

If any of these reduces the RMSE significantly, you have succeeded in improving your model!


`@possible_answers`
- Call importance() function on `rf_model` to check how the attributes used as predictors affect our model
- Call varImpPlot() function on `rf_model` to visually check variable importance
- What do you notice?


### `Note that:`

`Mean Decrease Accuracy (%IncMSE)` - This shows how much our model accuracy decreases if we leave out that variable.

`Mean Decrease Gini (IncNodePurity)` - This is a measure of variable importance based on the Gini impurity index used for the calculating the splits in trees.

The higher the value of mean decrease accuracy or mean decrease gini score, the higher the importance of the variable to our model.

We can see that the predictor `education` plays an important role in the accuracy of our model. We might include other variables from the wage dataset into our analyses and compare our model’s RMSE when this variables are present versus when absent.

This brings us to the end of this course. Keep finding ways to create better Machine Learning models.

### `Good luck in your future endeavors!`

`@hint`

- Type importance(rf_model) and varImpPlot(rf_model)

`@pre_exercise_code`
```{r}
library(caret)
library(randomForest)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_5412/datasets/ml5.RData"))
rf_model <- randomForest(wage_range ~ age + jobclass + education, data = training, importance = TRUE, ntree=800)

```

`@sample_code`
```{r}
# 1. Check what attributes affect our model the most. Use the `importance()` function on `rf_model`.

importance( )

# 2. Use the `varImpPlot()` function on `rf_model`

varImpPlot( )
```

`@solution`
```{r}

# 1. Check what attributes affect our model the most. Use the `importance()` function on `rf_model`.

importance(rf_model)

# 2. Use the `varImpPlot()` function on `rf_model`

varImpPlot(rf_model)
```

`@sct`
```{r}

test_function("importance",
              not_called_msg = "Try calling `importance()`")

test_function("varImpPlot",
              not_called_msg = "Try calling `varImpPlot()`")



```
