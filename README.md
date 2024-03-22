# Recipes-Analysis-Mexican-Style-

This is a project analysis from DSC 80 at UCSD

## Introduction

  Have you ever been in a situation where your friends were pretentious enough to claim that a certain ethnic food was superior? Have you or a loved one ever been subjected to the situation when deciding where to go out and eat and one person chooses an ethnic food that you are in fact not in the mood to eat. WELL, you’ve come to the right place. With new foods constantly being made it might be hard and stressful to decide what to eat, so this project aims to help you make those tough decisions depending on the ethnicity of the cuisine. This brings me to the current question, How does the ethnicity of the food affect the rating of the recipe? However, for now, we will only look at a small lens of this question. Specifically we will be asking if: **Mexican cuisine holds a higher rating on average compared to food not labeled as Mexican cuisine?**

  Before getting our hands dirty (not from the tacos), I will be using a data set from food.com that contains recipes and reviews dating from 2008 onwards. The recipes data frame contains 83782 rows which represents a unique recipe for every row. This data set also contains 12 columns total however the relevant ones that I mainly emphasize are the `tags` (tags that the recipe is labeled as), `nutrition` (nutritional value of the recipe which contains calories, total fat, sugar, sodium, protein, saturated fat, carbohydrates), `n_ingredients` (the number of ingredients), and `n_steps` (number of steps) columns. I also used another data frame which contained a column called `review` for reviews some people had left on certain recipes. This review data frame contained 731927 rows which did not contain unique recipes but unique reviews that people had left along with their rating of the food in a column called `rating`. As you will see in my analysis I ended up utilizing the rating column along with the review column. 

## Data Cleaning and Exploratory Data Analysis:

In terms of cleaning the data, I approached cleaning the data first by noticing the types of each value in the two dataframes. From this observation, I noticed that the nutrition column was consider a string object that looked like a list containing `calories(#)`, `total fat(PDV)`, `sugar(PDV)`, `sodium(PDV)`, `protein(PDV)`, `saturated fat(PDV)`, and `carbohydrates(PDV)` specifically in this order. Therefore, I had turned all the values in that column into an actual list and then appended each column into their own respective columns with their proper labels.

Next, I wanted to match the recipes with their respective reviews. Thus, I had merged the recipes and reviews data sets together.

After merging, I noticed that there was a significant amount of NaNs in the `rating` column. To further clean the data I had then filled all the NaNs in the rating column with 0. I had specifically changed them to 0 because they would still indicate a NaN value. For instance, in terms of ratings it is not possible to give a rating of 0, the lowest rating that one can get is a 1.

Finally, I added two new columns to the final data frame:
The first new column being added is called `avg_rating` which is the average rating from all the reviews for a specific recipe. 
The second column being added is called `is_mexican` and is derived from the ‘tags’ column. In this analysis, recipes tagged with ‘mexican’ are then considered a mexican dish. As a results, the True values indicates that a recipe has a ‘mexican’ tag and those that have False values did not tag this dish as ‘mexican’.
After cleaning the data this is what the final data frame looks like:

| name                                 |   minutes | tags                                                                                                                                                                                                                        |   n_steps |   n_ingredients |   calorie(#) |   sugar(PVD) |   rating | review                                                                                                                                                                                                                                                                                                                                           |   avg_rating | is_mexican   |
|:-------------------------------------|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|----------------:|-------------:|-------------:|---------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------:|:-------------|
| 1 brownies in the world    best ever |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] |        10 |               9 |        138.4 |           50 |        4 | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.                                                                                   |            4 | False        |
| 1 in canada chocolate chip cookies   |        45 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               |        12 |              11 |        595.1 |          211 |        5 | Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, & I made the whole batch & used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe! |            5 | False        |
| 412 broccoli casserole               |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 |               9 |        194.8 |            6 |        5 | This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!                                                                                                                                  |            5 | False        |
|                                      |           |                                                                                                                                                                                                                             |           |                 |              |              |          | The photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.                                                                                                                                                                                                        |              |              |
|                                      |           |                                                                                                                                                                                                                             |           |                 |              |              |          | Thanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)                                                                                                                                                                                                                          |              |              |
| 412 broccoli casserole               |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 |               9 |        194.8 |            6 |        5 | I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.                                                                                                                                                                               |            5 | False        |
| 412 broccoli casserole               |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 |               9 |        194.8 |            6 |        5 | Loved this.  Be sure to completely thaw the broccoli.  I didn&#039;t and it didn&#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.                                                                                                                                                     |            5 | False        |

