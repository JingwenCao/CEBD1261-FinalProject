# CEBD1261-FinalProject

README file (report)briefly summarizing the results obtained, explaining in 1-5 lines how toreproduce the results using the developed code, and reporting a few linesof conclusions

## EDA and Feature Correlation

## Modelling and Predictions
### Research Question

How accurately can we predict video games sales using Random Forest Regression?

#### Introduction

Based on field research, Random Forest Regression has unanimously emerged as the most accurate prediction model for global video game sales based on the data scraped from vgchartz.com (A list of video games with sales greater than 100,000 copies). Each record included a rank (relative to overall sales), the name of the game, the platform of the games release, the year of release, the genre of the game, the publisher of the game, and its sales in millions in North America, Europe, Japan, Other (the rest of the world), as well as globally. The analysis was conducted using the following libraries: SKlearn, Matplotlib, Numpy, and Pandas. The figures below represent the feature importance of the fields, as well as the performance of the selected model.

#### Methods

Following some exploratory data analysis using SQL in Databricks, the data was loaded into a Pandas dataframe for modelling and prediction. NaN values were handled for the Publisher field by dropping the rows with null values, and for the Year row by replacing the values with the median. The Name and Rank fields were dropped, as they did not add accuracy to the predictions. Lastly, the categorical fields Publisher, Platform, and Genre fields were label encoded. Some optimization was done by the way of converting all fields to a float16 type. The data was then split into features and target, and split again into test and train sets. Finally, the Random Forest Regression was fitted with this data, over 5 k-folds. 


#### Results

By printing the feature importances, we see that by far the strongest predictor for global sales was North American sales. Features such as Platform, Year, Genre, and Publisher had next to no impact on the performance of the game in the market.
The Random Forest Regression model, however, with the following fields, was able to quite accurately predict the global sales based on the training set:

| Parameter     | Value         |
| ------------- |:-------------:|
| n_estimators  | 100           |
| max_depth     | 10            |
| n_jobs        | -1            |

###### Figure 1
![Figure 1](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/08161862-91c6-44d1-afa0-14b1f235ab62.png)

###### Figure 2
![Figure 2](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/ec3e9fc2-410a-4ee1-95c8-092310ebabe5.png)

#### Discussion
It's no wonder the North American market is such a coveted one in the video game industry based on the results of this study. The success of a game, regardless of its publisher, platform, genre, and year of release, is almost entirely dependent on its ability to sell in North America. However, this dataset is clearly quite biased, as it is comprised of video games that have already sold well historically. Thus, this may have been impacted by factors such as the prevalance of the video game industry in the respective countries (for example, video games have been prevalent mostly in the US and Japan, but did not start to build traction until much later in other countries). Additionally, some major platforms have been left out of the dataset, such as mobile platforms and VR/XR/AR, which are titans in the industry today, and could heavily skew the data in a different direction altogether.
