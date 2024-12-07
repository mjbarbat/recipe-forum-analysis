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
We were provided with two raw CSV files, one that contained recipes, and one that contained reviews and ratings. We started data cleaning by merging the datasets together. They were merged so that all recipes that appeared in the first CSV file also appeared in the DataFrame, regardless of whether they had a rating or not. Then, in the new DataFrame, we filled all ratings of 0 with np.nan. This is because when someone was inputting a recipe,

In the merged dataset, fill all ratings of 0 with np.nan. (Think about why this is a reasonable step, and include your justification in your website.)
Find the average rating per recipe, as a Series.
Add this Series containing the average rating per recipe back to the recipes dataset however you’d like (e.g., by merging). Use the resulting dataset for all of your analysis.



