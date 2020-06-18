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
![Figure 1](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/08161862-91c6-44d1-afa0-14b1f235ab62.png)

###### Figure 2
![Figure 2](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/ec3e9fc2-410a-4ee1-95c8-092310ebabe5.png)

###### Figure 3
![Figure 1](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/08161862-91c6-44d1-afa0-14b1f235ab62.png)

###### Figure 4
![Figure 2](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/ec3e9fc2-410a-4ee1-95c8-092310ebabe5.png)

###### Figure 5
![Figure 1](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/08161862-91c6-44d1-afa0-14b1f235ab62.png)

###### Figure 6
![Figure 2](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/ec3e9fc2-410a-4ee1-95c8-092310ebabe5.png)

### Modelling and Predictions

By printing the feature importances, we see that by far the strongest predictor for global sales was North American sales. Features such as Platform, Year, Genre, and Publisher had next to no impact on the performance of the game in the market.
The Random Forest Regression model, however, with the following fields, was able to quite accurately predict the global sales based on the training set:

| Parameter     | Value         |
| ------------- |:-------------:|
| n_estimators  | 100           |
| max_depth     | 10            |
| n_jobs        | -1            |

###### Figure 7
![Figure 1](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/08161862-91c6-44d1-afa0-14b1f235ab62.png)

###### Figure 8
![Figure 2](https://github.com/JingwenCao/CEBD1261-FinalProject/blob/master/ec3e9fc2-410a-4ee1-95c8-092310ebabe5.png)

## Discussion
It's no wonder the North American market is such a coveted one in the video game industry based on the results of this study. The success of a game, regardless of its publisher, platform, genre, and year of release, is almost entirely dependent on its ability to sell in North America. However, this dataset is clearly quite biased, as it is comprised of video games that have already sold well historically. Thus, this may have been impacted by factors such as the prevalance of the video game industry in the respective countries (for example, video games have been prevalent mostly in the US and Japan, but did not start to build traction until much later in other countries). Additionally, some major platforms have been left out of the dataset, such as mobile platforms and VR/XR/AR, which are titans in the industry today, and could heavily skew the data in a different direction altogether.