### Univariate

<iframe
  src="assets/Number_of_Steps_Recipes.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
Looking at this univariate plot, it displays the amount of recipes that utilize a certain amount of steps. Therefore, we can see a lot of the recipes consist of using around 7 steps total.  

### Bivariate

<iframe
  src="assets/Avg_R_Num_Ing_M.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/Avg_R_Num_Ing_A.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
For context, the top scatter plot contains only the recipes that are tagged as Mexican while the bottom includes all the points from the entire data set. Each scatter plot, indicates the average rating based on its respective number of ingredients. Furthermore, when looking at the top plot which indicates those recipes that are tagged as Mexican you can see that as the recipes recieve a high averge rating the more ingredients they use. Looking at the two bivariate graphs overall, one can see that they both follow very a similar distribution where the higher the rating the more ingredients they have. 

### Interesting Aggregates

As my interesting aggregates, I had wanted to see what the in means in calorie per amount of steps the recipes would be while looking at it in the scope of whether the recipes were tagged as being Mexican.

| n_steps | False  | True   |
|---------|--------|--------|
| 1       | 267.24 | 182.10 |
| 2       | 301.08 | 249.48 |
| 3       | 288.73 | 200.46 |
| 4       | 325.55 | 304.04 |
| 5       | 342.13 | 335.52 |

For instance, the very first cell in this pivot table is telling us that that for the recipes that have one step and not tagged as Mexican have an average calorie count of 267.24. As overall, generally the calorie count in the foods that are not tagged as Mexican have a higher average than those that are tagged as being Mexican. Additionally, as we increase the number of steps the calorie mean typically increases.

## Assessment of Missingness:

### NMAR Analysis

In terms of NMAR, we can see that there are missing values (NaN values) in the `review` column. We can likely conclude that there are missing values here because while the people were rating the food they might have not felt very strongly about a particular recipe that they tried out. So because these people did not feel a strong enough emotion to create a review they might have felt like they had nothing to say and thus they left no review.

### Missingness Dependency

Now we can look at the missingness of some of the data that might depend on other columns in the dataset. To help explain the missingness of a column I used permutation tests on specific columns to potentially help explain the missingness seen in the rating column.

1. Rating and Sugar(PDV) (MAR)

First I had wanted to see if the missingness of the `rating` column was attributed to the `sugar(PVD)` column. Therefore, I conducted a permutation test with the following hypotheses:

**Null Hypothesis:** The missingness of rating does not depend on the sugar's percentage of daily value. 

**Alternative Hypothesis:** The missingness of rating does depend on the sugar's percentage of daily value. 

Additionally, to help aid me in figuring out which test statistic to use I had plotted these two distributions together. However, the shapes of the plot was hard to see because of some of the larger outliers in the data set. For the sake of visualzation purposes, I had dropped 500 rows that had the highest sugar percentage of daily value, but the permutation test still utilizes all the data. Thus, no data was actually dropped from the test.

<iframe
  src="assets/Sugar_Missing.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
Based on how similar the shapes were I decided to use absolute difference in means as my test statistic. 

For this permutation test I have created a new column in a copy of my original data frame called 'missing_ratings' that contains True if the rating is missing or false if the rating is not missing. Because in the beginning of cleaning this data, I had made all the nan values into zeros we can find the missing values by finding all the zeros in the ratings column. Thus,for my permutation test, I had shuffled the 'missing_rating' column 1000 times and computed the test statistic 1000 times.

