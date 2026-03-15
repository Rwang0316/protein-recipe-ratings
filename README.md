# Do High-Protein Recipes Actually Get Better Ratings?

### Richard Wang

### Dataset Overview

For this project, I am using the Food.com Recipes dataset, which combines recipe-level information with user ratings. The dataset was created by merging the RAW_recipes and interactions datasets to compute the average rating for each recipe.

The merged dataset contains one row per recipe and includes detailed nutritional information, preparation details, and aggregated user ratings.

After cleaning and merging, the dataset contains 78167 recipes.

### Research Question

This project is centered around the following question:

Are recipes with higher protein density associated with higher average user ratings?

Rather than examining absolute protein amount alone, this project focuses on protein density — the amount of protein relative to the recipe’s calorie content. This allows for a more meaningful comparison across recipes of different sizes and total caloric values.

### Why This Question Matters

In recent years, many brands actively market their food products and recipes as “high protein” to attract more customers. Protein has become a strong selling point in the food industry, often associated with health, fitness, and overall quality.

However, higher absolute protein does not necessarily mean a recipe is protein-dominant relative to its total nutritional profile. A high-calorie recipe may contain a large amount of protein but still be nutritionally unbalanced.

By investigating whether protein density is associated with user ratings, this project explores whether consumers truly prefer protein-heavy recipes or whether protein primarily functions as a marketing signal. Understanding this relationship provides insight into consumer behavior and the extent to which nutritional composition influences perceived quality.

### Relevant Columns

The following columns are central to this analysis:

**avg_rating**
The average rating given to a recipe by users (continuous variable from 1 to 5). This is the primary outcome variable.

**protein_pdv**
The percent daily value of protein contained in the recipe. This represents the amount of protein in the recipe.

**calories**
The total calorie content of the recipe. This is used to contextualize protein levels and allows for the creation of a protein density measure (protein relative to total calories).

From these variables, I construct a derived feature — **protein density** — to better capture how protein-dominant a recipe is relative to its overall caloric content.
