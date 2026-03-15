# Do High-Protein Recipes Actually Get Better Ratings?

### Author: Richard Wang

# Introduction

### Dataset Overview

This project uses the **Food.com Recipes dataset**, which combines recipe-level information with user interaction data. The dataset was constructed by merging two tables: `RAW_recipes`, which contains detailed information about each recipe, and `interactions`, which contains user ratings and reviews. After merging these datasets, I computed the **average rating for each recipe** to summarize user feedback.

The final merged dataset contains **78,167 recipes**, with each row representing a single recipe. The dataset includes information about recipe preparation details, nutritional content, and aggregated user ratings.

---

### Research Question

The central question for this project is:

**Are recipes with higher protein density associated with higher average user ratings?**

Rather than examining the absolute amount of protein in a recipe, I focus on **protein density**, defined as the amount of protein relative to the recipe’s calorie content. This approach allows for more meaningful comparisons across recipes with different serving sizes and total caloric values.

---

### Why This Question Matters

In recent years, many food brands and recipes have increasingly marketed themselves as **“high protein.”** Protein is commonly associated with health, fitness, and nutritional quality, and it has become a strong marketing signal in the food industry.

However, a recipe with a high absolute amount of protein may also contain a large number of calories, meaning that protein may not actually dominate its nutritional profile. Examining **protein density** instead of raw protein content provides a clearer picture of how protein-heavy a recipe truly is.

By studying the relationship between protein density and user ratings, this project investigates whether consumers genuinely prefer protein-dense recipes or whether protein primarily serves as a marketing signal. This analysis provides insight into how nutritional composition may influence user perceptions of recipe quality.

---

### Relevant Columns

Several variables in the dataset are particularly important for this analysis:

**avg_rating**  
The average rating given to a recipe by users, ranging from 1 to 5. This is the primary outcome variable used to measure recipe popularity.

**protein_pdv**  
The percent daily value (PDV) of protein contained in the recipe. This represents the relative amount of protein in the dish.

**calories**  
The total calorie content of the recipe. This variable provides context for interpreting protein levels.

Using these variables, I construct a derived feature called **protein density**, which represents the amount of protein relative to total calories. This feature helps capture how protein-dominant a recipe is within its overall nutritional profile.


# Data Cleaning and Exploratory Data Analysis
# Assessment of Missingness
# Hypothesis Testing
# Framing a Prediction Problem
# Baseline Model
# Final Model
# Fairness Analysis