<iframe
  src="assets/Sugar_MAR.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
Looking at my resulting p-value and histogram, I can see that my resulting p-value is less than my alpha (0.05) therefore, I reject my null hypothesis. Thus, based on my test results, the the missingness of rating is a result of MAR because it appears from the test that rating depends on sugar(PDV).

2. Rating and Minutes (MCAR)

Now I had wanted to see if the missingness of the rating column was attributed to the `minutes` column. Therefore, I conducted a permutation test with the following hypotheses:

**Null Hypothesis:** The missingness of rating does not depend on the minutes it takes to prepare the meal. 

**Alternative hypothesis:** The missingness of rating does depend on the minutes it takes to prepare the meal. 

Additionally, to help aid me in figuring out which test statistic to use I had plotted these two distributions together. However, once again the shapes of the plot was hard to see because of some of the larger outliers in the data set. For the sake of visualzation purposes, I had dropped 500 rows that had the highest amount of minutes, but the permutation test still utilizes all the data. Thus, no data was actually dropped for the test.

<iframe
  src="assets/Minutes_Missing.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Similar to the last permutation test, I have created a new column called `missing_ratings` to indicate rating's missingness. Once again, because the minutes column contains numerical values, and because of the plot above displaying the similar shapes, I am able to use absolute mean differnce as mt test statistic for this permutation test.

<iframe
  src="assets/Minutes_MCAR.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Looking at my resulting p-value and histogram, I can see that my p-value is greater than my alpha (0.05) therefore, I fail to reject my null hypothesis. Thus, based on my test results, the the missingness of rating is not a result of MAR because rating does not depend on minutes. Thus the missingness is a result of MCAR.

## Hypothesis Testing

The salient question that I will be preforming an analysis on is: **Do recipes tagged as Mexican hold a higher rating on average compared to other recipes that are not labeled Mexican?**

**Null Hypothesis:** There will be no significant difference between the average rating for recipes tagged as Mexican versus those that aren't. 

**Alternative hypothesis:** There will be a significant difference between the average rating for recipes tagged as Mexican versus those that aren't. 

For my salient question, I will proceed by utilizing a permutation test in which I will shuffle the `is_mexican` column that I had made previously and test to see whether there is my data result from random chance or there is a signifcant difference.

My alternative hypothesis is one-sided because it is common knowledge (and my own opinion) that Mexican food is one of the more well known and well liked cuisines world wide (source: me). Thus, with this prior knowledge in mind we should anticipate that Mexican food will be rated higher and therefore my alternative hypothesis reflects this.

<iframe
  src="assets/Hyp_Test.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Because avg_rating is numerical I used the difference in means as my test statistic with an alpha of 0.05. 

## Framing a Prediction Problem
Now looking in terms of ratings, as we have mentioned and seen before there are many missing values in the ratings column. This might make it hard for one to determine whether they would like to make a certain recipe or not in the future. This is a tragedy that we must overcome. Think of all the tasty cuisines that many people will not have the chance to taste, the chance to have that authentic ratatouille experience (especially if it is a Mexican cuisine). Therefore For my prediction model I aim to be able to predict the rating of each recipe. 

Initially, I had thought that it would be better to perform a regression model because realistically it is not impossible to have a rating between two and 3 stars. However, as you’ll see later on I realized that for this type of data it is better to utilize a multi-classification model instead. The way that I am measuring these models is by using root mean square error for my base model. The reason why I chose this over the other suitable metrics is because then I would be able to tell how far apart on average all of my predictions were from the actual values. Thus, it gave me insight because the root mean square error was the same unit as the values that I am working with, so I can make judgements off of the comparisons. For my final model, I did end up utilizing the f1-score. Because my data is  unbalanced this means that I should not use accuracy and instead use f1-score which is more resilient from having an unbalanced classification.

## Baseline Model

