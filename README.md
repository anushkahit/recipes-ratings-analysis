# Recipes and Ratings Analysis: Do recipes with chocolate have a higher rating?
This project is an exploratory data analysis project for the class DSC 80 at UCSD by Anushka Purohit and Neil Damle.

## Introduction
### Introduction and Question Identification
This data set is composed of two components - a recipe component (with individual recipes and their details) and an interactions component (which includes the reviews of recipes). To create the dataset that we analyzed, we merged these two components to create a dataset of recipes along with their average ratings. Other information in this merged dataset included the ingredients in each recipe, as well as the number of steps required to make it. The final dataset has 83782 rows, or 83, 782 individual recipes. This is a highly applicable/relevant dataset because of its size, and the fact that it is crowdsourced, which means it may be able to serve as a representation of all recipes in general.

After looking at the dataset, the question we decided to dive deeper into was: **Do recipes with chocolate have higher ratings?**

We thought this was a relevant question because it would allow us to explore the psychology of recipe rating, and potentially identify if people’s sweet tooth affected how they judged a dish’s quality. The reason we chose chocolate in particular was because of its specificity, and also its presence in a variety of well known desserts and sweet dishes. 

As we moved forward with this question, the most important columns in the dataset were the ratings column and the chocolate column (which we created). The *rating* column was the average rating of a recipe from the interactions dataset, and it allowed us to quantify the perceived quality of a dish. The *chocolate* column was one created from the *ingredients* column, by searching for ingredient lists that included the word ‘chocolate’. The chocolate column then served as a boolean way to identify recipes containing chocolate. There were some issues with this method, such as a failure to account for typos or mislabeled ingredient names, but it served as an overall accurate representation.

---
## Cleaning and EDA (Exploratory Data Analysis)
### Data Cleaning
Some of the initial data cleaning efforts took place before merging the two datasets together. We converted all the ratings in the interaction dataframe that were 0 to np.nan, which allowed us to ignore them in the calculations for the mean. 

Once we had a merged dataset, we had to make sure that all the columns were the correct types. For example, we had to convert the *submitted* column, which was originally a string, to datetime objects, which allowed us to make visualizations and analyses using that data. Many of the columns also started as strings which only looked like lists, rather than actually being lists of strings. To solve this, we split these strings and added the components to lists. This allowed us to actually access individual components of these lists. Interestingly, the *ingredients* column also had a similar problem, but because we only used it to check if chocolate was an ingredient, we did not convert it to a list. We instead searched the whole string for occurrences of the string “chocolate”, which allowed us to create the *chocolate* column in the data frame.

| name                                 |     id |   minutes |   contributor_id | submitted           |   n_steps | ingredients                                                                                                                                                                                                                             |   n_ingredients |   rating | chocolate   |
|:-------------------------------------|-------:|----------:|-----------------:|:--------------------|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|:------------|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27 00:00:00 |        10 | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                          |               9 |        4 | True        |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11 00:00:00 |        12 | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 |        5 | True        |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30 00:00:00 |         6 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 |        5 | False       |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12 00:00:00 |         7 | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 |        5 | False       |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06 00:00:00 |        17 | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 |        5 | False       |

### Univariate Analysis
Although we did single variable analysis on many columns, the one we’d like to highlight is this visualization we created for the chocolate column. It shows the number of recipes that do and do not contain chocolate. From this, we can see that while a majority of recipes do not contain chocolate, there is a large sample size (~5000 recipes) that do. This means that the data we analyze can be judged as fairly representative of recipes as a whole.

<iframe src="assets/UA2.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis
Below, you can see a plot for average rating by number of ingredients in a recipe, that is also accompanied by a boxplot for the number of ingredients. While this plot is only tangentially related to our overarching question, it serves to potentially highlight some trends regarding the perception/reception of complex recipes. Overall, most ingredient values had high average ratings, but it followed a downward trend until around 10 ingredients, at which point rating started to increase as ingredients increased. This could indicate that there was a threshold at which the number of ingredients signified rich complexity rather than unnecessary complication. Also, from the box plot, we can see that most recipes are between 5-15 ingredients.

