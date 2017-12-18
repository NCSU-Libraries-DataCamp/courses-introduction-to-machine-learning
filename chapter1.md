---
title       : "Machine Learning: Opening up the Black Box"
description : This chapter provides a general introduction to machine learning.
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf


--- type:PlainMultipleChoiceExercise lang:r xp:50 skills:1 key:53d9ea348c
## The Buzzword

According to Wikipedia, Arthur Samuel in 1959 defined Machine Learning as the subfield of computer science that gives computers the ability to learn without being explicitly programmed. This means that machines will be given the ability to make inferences and observation by learning from data. In other words, **machine learning is the science of teaching the machine to identify trends and patterns in data that cannot easily be detected by humans.** 

### `CLASS ACTIVITY:`
**QUESTION: From the above definition, which of the following is not a Machine Learning Task?**

*** =instructions
- Self driving cars
- A program that prints the next 20 leap years
- A program that categorizes emails into spam and non-spam
- Predicting galaxies

*** =hint
Take a look at the options. Which task requires explicitly programming the computer?

*** =pre_exercise_code
```{r}
# None

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! Even I can calculate the next 50 leap years and I'm only human."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```


--- type:PlainMultipleChoiceExercise lang:r xp:50 skills:1 key:40173c5d8e
## Machine Learning Process

A human can learn the voices of 10 (or perhaps 100) co-workers and be able to identify them without looking. A machine, however, can learn the voices of over 10,000 people and be able to predict whose voice it is. How? Machine learning of course.

The steps involved in Machine Learning include the following:

- Getting data
- Preprocessing the data (Clean, Prepare, Manipulate Data & Exploratory Data Analysis (may include visualization)
- Training the Model
- Testing the Model
- Post-Processing the data (Visualizing, Evaluating, Improving the Model & Presenting)

The first two steps are typical for any analysis involving data, but **creating a model is a critical part of machine learning.**

### `CLASS ACTIVITY:`

If machines can learn 10,000 voices and humans can only learn between 10 and 100, does that make computers smarter than humans?

*** =instructions
-Yes
-No 
-Don't know

*** =hint

*** =pre_exercise_code
```{r}
# None 
```

*** =sct
```{r}

msg_bad <- "Just because computers can learn faster than humans doesn't make them smarter. We still have some advantages!"
msg_success <- "We humans are still pretty smart."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad))

```




--- type:PlainMultipleChoiceExercise lang:r xp:100 skills:1 key:06d44465f4

## The Model: the Secret Weapon in Machine Learning

A model is an artifact or a formula created by the process of learning from previous data. When you plug in historical data into a machine learning algorithm, you get a model.

In the above example, the machine uses a model that takes in an input (a person’s voice), does some processing and predicts the name of the person as the output. 

In chapter 3, you learn how to test, evaluate, and improve your model.


### `CLASS ACTIVITY:`

A good machine learning model depends on which of the following? 

*** =instructions
- Type of the data and software or statistical tool used for analysis
- Type of machine learning algorithm used and software or statistical tool used for analysis
- The quality of the dataset and type of machine learning algorithm used
*** =hint
Clean historical data + Good Machine Learning algorithm = Great Model!
*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly!"
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_success))
```