For my baseline model, like I mentioned before, I unfortunately started off with Random Forest Regressor because my values are numerical and realistically it is possible to have ratings that could be continuous. So I tried to use a regressor as my baseline. Moving forward, for my baseline I had utilized the `n_ingredients` and `calorie(#)` columns. These two columns are qualitative and thus I had then binarized them at their respective means. I figured that these two columns would be some of the most relevant because the calorie column might explain why the higher ratings. For instance, if the meal was more fulfilling then maybe the calorie count was higher, making people give higher ratings. I had also done a number of ingredients because I noticed while I was doing my EDA that the higher the rating was that there were also more recipes with more ingredients.

Additionally, I had hot encoded my `is_mexican` column, which is nominal data. I thought that knowing the ethnicity of the food might help with predicting the rating. As we had seen in my hypothesis test, the dishes labeled as Mexican were likely rated higher not due to chance.Therefore, I applied this new found knowledge to my baseline. 

Finally, looking at the rmse which is 1.7858108334251612, I think my model is not doing so fire. I do not think it is doing good because the rmse value is so large for the ratings to be 1 to 5 stars. More specifically, it means on average my predictions with the model are almost 2 stars off. Therefore, I have concluded that this model was not the way to go.

## Final Model

For my final model, I had done a RandomForestClassifier. I created two new features which included the complexity of the recipe through using the column `n_steps` and I had sorted out positive and negative reviews through the  `review` column. I figured that the more steps there were in creating a recipe the easier the recipe is to follow and thus higher the rating. Additionally, I had felt like the review column might have been able to tell me the sentiment behind the review which I feel like might help explain what rating the user gave. So I had created a function which went through each review and looked for specific words  like ”great” and “happy” and I considered that review as True. If the other reviews did not contain words like these I had labeled them as False. In addition to those two new columns, I had also simply passed through the `avg_rating` column into the model. I implemented the average rating column because I felt like knowing what the rating of the recipe is might be a good general baseline for what people think about the recipe.

Finally, I had decided to use RandomForestClassifier because I had seen from my previous model that regression was creating poor predictions even after adding different columns to the model. It was until then when I realized that using a classifier simply for this data set would help improve my model’s predictions. I chose this because in this data set the ratings are whole numbers therefore they are easier to classify. Moving forwards, the method that I had used to create my overall model is utilizing GridSearchCV and I would fit my final multiple times on different hyperparameters to find the hyperparameter that worked the best for my model. For instance, once it would fit hyperparameters on my gridsearch object I was then able to check the f1-score and see whether it improved. If it had then I would try different hyperparameters around the ones GridSearchCV’s `.bestparams` had told me. Finally, I received my hyperparameters as `clf__max_depth` = 20, `clf__min_samples_split` =  75, `clf__n_estimators` = 500.

 Although I utilized f1-score to improve my final model compared to my base model where I used RMSE, I can see a significant improvement in my model’s performance. For this improvement, I had looked at both of my model’s accuracy instead so that they would be on the same metric type of metric. There I saw a significantly higher accuracy on my final model (0.77 on testing data) than on my base model (0.0005247939955534964 on testing data). Therefore, I concluded that my final model performed better in comparison to the base model. 

## Fairness Analysis

For my fairness analysis, I wanted to see if the recipes with **lower average ratings** (0 to 2.5) were as correctly predicted as the recipes with a **higher average rating** (2.5 to 5). Therefore my hypotheses were as followed:

**Null Hypothesis:** My model is fair. Its f1-score for predicting the ratings of recipes with lower average ratings (0 to 2.5 stars) will be roughly the same for predicting the ratings of recipes with higher average ratings (2.5 to 5 stars).


**Alternative Hypothesis:** Our model is unfair. Its  f1-score for predicting ratings for the recipes with lower average rating (0 to 2.5 stars) is lower than its f1-score for predicting ratings with higher average ratings (2.5 to 5 stars). 

To preform this permutation test I then did a test statistic of a difference in means utilizing an f1-score as my evaluation metric. For my alpha level I had done 0.05 and my p-value was 0.0. Therefore, I reject my null hypothesis and that my outcome is not likely out of random chance.