<iframe src="assets/BA2.html" width=800 height=600 frameBorder=0></iframe>

### Interesting Aggregates
The interesting aggregate that we chose to look at was created by grouping by the chocolate column, and taking the mean of the resulting groups. As seen below, some interesting takeaways include the fact that recipes with chocolate tend to take slightly less time and fewer ingredients, but with more steps. Most related to our main question, however, is the fact that recipes with chocolate tend to have a higher, albeit very slightly higher, average rating.

|     id |   minutes |   contributor_id |   n_steps |   n_ingredients |   rating |
|-------:|----------:|-----------------:|----------:|----------------:|---------:|
| 381916 |  116.673  |      1.47963e+07 |   10.0049 |         9.24079 |  4.62467 |
| 373584 |   88.5087 |      1.89899e+07 |   11.7294 |         8.78158 |  4.63664 |

---
## Assessment of Missingness
### NMAR Analysis
In our dataset, the column 'description' has missing values. We believe this column is NMAR (Not Missing At Random) because it appears that missingness depends on the missing value itself. For example, it could be that the author of the recipe decided not to provide a description because the author may have been uploading their recipe on their phone and did not want to type out a long description. We could additionally obtain a "device type" column that would tell us what device the user uploaded their recipe on, which could possibly make 'description' Missing At Random (MAR).
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
After conducting our permutation test, we got a p-value of 0.11, which is greater than the significance value of 0.05 so we conclude that the missingness of 'rating' does not depend on 'n_ingredients'. 


Next, we analyzed 'rating' column's dependency of missingness on the column 'n_steps'.
Here is a histogram distribution plot showing the distribution of 'n_steps' when 'rating' is missing and when 'rating' is not missing. There are also box plots on the top showing the spread of the two.

<iframe src="assets/hist_n_steps.html" width=800 height=600 frameBorder=0></iframe>

You can notice that the distribution shapes are very similar but are slightly shifted. 
Here is also a kernel density estimate plot of the two distributions. 

<iframe src="assets/kde_n_steps.html" width=800 height=600 frameBorder=0></iframe>

Since the shapes are pretty similar but just shifted, we decided to use the absolute difference of means test statistic when conducting the permutation test. 
After conducting the permutation test, we got a p-value of 0.0.
We also did a permutation with the Kolmogorov-Smirnov test statistic since the location of the centers were very similar. For this, we got a p-value of 3.813369074131651e-13, which is extremely small and rounds to 0. 
Since the p-value is less than the significance level of 0.05, we conclude that the missingness of 'rating' does depend on the column 'n_steps'. 
Here is an empirical distribution of the absolute difference of means for this permutation test:

<iframe src="assets/fig.html" width=800 height=600 frameBorder=0></iframe>

The red line is the observed absolute difference of means, which you can see was pretty far from the rest of the simulated differences. 

---
## Hypothesis Testing
We chose to do a permutation test on this data set, in which we repeatedly shuffled the chocolate column to generate simulated statistics. 

Our Null Hypothesis was: The presence of chocolate in a recipe does not affect its rating. In other words, recipes without chocolate will have the same average rating as recipes with chocolate.
Our Alternative Hypothesis was: The presence of chocolate in a recipe will increase its rating.

The test statistic we chose to use was the difference in group rating means between recipes with and without chocolate. Our observed statistic was .01197. We chose to run the test at a .05 significance level and created 1000 simulated statistics.

After running the simulations, the resulting p-value was .116, which means that we would fail to reject the null hypothesis because there is a non-negligible change that the observed difference occurred by chance alone. This means that we cannot reject the null hypothesis, which also means we cannot claim that the presence of chocolate in a recipe would mean higher ratings. See below for a visualization of the results.

<iframe src="assets/test.html" width=800 height=600 frameBorder=0></iframe>
