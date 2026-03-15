# Do High-Protein Recipes Actually Get Better Ratings?

### Author: Richard Wang

# Introduction

## Dataset Overview

This project uses the **Food.com Recipes dataset**, which combines recipe-level information with user interaction data. The dataset was constructed by merging two tables: `RAW_recipes`, which contains detailed information about each recipe, and `interactions`, which contains user ratings and reviews. After merging these datasets, I computed the **average rating for each recipe** to summarize user feedback.

The final merged dataset contains **78,167 recipes**, with each row representing a single recipe. The dataset includes information about recipe preparation details, nutritional content, and aggregated user ratings.

---

## Research Question

The central question for this project is:

**Are recipes with higher protein density associated with higher average user ratings?**

Rather than examining the absolute amount of protein in a recipe, I focus on **protein density**, defined as the amount of protein relative to the recipe’s calorie content. This approach allows for more meaningful comparisons across recipes with different serving sizes and total caloric values.

---

## Why This Question Matters

In recent years, many food brands and recipes have increasingly marketed themselves as **“high protein.”** Protein is commonly associated with health, fitness, and nutritional quality, and it has become a strong marketing signal in the food industry.

However, a recipe with a high absolute amount of protein may also contain a large number of calories, meaning that protein may not actually dominate its nutritional profile. Examining **protein density** instead of raw protein content provides a clearer picture of how protein-heavy a recipe truly is.

By studying the relationship between protein density and user ratings, this project investigates whether consumers genuinely prefer protein-dense recipes or whether protein primarily serves as a marketing signal. This analysis provides insight into how nutritional composition may influence user perceptions of recipe quality.

---

## Relevant Columns

Several variables in the dataset are particularly important for this analysis:

**avg_rating**  
The average rating given to a recipe by users, ranging from 1 to 5. This is the primary outcome variable used to measure recipe popularity.

**protein_pdv**  
The percent daily value (PDV) of protein contained in the recipe. This represents the relative amount of protein in the dish.

**calories**  
The total calorie content of the recipe. This variable provides context for interpreting protein levels.

Using these variables, I construct a derived feature called **protein density**, which represents the amount of protein relative to total calories. This feature helps capture how protein-dominant a recipe is within its overall nutritional profile.


# Data Cleaning and Exploratory Data Analysis

## Data Cleaning

Before beginning the analysis, I cleaned the Food.com recipes dataset to ensure that the variables used in the project were accurate, interpretable, and comparable across recipes.

The original data came from two files: `RAW_recipes`, which contains recipe-level information such as preparation time, ingredients, and nutritional values, and `interactions`, which contains user ratings and reviews. Because ratings are stored separately from the recipes themselves, I first merged these two datasets so that each recipe could be associated with the ratings given by users. After merging, I computed an `avg_rating` column representing the average rating for each recipe.

Recipes with no ratings were removed from the dataset. Since the research question focuses on whether nutritional characteristics are associated with **user ratings**, recipes without ratings cannot contribute to this analysis and would introduce missing values in the target variable.

Next, I cleaned the `nutrition` column. In the raw dataset, this column is stored as a string that represents a list of values rather than as individual numeric variables. According to the dataset documentation, the list contains values for calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates. I parsed this column and separated it into individual numeric columns so that these nutritional variables could be analyzed and used for feature construction.

To better compare recipes of different sizes, I created a new feature called **protein density**, defined as the protein percent daily value divided by the total calories in the recipe. This transformation is important because absolute protein alone can be misleading; a recipe with high protein may simply have very high calories overall. Protein density provides a more meaningful measure of how protein-heavy a recipe is relative to its caloric content.

After constructing this feature, I removed rows with missing values in either protein or calories, since these variables are necessary to compute protein density. Finally, I removed extreme outliers in protein density using the **interquartile range (IQR) rule**. Outliers may occur due to data entry issues or unusual recipes and can disproportionately influence visualizations and statistical analysis.

These cleaning steps ensured that the dataset used in the analysis contains valid numeric variables, meaningful nutritional features, and reliable rating information.

### Cleaned Dataset Preview

Below are the first few rows of the cleaned dataset used for the analysis.

| name                                 |   minutes |   n_steps |   n_ingredients |   calories |   protein_pdv |   protein_density |   avg_rating |
|:-------------------------------------|----------:|----------:|----------------:|-----------:|--------------:|------------------:|-------------:|
| 1 brownies in the world    best ever |        40 |        10 |               9 |      138.4 |             3 |         0.0216763 |            4 |
| 1 in canada chocolate chip cookies   |        45 |        12 |              11 |      595.1 |            13 |         0.0218451 |            5 |
| 412 broccoli casserole               |        40 |         6 |               9 |      194.8 |            22 |         0.112936  |            5 |
| millionaire pound cake               |       120 |         7 |               7 |      878.3 |            20 |         0.0227713 |            5 |
| 2000 meatloaf                        |        90 |        17 |              13 |      267   |            29 |         0.108614  |            5 |

## Univariate Analysis

To better understand the key variables used in this project, I examined the distributions of **protein density** and **average recipe ratings** separately.

### Distribution of Protein Density

<iframe
  src="assets/protein-density.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>
The distribution of **protein density** is **right-skewed**, meaning that most recipes have relatively low protein density while a smaller number of recipes have much higher protein density. This suggests that highly protein-dense recipes are less common in the dataset, while most recipes contain more moderate or lower levels of protein relative to calories.

### Distribution of Average Recipe Ratings

<iframe
  src="assets/avg-rating.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>
The distribution of **average recipe ratings** is concentrated near the high end of the scale, especially around **4 to 5 stars**. This suggests that Food.com users tend to rate recipes positively overall, which may indicate **rating inflation** or a general tendency for users to leave favorable reviews.

## Bivariate Analysis

To examine the relationship between nutritional composition and user ratings, I compared **average recipe ratings** across groups of **protein density**.

### Protein Density vs Average Recipe Rating

To make the relationship easier to interpret, I divided recipes into four groups based on protein density quartiles: **Low**, **Medium-Low**, **Medium-High**, and **High**. I then used a box plot to compare the distribution of `avg_rating` across these groups.

<iframe
  src="assets/protein-rating-boxplot.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>

The median ratings appear fairly similar across all four protein density groups, suggesting that recipes with higher protein density do not consistently receive higher average ratings. While there may be slight differences in spread or central tendency across groups, the plot does not show a strong visual association between protein density and recipe ratings.

## Interesting Aggregates

To further examine the relationship between protein density and user ratings, I grouped recipes into four protein density levels based on quartiles: **Low, Medium-Low, Medium-High, and High**. I then computed summary statistics of the average rating within each group.

<iframe
  src="assets/protein-density-summary.html"
  width="700"
  height="350"
  frameborder="0">
</iframe>

The table summarizes the number of recipes and rating statistics for each protein density group. The average ratings are very similar across groups, ranging from roughly **4.60 to 4.66**, and the median rating is **5.0 in all groups**. This suggests that recipes with higher protein density do not appear to receive noticeably higher ratings than those with lower protein density.

While the distributions are very similar, these small differences motivate a **formal hypothesis test** to determine whether any observed differences could simply be due to random variation.







# Assessment of Missingness
# Hypothesis Testing
# Framing a Prediction Problem
# Baseline Model
# Final Model
# Fairness Analysis
