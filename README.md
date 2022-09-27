# Addiscore – An indicator to simplify the choice of prepared meals

## Overview

Around 80% of products in supermarkets are prepared meals.

**Making a healthy choice** between these products is **extremely complicated** :

- The list of ingredients is often in many languages, full of incomprehensible extracts, and too small to read
- Some basic products (example : Beef Carpaccio) are labelled Good (Nutriscore A) to Bad (Nutriscore D)
- The number of additives is not mentioned or considered by the Nutriscore.
- To replace gluten, fats or sugars and improve their Nutriscore, many « healthy » products are packed full of potentially dangerous additives.

This project conducts statistical and exploratory analysis of open data contributed by thousands of volunteers in the worldwide OpenFoodFacts database (https://world.openfoodfacts.org/)

By combining this data with JSON data from REST api calls to addititive information, the project concludes:

- **We don't know what we eat** (80% of products are missing the list of ingredients in apps like Yuka)
- More than **50% of products contain risky additives** (>75% of sandwiches)
- **No way to distinguish products with risky additives**

To aid consumers make healthy choices, two indicators are proposed to supplement the Nutriscore

- **Addiscore_risk** : A colour to indicate **the presence of risky additives**:

  - 🟩 no additives 🟨 low risk 🟧 moderate risk 🟥 high risk of over-exposure

- **Addiscore** – A score based on the number of additives in each risk group.
  - For example: `addiscore = 1 * [low risk] + 2 * [moderate risk] + 5 * [high risk]`

The relation between these two indicators and the nutriscore is explored for different food groups and by country.

### Conclusion: How to Avoid Risky Additives in Ready-to-Eat Meals

- ➡️ Avoid prepared products from food categories at high risk:
  - sandwiches, pizzas, artificially sweetened drinks, dairy desserts, processed meats
- ➡️ Use a (simple) recommendation system based on the addiscore:
  - find the main category of a given product (example: pizza)
  - if there are other products in this category
    - sort by addiscore
    - propose alternative products with the best nutrigrade in the top addiscore

## Motivation

This is project 3 for the **Master in Data Science** (in French, BAC+5) from OpenClassrooms, which requests innovative ideas for applications related to food for the French public health agency

The project demonstrates :

- cleaning and preprocessing pipelines for large files of structured data (> 4 Gb)
- readable and relevant graphic representations
- univariate and multivariate statistical analysis (parametric and non-parametric tests)

## Requirements

To run the notebooks, the dataset must be placed in a DATA_FOLDER ('data/raw'). Python libraries are listed in `requirements.txt`. Each notebook also includes a list of its own requirements, and a procedure for `pip install` of any missing libraries.

**Data** : The dataset (format CSV) can be downloaded (~5Gb) from the site <https://world.openfoodfacts.org/data> or directly from this link: [en.openfoodfacts.org.products.csv](https://static.openfoodfacts.org/data/en.openfoodfacts.org.products.csv.gz)

**Python libraries** :
`numpy, pandas, matplotlib, seaborn, scikit-learn, scipy, statsmodels, missingno, requests, wordcloud`

## Files

- [P3_nettoyage.ipynb](./P3_nettoyage.ipynb) : import, cleaning, conversion of json API requests to additives tables
  <a href="https://colab.research.google.com/github/mrcreasey/oc-ds-p3-eda-visualisation/blob/master/P3_nettoyage.ipynb" target="blank"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab"/></a>
- [P3_exploration.ipynb](./P3_exploration.ipynb) : exploratory data analysis, univariate and multivariate statistical analysis
  <a href="https://colab.research.google.com/github/mrcreasey/oc-ds-p3-eda-visualisation/blob/master/P3_exploration.ipynb" target="blank"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab"/>
  </a>
- [P3_support.pdf](./P3_support.pdf) : a presentation of the project

_Note_ : Files are in French. _As requested for the project, the jupyter notebooks have not been cleaned up : the focus is on data cleaning, imputation, data visualisation and statistical analysis_.

_Custom functions created in this project for data preprocessing, statistical analysis and data visualisation are encapsulated within each notebook, to avoid importing and versioning custom libraries._

## Approach

While exploring the data, questions arise, necessitating an iterative cleaning process. For example:

- The database contains data contributed over a period of almost 10 years.
  - How frequently are products updated ?
  - What percentage of products are still relevant?`
- There are 1000s of contributors, most provide incomplete information
  - Over 80% of French products are missing all information about ingredients and additives: Mobile apps used to "choose healthy food products" are unable to assess the additive risk for 80% of products
  - Why do some products have over 200 registers in the database?
  - Can we merge data from many countries ?
  - Can we impute additive risks from a product category?
  - Can we avoid additives by avoiding certain product categories ?

The number of possibilities for exploration of data is enormous.

For details of exploration, see the table of contents in each workbook, and the presentation slides.

### Data Cleaning

Data cleaning was conducted using Google Colab, using machines with 16Gb RAM.

Processing pipelines were created including:

- Conversion to datetime, integer and category data types
- Elimination of irrelevant columns and duplicate information (products)
- Outlier detection and treatment of aberrant data
- Imputation of missing values (median, KNN regressors, decision tree regressors)
- Conversion of hierachical additives JSON to flat CSV tables

### Univariate and multivariate statistical analyses:

Statistical analysis and visualisation of additives is not trivial: The additives are present as (nested) lists of tags in one of many tag columns.

Descriptive statistics were calculated on data filtered and / or grouped by country, year, contributor, food category, NOVA group, nutriscore group, addiscore_risk group...

- Mean, standard deviation, median, skew, kurtosis
- Outliers were detected by percentiles (Inter-Quartile Range)
- Pearson's correlation for numeric variables

For testing hypotheses, the following tests were used:

- Tests of normality: Shapiro-Wilk, Kolmogorov-Smirnov goodness-of-fit,
- Tests of homoscedascity: Bartlett, Levene
- Parametric tests: Student's t-test, ANOVA (F-test)
- Non-parametric tests: (Wilcoxon) Mann–Whitney U test, Kruskal-Wallis H-test, Pairwise Tukey HSD

### Data Visualisation

A wide range of data visualisation techniques were used to explore the data.

- KDE plot, histogram, pie chart, time serie, stacked column, venn diagram
- correlation heatmap, pairplot, barplot, lineplot, jointplot, box-whisker plot
- PCA (principal component analysis), dendrogram, clustermap
- wordclouds

## Features (Keywords)

- api requests, json manipulation, datetime conversions
- python, data-preprocessing, exploratory data analysis, data visualisation
- filter, explode, group, intersect, visualise tag list columns

## Skills acquired

- Perform cleaning operations on structured data
- Communicate results using readable and relevant graphic representations
- Perform multivariate statistical analysis
- Perform univariate statistical analysis
