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
| **n_steps** | Number of steps in recipe |
| **n_ingredients** | Number of ingredients in recipe |
| **rating** | Rating given |

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning 
We were provided with two raw CSV files, one that contained recipes, and one that contained reviews and ratings. We started data cleaning by merging the datasets together. They were merged so that all recipes that appeared in the first CSV file also appeared in the DataFrame, regardless of whether they had a rating or not. Then, in the new DataFrame, we filled all ratings of 0 with np.nan. We were able to do this because when someone was inputting a recipe, the lowest rating that they could have given is 1 star, so a rating of 0 stars really means that they didn't rate it. After that, we found the average rating per recipe, and added this as a column back to the recipes dataframe. 

Then, we looked at the columns we were using and noticed that there were some really large outliers (specifically in the 'minutes' column, but also smaller outliers in the 'n_ingredients' and 'n_steps' columns). To combat this, we chose to only consider the data that is within 2 standard deviations of the mean for these three columns. 

Below is the first couple of rows of the data cleaned DataFrame. This preview only includes the relevant columns. 

| name                                 |   minutes |   n_steps |   average rating |   n_ingredients |
|:-------------------------------------|----------:|----------:|-----------------:|----------------:|
| 1 brownies in the world    best ever |        40 |        10 |                4 |               9 |
| 1 in canada chocolate chip cookies   |        45 |        12 |                5 |              11 |
| 412 broccoli casserole               |        40 |         6 |                5 |               9 |
| millionaire pound cake               |       120 |         7 |                5 |               7 |
| 2000 meatloaf                        |        90 |        17 |                5 |              13 |

### Univariate Analysis

We performed univariate analysis on the "minutes" column in the dataset. 

<iframe
  src="assets/minutes-box.html"
  width="800"
  height="1000"
  frameborder="0"
></iframe>

From this graph, we can see that most of the data is centered between 20 minutes and 50 minutes, and it is heavily right-skewed. The data towards the top of the graph is more spread out than the data towards the bottom of the graph. From the graph, we can tell that "minutes" is most likely to be between 20 and 50, and this could be helpful when considering our initial question. 

### Bivariate Analysis
First, we added a column in the DataFrame that was a ratio of ingredients to steps (n_ingredients / n_steps). Then, we performed a bivariate analysis by graphing this column against the "minutes" column. 

<iframe
  src="assets/step-ing-ratio-minutes.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

From this graph, we can see that there is a roughly negative relationship between the step-ingredient ratio and time it takes to prepare a recipe. We ccan also see that some of the recipes that take the longest to prepare have a lower step-ingredient ratio. 

### Interesting Aggregates

Below is an interesting aggregate to note in the data set. 

|   Number of Steps |   Average Cooking Time (Minutes) |
|------------------:|---------------------------------:|
|                 1 |                          9.42455 |
|                 2 |                         11.8178  |
|                 3 |                         17.5343  |
|                 4 |                         22.7988  |
|                 5 |                         28.0374  |
|                 6 |                         32.08    |
|                 7 |                         34.7543  |
|                 8 |                         37.1898  |
|                 9 |                         39.558   |
|                10 |                         41.2045  |
|                11 |                         42.558   |
|                12 |                         44.9707  |
|                13 |                         45.5209  |
|                14 |                         47.1639  |
|                15 |                         49.0698  |
|                16 |                         49.6452  |
|                17 |                         51.7282  |
|                18 |                         51.4198  |
|                19 |                         52.8817  |
|                20 |                         53.129   |
|                21 |                         54.423   |
|                22 |                         59.5752  |
|                23 |                         58.4765  |
|                24 |                         57.567   |

We first grouped by the number of steps, then used the aggregate function mean() on the "minutes" column to find the mean cooking time. This table showed us that there is a positive correlation between these two variables. 

To visualize this relationship more, we also created a bar chart: 

<iframe
  src="assets/agg-box.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

As predicted, the graph shows that there is a positive correlation between number of steps and the average cooking time (when grouped by the number of steps in a recipe). 

### Imputation 
The only imputation we performed was previously mentioned in the Data Cleaning section. For completeness, it is restated below: 

In the new DataFrame, we filled all ratings of 0 with np.nan. We were able to do this because when someone was inputting a recipe, the lowest rating that they could have given is 1 star, so a rating of 0 stars really means that they didn't rate it.

## Baseline Model
Our baseline model utilizes a Random Forest Regressor in order to model the data. Our features - 'steps' and 'ingredients' - are both quantitative variables that we will use in order to predict average recipe preparation time across our dataset. This model performed with an r-squared value of 0.25 and a mean-squared-error (MSE) of 441.26. Thus, we can conclude that our current model does not fit the trends in our data very well - the r-squared value is relatively small and the MSE is high. We will need to better train the model in order to recieve better results.

### Final Model
Our final model introduces two new features - the ratio between the number of ingredients and the number of steps, called “ratio”, and the average ratings across recipes in the dataset. We decided to include “ratio” in our model, as the plot between the number of ingredients and number of steps in a recipe displayed a promising association. We felt that observing the relationship between this ratio and the number of minutes could lead to the further discovery of trends in our dataset. Similarly, we included the average ratings feature because it seemed reasonable to assume that recipes with shorter preparation times might result in higher ratings by users. We modified the “rating” column to be the average of every rating for a given recipe in the dataset (as we noticed there were varying ratings for the same recipe). We expected both of these variables to decrease our model’s MSE.

Our final estimate uses a Random Forest Regression model, where we took the logarithms of our features. We determined that several of our features followed patterns that resembled a logarithmic curve, which informed our decision to choose this feature engineering. Our two hyperparameters - as shown by a grid search analysis - were max depth (2 through 200 with 20 steps) and number of estimators (2 through 100 with 10 steps). The best max depth result was 22 and the best number of estimators result was 92. The addition of these new estimators decreased our MSE to 324.25, suggesting that these new features made a significant improvement to our model.


