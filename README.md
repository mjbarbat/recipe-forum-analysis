# Food.com Recipe Analysis

Food.com Recipe and Rating Analysis is a comprehensive data science project designed to explore culinary trends from recipes and user reviews. The project involves multiple stages of analysis, including data preprocessing, exploratory data analysis, and modeling.

Authors: Manu Anand & Melissa Barbat

## Introduction

In this project, we are analyzing a dataset of recipes and ratings sourced from [food.com](food.com), focusing on predicting cooking time based on the number of steps in a recipe. The dataset includes detailed information about recipes, such as preparation time and user-generated tags, alongside user ratings and reviews. This subset of data spans recipes and reviews submitted since 2008, offering a large foundation for analysis.

Our approach begins with cleaning the dataset and conducting exploratory data analysis to understand the relationship between recipe attributes and cooking time. We will also analyze potential patterns and correlations between the number of steps and preparation time across a variety of recipe types.

Our research question is: 

>**How accurately can we predict cooking time based on the number of steps in a recipe?**

Using this investigation, we aim to build a predictive model that helps streamline recipe planning for users by providing accurate cooking time estimates. This insight could enhance recipe recommendation systems, improving user experience by tailoring recommendations to their time constraints and preferences.

### Description of Columns

The dataset provides a comprehensive collection of columns that capture key details about recipes and user interactions on Food.com. With 4,051,980 rows, this dataset offers insights into cooking times, recipe steps, user reviews, and ratings. Below is an introduction to some of the essential columns:


| Column                                                      | Description         |
| ----------------------------------------------------------- | ------------------- |
| **name** | Recipe name |
| **minutes**  | minutes to prepare recipe |
| **tags**  | Food.com tags for recipe |
| **n_steps** | Number of steps in recipe |
| **n_ingredients** | Number of ingredients in recipe |
| **steps** | Text for recipe steps, in order |
| **rating** | Rating given |
| **review** | Review text |

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning 
We were provided with two raw CSV files, one that contained recipes, and one that contained reviews and ratings. We started data cleaning by merging the datasets together. They were merged so that all recipes that appeared in the first CSV file also appeared in the DataFrame, regardless of whether they had a rating or not. Then, in the new DataFrame, we filled all ratings of 0 with np.nan. This is because when someone was inputting a recipe, the lowest rating that they could have given is 1 star, so a rating of 0 stars really means that they didn't rate it. After that, we found the average rating per recipe, and added this as a column back to the recipes dataframe. 

Then, we looked at the columns we were using and noticed that there were some really large outliers (specifically in the 'minutes' column, but also smaller outliers in the 'n_ingredients' and 'n_steps' columns). To combat this, we chose to only consider the data that is within 2 standard deviations of the mean for these three columns. 

Below is the first couple of rows of the data cleaned DataFrame. This preview only includes the relevant columns. 

|    | name                                 |   minutes |   n_steps |   average rating |   n_ingredients |
|---:|:-------------------------------------|----------:|----------:|-----------------:|----------------:|
|  0 | 1 brownies in the world    best ever |        40 |        10 |                4 |               9 |
|  1 | 1 in canada chocolate chip cookies   |        45 |        12 |                5 |              11 |
|  2 | 412 broccoli casserole               |        40 |         6 |                5 |               9 |
|  3 | 412 broccoli casserole               |        40 |         6 |                5 |               9 |
|  4 | 412 broccoli casserole               |        40 |         6 |                5 |               9 |