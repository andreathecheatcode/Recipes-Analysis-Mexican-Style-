# Recipes-Analysis-Mexican-Style-

This is a project analysis from DSC 80 at UCSD

## Introduction

  Have you ever been in a situation where your friends were pretentious enough to claim that a certain ethnic food was superior? Have you or a loved one ever been subjected to the situation when deciding where to go out and eat and one person chooses an ethnic food that you are in fact not in the mood to eat. WELL, you’ve come to the right place. With new foods constantly being made it might be hard and stressful to decide what to eat, so this project aims to help you make those tough decisions depending on the ethnicity of the cuisine. This brings me to the current question, How does the ethnicity of the food affect the rating of the recipe? However, for now, we will only look at a small lens of this question. Specifically we will be asking if: **Mexican cuisine holds a higher rating on average compared to food not labeled as Mexican cuisine?**

  Before getting our hands dirty (not from the tacos), I will be using a data set from food.com that contains recipes and reviews dating from 2008 onwards. The recipes data frame contains 83782 rows which represents a unique recipe for every row. This data set also contains 12 columns total however the relevant ones that I mainly emphasize are the tags, nutritional value, the number of ingredients, and number of steps columns. I also used another data frame which contained some of the reviews some people had left on certain recipes. This review data frame contained 731927 rows which did not contain unique recipes but unique reviews that people had left along with their rating of the food. As you will see in my analysis I ended up utilizing the rating column along with the review column. 

## Data Cleaning and Exploratory Data Analysis:

In terms of cleaning the data, I approached cleaning the data first by noticing the types of each value in the two dataframes. From this observation, I noticed that the nutrition column was consider a string object that looked like a l
ist containing 'calories(#)', 'total fat(PDV)', 'sugar(PDV)', 'sodium(PDV)', 'protein(PDV)', 'saturated fat(PDV)', 'carbohydrates(PDV)' specifically in this order. Therefore, I had turned all the values in that column into an actual list and then appended each column into their own respective columns with their proper labels.

Next, I wanted to match the recipes with their respective reviews. Thus, I had merged the recipes and reviews data sets together.

After merging, I noticed that there was a significant amount of NaNs in the ratings column. To further clean the data I had then filled all the NaNs in the rating column with 0. I had specifically changed them to 0 because they would still indicate a NaN value. For instance, in terms of ratings it is not possible to give a rating of 0, the lowest rating that one can get is a 1.

Finally, I added two new columns to the final data frame:
The first new column being added is called ‘avg_rating’ which is the average rating from all the reviews for a specific recipe. 
The second column being added is called ‘is_mexican’ and is derived from the ‘tags’ column. In this analysis, recipes tagged with ‘mexican’ are then considered a mexican dish. As a results, the True values indicates that a recipe has a ‘mexican’ tag and those that have False values did not tag this dish as ‘mexican’
After cleaning the data this is what the final data frame looks like:

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

In terms of NMAR, we can see that there are missing values (NaN values) in the review columns. We can likely conclude that there are missing values here because while the people were rating the food they might have not felt very strongly about a particular recipe that they tried out. So because these people did not feel a strong enough emotion to create a review they might have felt like they had nothing to say and thus they left no review.

### Missingness Dependency

Now we can look at the missingness of some of the data that might depend on other columns in the dataset. To help explain the missingness of a column I used permutation tests on specific columns to potentially help explain the missingness seen in the rating column.

1. Rating and Sugar(PDV) (MAR)

First I had wanted to see if the missingness of the rating column was attributed to the 'sugar(PVD)' column. Therefore, I conducted a permutation test with the following hypotheses:

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

Now I had wanted to see if the missingness of the rating column was attributed to the 'minutes' column. Therefore, I conducted a permutation test with the following hypotheses:

**Null Hypothesis:** The missingness of rating does not depend on the minutes it takes to prepare the meal. 

**Alternative hypothesis:** The missingness of rating does depend on the minutes it takes to prepare the meal. 

Additionally, to help aid me in figuring out which test statistic to use I had plotted these two distributions together. However, once again the shapes of the plot was hard to see because of some of the larger outliers in the data set. For the sake of visualzation purposes, I had dropped 500 rows that had the highest amount of minutes, but the permutation test still utilizes all the data. Thus, no data was actually dropped for the test.

<iframe
  src="assets/Minutes_Missing.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Similar to the last permutation test, I have created a new column called 'missing_ratings' to indicate rating's missingness. Once again, because the minutes column contains numerical values, and because of the plot above displaying the similar shapes, I am able to use absolute mean differnce as mt test statistic for this permutation test.

<iframe
  src="assets/Minutes_MCAR.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Looking at my resulting p-value and histogram, I can see that my p-value is greater than my alpha (0.05) therefore, I fail to reject my null hypothesis. Thus, based on my test results, the the missingness of rating is not a result of MAR because rating does not depend on minutes. Thus the missingness is a result of MCAR.
