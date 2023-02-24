# Recipes and Ratings and Analysis: Do recipes with chocolate have a higher rating?
This project is an exploratory data analysis project for the class DSC 80 at UCSD by Anushka Purohit and Neil Damle.

## Introduction
### Introduction and Question Identification
This data set is composed of two components - a recipe component (with individual recipes and their details) and an interactions component (which includes the reviews of recipes). To create the dataset that we analyzed, we merged these two components to create a dataset of recipes along with their average ratings. Other information in this merged dataset included the ingredients in each recipe, as well as the number of steps required to make it. The final dataset has 83782 rows, or 83, 782 individual recipes. This is a highly applicable/relevant dataset because of its size, and the fact that it is crowdsourced, which means it may be able to serve as a representation of all recipes in general.

After looking at the dataset, the question we decided to dive deeper into was: **Do recipes with chocolate have higher ratings?**

We thought this was a relevant question because it would allow us to explore the psychology of recipe rating, and potentially identify if people’s sweet tooth affected how they judged a dish’s quality. The reason we chose chocolate in particular was because of its specificity, and also its presence in a variety of well known desserts and sweet dishes. 

As we moved forward with this question, the most important columns in the dataset were the ratings column and the chocolate column (which we created). The *rating* column was the average rating of a recipe from the interactions dataset, and it allowed us to quantify the perceived quality of a dish. The *chocolate* column was one created from the *ingredients* column, by searching for ingredient lists that included the word ‘chocolate’. The chocolate column then served as a boolean way to identify recipes containing chocolate. There were some issues with this method, such as a failure to account for typos or mislabeled names, but it served as an overall accurate representation.

---
## Cleaning and EDA (Exploratory Data Analysis)
### Data Cleaning
### Univariate Analysis
### Bivariate Analysis
### Interesting Aggregates
---
## Assessment of Missingness
### NMAR Analysis
In our dataset, the column 'description' has missing values. We believe this column is NMAR (Not Missing At Random) because 
### Missingness Dependency
To analyze missingness, we chose the 'rating' column which is a quantitative column with missing values. 
We wanted to analyze its dependency of missingness of 'rating' with other columns. 

First we analyzed 'rating' column's dependency of missingness on the column 'n_ingredients'.
Here is a histogram distribution plot showing the distribution of 'n_ingredients' when 'rating' is missing and when 'rating' is not missing. There are also box plots on the top showing the spread of the two.
<iframe src="assets/hist_ingred.html" width=800 height=600 frameBorder=0></iframe>
You can notice that the distributions when rating is missing and rating is not missing are very similar and centered around the same location as well.
Here is also a kernel density estimate plot of the two distributions. Here you can see that they are centered around the same location but the shape is different. When rating is not missing, the distribution has a more zig-zag pattern.
<iframe src="assets/kde_n_ingred.html" width=800 height=600 frameBorder=0></iframe>
Since the shapes are slightly different but centered around the same location, we chose to use the Kolmogorov-Smirnov test statistic when conducting the permutation test. 
After conducting our permutation test, we got a p-value of 0.11, which is greater than the significance value of 0.05 so we fail to reject the null hypothesis and conclude that the missingness of 'rating' does not depend on 'n_ingredients'. 

Next, we analyzed 'rating' column's dependency of missingness on the column 'n_steps'.
Here is a histogram distribution plot showing the distribution of 'n_steps' when 'rating' is missing and when 'rating' is not missing. There are also box plots on the top showing the spread of the two.
<iframe src="assets/hist_n_steps.html" width=800 height=600 frameBorder=0></iframe>
You can notice that the distribution shapes are very similar but are slightly shifted. 
Here is also a kernel density estimate plot of the two distributions. 
<iframe src="assets/kde_n_steps.html" width=800 height=600 frameBorder=0></iframe>
Since the shapes are pretty similar but just shifted, we decided to use the absolute difference of means test statistic when conducting the permutation test. 
After conducting the permutation test, we got a p-value of 0.0.
We also did a permutation with the Kolmogorov-Smirnov test statistic since the location of the centers were very similar. For this, we got a p-value of 3.813369074131651e-13, which is extremely small and rounds to 0. 
Since the p-value is less than the significance level of 0.05, we reject the null hypothesis and conclude that the missingness of 'rating' does depend on the column 'n_steps'. 
Here is an empirical distribution of the absolute difference of means for this permutation test:
<iframe src="assets/fig.html" width=800 height=600 frameBorder=0></iframe>
The red line is the observed absolute difference of means, which you can see was pretty far from the rest of the simulated differences. 
---
## Hypothesis Testing


