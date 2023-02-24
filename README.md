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
Some of the initial data cleaning efforts took place before merging the two datasets together. We converted all the ratings in the interaction dataframe that were 0 to np.nan, which allowed us to ignore them in the calculations for the mean. 

Once we had a merged dataset, we had to make sure that all the columns were the correct types. For example, we had to convert the *submitted* column, which was originally a string, to datetime objects, which allowed us to make visualizations and analyses using that data. Many of the columns also started as strings which only looked like lists, rather than actually being lists of strings. To solve this, we split these strings and added the components to lists. This allowed us to actually access individual components of these lists. Interestingly, the *ingredients* column also had a similar problem, but because we only used it to check if chocolate was an ingredient, we did not convert it to a list. We instead searched the whole string for occurrences of the string “chocolate”, which allowed us to create the *chocolate* column in the data frame.

| name                                 |     id |   minutes |   contributor_id | submitted           | tags                                                                                                                                                                                                                                                                                                                  | nutrition                                                         |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                                                                             |   n_ingredients |   rating | chocolate   |
|:-------------------------------------|-------:|----------:|-----------------:|:--------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|:------------|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27 00:00:00 | ['60-minutes-or-less', ' time-to-make', ' course', ' main-ingredient', ' preparation', ' for-large-groups', ' desserts', ' lunch', ' snacks', ' cookies-and-brownies', ' chocolate', ' bar-cookies', ' brownies', ' number-of-servings']                                                                              | ['138.4', ' 10.0', ' 50.0', ' 3.0', ' 3.0', ' 19.0', ' 6.0']      |        10 | ['heat the oven to 350f and arrange the rack in the middle', ' line an 8-by-8-inch glass baking dish with aluminum foil', ' combine chocolate and butter in a medium saucepan and cook over medium-low heat ', ' stirring frequently ', ' until evenly melted', ' remove from heat and let cool to room temperature', ' combine eggs ', ' sugar ', ' cocoa powder ', ' vanilla extract ', ' espresso ', ' and salt in a large bowl and briefly stir until just evenly incorporated', ' add cooled chocolate and mix until uniform in color', ' add flour and stir until just incorporated', ' transfer batter to the prepared baking dish', ' bake until a tester inserted in the center of the brownies comes out clean ', ' about 25 to 30 minutes', ' remove from the oven and cool completely before cutting']                                                                                                                                                                                                                                                                                                                                                      | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                          |               9 |        4 | True        |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11 00:00:00 | ['60-minutes-or-less', ' time-to-make', ' cuisine', ' preparation', ' north-american', ' for-large-groups', ' canadian', ' british-columbian', ' number-of-servings']                                                                                                                                                 | ['595.1', ' 46.0', ' 211.0', ' 22.0', ' 13.0', ' 51.0', ' 26.0']  |        12 | ['pre-heat oven the 350 degrees f', ' in a mixing bowl ', ' sift together the flours and baking powder', ' set aside', ' in another mixing bowl ', ' blend together the sugars ', ' margarine ', ' and salt until light and fluffy', ' add the eggs ', ' water ', ' and vanilla to the margarine / sugar mixture and mix together until well combined', ' add in the flour mixture to the wet ingredients and blend until combined', ' scrape down the sides of the bowl and add the chocolate chips', ' mix until combined', ' scrape down the sides to the bowl again', ' using an ice cream scoop ', ' scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', ' bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', ' serve hot and enjoy !']                                                                                                                                                                                                                                                                                                      | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 |        5 | True        |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30 00:00:00 | ['60-minutes-or-less', ' time-to-make', ' course', ' main-ingredient', ' preparation', ' side-dishes', ' vegetables', ' easy', ' beginner-cook', ' broccoli']                                                                                                                                                         | ['194.8', ' 20.0', ' 6.0', ' 32.0', ' 22.0', ' 36.0', ' 3.0']     |         6 | ['preheat oven to 350 degrees', ' spray a 2 quart baking dish with cooking spray ', ' set aside', ' in a large bowl mix together broccoli ', ' soup ', ' one cup of cheese ', ' garlic powder ', ' pepper ', ' salt ', ' milk ', ' 1 cup of french onions ', ' and soy sauce', ' pour into baking dish ', ' sprinkle remaining cheese over top', ' bake for 25 minutes or until cheese is lightly browned', ' sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly ', ' about 10 more minutes']                                                                                                                                                                                                                                                                                                                                                 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 |        5 | False       |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12 00:00:00 | ['time-to-make', ' course', ' cuisine', ' preparation', ' occasion', ' north-american', ' desserts', ' american', ' southern-united-states', ' dinner-party', ' holiday-event', ' cakes', ' dietary', ' christmas', ' thanksgiving', ' low-sodium', ' low-in-something', ' taste-mood', ' sweet', ' 4-hours-or-less'] | ['878.3', ' 63.0', ' 326.0', ' 13.0', ' 20.0', ' 123.0', ' 39.0'] |         7 | ['freheat the oven to 300 degrees', ' grease a 10-inch tube pan with butter ', ' dust the bottom and sides with flour ', ' and set aside', ' in a large mixing bowl ', ' cream the butter and sugar with an electric mixer and add the eggs one at a time ', ' beating after each addition', ' alternately add the flour and milk ', ' stirring till the batter is smooth', ' add the two extracts and stir till well blended', ' scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean ', ' about 1 1 / 2 hours', ' cool the cake in the pan on a rack for 5 minutes ', ' then turn it out on the rack to cool completely']                                                                                                                                                                                                                                                                                                                                  | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 |        5 | False       |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06 00:00:00 | ['time-to-make', ' course', ' main-ingredient', ' preparation', ' main-dish', ' potatoes', ' vegetables', ' 4-hours-or-less', ' meatloaf', ' simply-potatoes2']                                                                                                                                                       | ['267.0', ' 30.0', ' 12.0', ' 12.0', ' 29.0', ' 48.0', ' 2.0']    |        17 | ['pan fry bacon ', ' and set aside on a paper towel to absorb excess grease', ' mince yellow onion ', ' red bell pepper ', ' and add to your mixing bowl', ' chop garlic and set aside', ' put 1tbsp olive oil into a saut pan ', ' along with chopped garlic ', ' teaspoons white pepper and a pinch of kosher salt', ' bring to a medium heat to sweat your garlic', ' preheat oven to 350f', ' coarsely chop your baby spinach add to your heated pan ', ' stir frequently for approximately 5 min to wilt', ' add your spinach to the mixing bowl', ' chop your now cooled bacon ', ' and add it to the mixing bowl', ' add your meatloaf mix to the bowl ', ' with one egg and mix till thoroughly combined', ' add your goat cheese ', ' one egg ', ' 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', ' transfer to a 9x5 meatloaf pan ', ' and cook for 60 min or until the internal temperature is at least 160f', ' let stand for 5min', ' melt 1tbsp unsalted butter into a frying pan ', ' and cook up to three eggs at a time', ' crack each egg into a separate dish ', ' in order to prevent egg shells from reaching the pan ', ' then add salt and pepper to taste', ' wait until the egg whites are firm looking ', ' but slightly runny on top before flipping your eggs', ' after flipping ', ' wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf'] | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 |        5 | False       |

