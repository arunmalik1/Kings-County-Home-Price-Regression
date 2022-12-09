Kings County Real Estate Project 
by Arun Malik

## Project Overview

Create a multiple linear regression model to analyze home sales in Seattle and the surrounding area.

## Business Problem

A/B real estate company is the stakeholder for this project. Their mission is to help people buy and sell homes in Seattle, by providing advice on what renovations homeowners should focus on to increase property value.

## The Data 

The data can be found on kaggle with the following link:
https://www.kaggle.com/datasets/shivachandel/kc-house-data

It was provided to us by the Flatrion School in NYC

## Data Cleaning Process

The first step in cleaning the data was to look for null values. The most missing values were in the waterfront and yr_renovated columns. I decided to replace the null values with 0's because I didn't want to lose too much data.

## Feature Transformation

Machine learning requires data to be in 0's and 1's, so all the categorical and ordinal variables have to be transformed. Waterfront is a yes/no categorical variable and required a simple transformation.

View, condition and grade are features that have order. I chose the Python mapping technique to transform their values keeping in mind to retain their classification in tact.

## Feature analysis and visualization

I wanted to see what features had the highest correlation to price. A correlation heatmap shows that the the top three features are sqft of living space, the grade of the property and sqft of above space(space that does not count the basement of the property).







Price is rightly skewed and I didn't want to delete the outliers because I wanted to keep as much of the data as possible. So, I took the log of price to make the distribution more normal.










Since sqft of living and grade had the highest correlation, I created a plot to display all 3 features. As expected, increasing the sqft of a property increases the price. If you look at a house with similar square footage, the house with higher grade value is much more expenive.












Grade has an exponential effect on price. Therefore, a property owner should focus on inceasing the grade of their property.




I made charts to display their relationship to price and to me the most interesting to me was bedrooms. Adding more then eight bedrooms negatively affected prices. I am inferring this is due to a reduction in square foot living.





Zipcode is a big factor in determining the price of a home, so I wanted to display the zipcodes with the highest average price.






Houses near a waterfront have far higher prices, again not surprising.






## Regression Model building

For model number 3 

I built a total of 3 models for this project. The first model used the features with the top ten correlated features and the resulting R^2 was 78.49. In order to get an accurate prediction, I had to standardize the data. This is a crucial step because otherwise grade which has values from 0 to 5, would get overpowered by features such as sqft which are in the 1000's.

The coeffients for sqft_living was $142.00 and grade was $49,993. So this model is telling us that for every one unit increase in sqft_living, price will increase by $142.00



## Model 2
I only used sqft_living and zipcodes for this model because I wanted to see the effect of these two features on price. The R^2 of this model was only 73.47% and the affect of zipcode is difficult to understand because the model is taking in all zipcodes in Seattle.




## Model 3, the final model

The final model had all the features available in the data set. It resulted with a R^2 of 0.875, meaning that the model has a 87.5% accuracy level. Coefficients of sqft_living and grade were $132.00 and $58,882.








