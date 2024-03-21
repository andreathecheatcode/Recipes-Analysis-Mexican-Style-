# Recipes-Analysis-Mexican-Style-

This is a project analysis from DSC 80 at UCSD

## Introduction

  Have you ever been in a situation where your friends were pretentious enough to claim that a certain ethnic food was superior? Have you or a loved one ever been subjected to the situation when deciding where to go out and eat and one person chooses an ethnic food that you are in fact not in the mood to eat. WELL, you’ve come to the right place. With new foods constantly being made it might be hard and stressful to decide what to eat, so this project aims to help you make those tough decisions depending on the ethnicity of the cuisine. This brings me to the current question, How does the ethnicity of the food affect the rating of the recipe? However, for now, we will only look at a small lens of this question.Specifically we will be asking if: **Mexican cuisine holds a higher rating on average compared to food not labeled as Mexican cuisine?**

  Before getting our hands dirty (not from the tacos), I will be using a data set from food.com that contains recipes and reviews dating from 2008 onwards. The recipes data frame contains 83782 rows which represents a unique recipe for every row. This data set also contains 12 columns total however the relevant ones that I mainly emphasize are the tags, nutritional value, the number of ingredients, and number of steps columns. I also used another data frame which contained some of the reviews some people had left on certain recipes. This review data frame contained 731927 rows which did not contain unique recipes but unique reviews that people had left along with their rating of the food. As you will see in my analysis I ended up utilizing the rating column along with the review column. 

