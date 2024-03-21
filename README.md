# Recipes-Analysis-Mexican-Style-

This is a project analysis from DSC 80 at UCSD

## Introduction

  Have you ever been in a situation where your friends were pretentious enough to claim that a certain ethnic food was superior? Have you or a loved one ever been subjected to the situation when deciding where to go out and eat and one person chooses an ethnic food that you are in fact not in the mood to eat. WELL, you’ve come to the right place. With new foods constantly being made it might be hard and stressful to decide what to eat, so this project aims to help you make those tough decisions depending on the ethnicity of the cuisine. This brings me to the current question, How does the ethnicity of the food affect the rating of the recipe? However, for now, we will only look at a small lens of this question.Specifically we will be asking if: **Mexican cuisine holds a higher rating on average compared to food not labeled as Mexican cuisine?**

  Before getting our hands dirty (not from the tacos), I will be using a data set from food.com that contains recipes and reviews dating from 2008 onwards. The recipes data frame contains 83782 rows which represents a unique recipe for every row. This data set also contains 12 columns total however the relevant ones that I mainly emphasize are the tags, nutritional value, the number of ingredients, and number of steps columns. I also used another data frame which contained some of the reviews some people had left on certain recipes. This review data frame contained 731927 rows which did not contain unique recipes but unique reviews that people had left along with their rating of the food. As you will see in my analysis I ended up utilizing the rating column along with the review column. 

## Data Cleaning and Exploratory Data Analysis:

In terms of cleaning the data, I approached cleaning the data first by noticing the types of each value in the two dataframes. From this observation, I noticed that the nutrition column was consider a string object that looked like a list containing 'calories(#)', 'total fat(PDV)', 'sugar(PDV)', 'sodium(PDV)', 'protein(PDV)', 'saturated fat(PDV)', 'carbohydrates(PDV)' specifically in this order. Therefore, I had turned all the values in that column into an actual list and then appended each column into their own respective columns with their proper labels.

Next, I wanted to match the recipes with their respective reviews. Thus, I had merged the recipes and reviews data sets together.

After merging, I noticed that there was a significant amount of NaNs in the ratings column. To further clean the data I had then filled all the NaNs in the rating column with 0. I had specifically changed them to 0 because they would still indicate a NaN value. For instance, in terms of ratings it is not possible to give a rating of 0, the lowest rating that one can get is a 1. 

Finally, I added two new columns to the final data frame:
The first new column being added is called ‘avg_rating’ which is the average rating from all the reviews for a specific recipe. 
The second column being added is called ‘is_mexican’ and is derived from the ‘tags’ column. In this analysis, recipes tagged with ‘mexican’ are then considered a mexican dish. As a results, the True values indicates that a recipe has a ‘mexican’ tag and those that have False values did not tag this dish as ‘mexican’
After cleaning the data this is what the final data frame looks like:


