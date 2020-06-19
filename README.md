# CEBD1261-FinalProject

*To run the code:*

*1. Import the vgsales.csv file in Databricks*

*2. Import the .html worksheet in Databricks*

*3. Attach the worksheet to a running cluster with the mlflow library installed*

*4. Run the worksheet*

## Research Question

What interesting trends emerge from the data, and how accurately can we predict video games sales using Random Forest Regression?

## Introduction

The dataset, from Kaggle, consists of a list of video games with sales greater than 100,000 copies, which was scraped from vgchartz.com. Each record included a rank (relative to overall sales), the name of the game, the platform of the games release, the year of release, the genre of the game, the publisher of the game, and its sales in millions in North America, Europe, Japan, Other (the rest of the world), as well as globally. The analysis was conducted using spark, SQL, and python, particularly the following libraries: Sklearn, Matplotlib, Numpy, Seaborne and Pandas. The following report will go over the exploratory data analysis, as well as the predictive modelling done with the Random Forest Regression mdoel.

## Methods
### EDA and Feature Correlation
The dataset was loaded into a spark table and subsequently cleaned. The Platform, Genre and Publisher fields were transformed into categorical data distribution (integer) through label encoding in order to calculate correlation matrix. Exploratory data analysis was done using SQL qureires, and visualized using the default Databricks display. Finally, Seaborn was used to create a correlation matrix to assess the correaltion of the features of the dataset.

### Modelling and Predictions
Following some exploratory data analysis using SQL in Databricks, the data was loaded into a Pandas dataframe for modelling and prediction. NaN values were handled for the Publisher field by dropping the rows with null values, and for the Year row by replacing the values with the median. The Name and Rank fields were dropped, as they did not add accuracy to the predictions. Lastly, the categorical fields Publisher, Platform, and Genre fields were label encoded. Some optimization was done by the way of converting all fields to a float16 type. The data was then split into features and target, and split again into test and train sets. Finally, the Random Forest Regression was fitted with this data, over 5 k-folds. 

## Results
### EDA and Feature Correlation

###### Figure 1
![Figure 1](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/Figures/Figure_1.png)

Here we plot Global Sales versus Year by using series grouping (sum) in Genre. This plot demonstrates how each category in Genre performs in terms of total Global Sales per year. From 1980 to 2010, almost all Genre categories show increasing Global Sales trend especially Action, Sports, Shooter and Misc. This plot also help us to understand how market volume increases in time. On the other hand, there is dramatic drop of Global Sales after 2014, which is probably due to lack of provided dataset after 2014. Amount of data provided for 2014 and after corresponds to only 10% of whole data.

###### Figure 2
![Figure 2](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/Figures/Figure_2.png)

We select first 20 games having the highest global sales and create a bar plot to visualize their sale rates by grouping them with respect to different markets. Market is dominated especially by the NA sales. This plot also demonstrates how regions can have different interest on gaming.

###### Figure 3
![Figure 1](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/Figures/Figure_3.png)

It is pretty clear that Nintendo dominates the market between the years of 1980 and 2017. They share 63% of the total global sales of top 100 games. Activision follows Nintendo as second with its share of 11%, Take-two as third. This pie chart verifies that Nintendo, thanks to its product Wii, has very high global sales and therefore owns the majority of the market share.

###### Figure 4
![Figure 2](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/Figures/Figure_4.png)

It is pretty clear that Nintendo dominates the market between the years of 1980 and 2017. They share 63% of the total global sales of top 100 games. Activision follows Nintendo as second with its share of 11%, Take-two as third. This pie chart verifies that Nintendo, thanks to its product Wii, has very high global sales and therefore owns the majority of the market share.

###### Figure 5
![Figure 1](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/Figures/Figure_5.png)

We classify Games with respect to their Year, labeled as OLD if it is released before 2007 and as NEW for 2007 and after. We determined 2007 as the Year in order to provide almost equal separation to provide balance. This bar plot indicates that NEW games have more total global sales than OLD games while OLD games have higher average global sales than the NEW ones.

###### Figure 6
![Figure 2](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/Figures/heatmap.png)

 Among them, NA and EU sales have very high correlation with global sales such as 0.94 and 0.9 respectively. This verifies our initial observation in Figure 2 about the dominancy of NA and Europe in the market. NA and EU sales almost determine the global sale. However, JP has significantly less correlation with all NA, EU and Global sales. This indicates and verifies again our previous observation that JP market favours different type of games like Role Playing - Pokemon compared to others. On the other hand, Platform, Genre and Publisher show no correlation between each other and sales. Having no particular pattern between these features and sales make sense because there are many outliers having enormous sale values like Wii Sports, Tetris, Super Mario, etc. with irregular Year pattern. One can even guess next hit will belong to Nintendo due to the fact that 63% of top 100 games belongs to it, but nevertheless average games seem drops this correlation.

### Modelling and Predictions

By printing the feature importances, we see that by far the strongest predictor for global sales was North American sales. Features such as Platform, Year, Genre, and Publisher had next to no impact on the performance of the game in the market.
The Random Forest Regression model, however, with the following fields, was able to quite accurately predict the global sales based on the training set:

| Parameter     | Value         |
| ------------- |:-------------:|
| n_estimators  | 100           |
| max_depth     | 10            |
| n_jobs        | -1            |

###### Figure 7
![Figure 1](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/Figures/FeatureImportance.png)

###### Figure 8
![Figure 2](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/Figures/AccuracyofModel.png)

## Discussion
It's no wonder the North American market is such a coveted one in the video game industry based on the results of this study. The success of a game, regardless of its publisher, platform, genre, and year of release, is almost entirely dependent on its ability to sell in North America. However, this dataset is clearly quite biased, as it is comprised of video games that have already sold well historically. Thus, this may have been impacted by factors such as the prevalance of the video game industry in the respective countries (for example, video games have been prevalent mostly in the US and Japan, but did not start to build traction until much later in other countries). Additionally, some major platforms have been left out of the dataset, such as mobile platforms and VR/XR/AR, which are titans in the industry today, and could heavily skew the data in a different direction altogether.