### Univariate Analysis
Although we did single variable analysis on many columns, the one we’d like to highlight is this visualization we created for the chocolate column. It shows the number of recipes that do and do not contain chocolate. From this, we can see that while a majority of recipes do not contain chocolate, there is a large sample size (~5000 recipes) that do. This means that the data we analyze can be judged as fairly representative of recipes as a whole.

<iframe src="assets/UA2.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis
Below, you can see a plot for average rating by number of ingredients in a recipe, that is also accompanied by a boxplot for the number of ingredients. While this plot is only tangentially related to our overarching question, it serves to potentially highlight some trends regarding the perception/reception of complex recipes. Overall, most ingredient values had high average ratings, but it followed a downward trend until around 10 ingredients, at which point rating started to increase as ingredients increased. This could indicate that there was a threshold at which the number of ingredients signified rich complexity rather than unnecessary complication. Also, from the box plot, we can see that most recipes are between 5-15 ingredients.

<iframe src="assets/BA2.html" width=800 height=600 frameBorder=0></iframe>

### Interesting Aggregates
The interesting aggregate that we chose to look at was created by grouping by the chocolate column, and taking the mean of the resulting groups. As seen below, some interesting takeaways include the fact that recipes with chocolate tend to take slightly less time and fewer ingredients, but with more steps. Most related to our main question, however, is the fact that recipes with chocolate tend to have a higher, albeit very slightly higher, average rating.


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
We chose to do a permutation test on this data set, in which we repeatedly shuffled the chocolate column to generate simulated statistics. 

Our Null Hypothesis was: The presence of chocolate in a recipe does not affect its rating. In other words, recipes without chocolate will have the same average rating as recipes with chocolate.
Our Alternative Hypothesis was: The presence of chocolate in a recipe will increase its rating.

The test statistic we chose to use was the difference in group rating means between recipes with and without chocolate. Our observed statistic was .01197. We chose to run the test at a .05 significance level and created 1000 simulated statistics.

After running the simulations, the resulting p-value was .116, which means that we would fail to reject the null hypothesis because there is a non-negligible change that the observed difference occurred by chance alone. This means that we cannot reject the null hypothesis, which also means we cannot claim that the presence of chocolate in a recipe would mean higher ratings. See below for a visualization of the results.

<iframe src="assets/test.html" width=800 height=600 frameBorder=0></iframe>
