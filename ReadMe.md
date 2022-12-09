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

![Corr Plot](https://user-images.githubusercontent.com/115169255/206781732-5cb61c94-4cf0-4cc3-8e7d-abf73364b0dd.png)

Price is rightly skewed and I didn't want to delete the outliers because I wanted to keep as much of the data as possible. So, I took the log of price to make the distribution more normal. Since sqft of living and grade had the highest correlation, I created a plots to display them. As expected, increasing the sqft of a property increases the price. If you look at a house with similar square footage, the house with higher grade value is much more expenive.


![SqftPlot](https://user-images.githubusercontent.com/115169255/206782054-9c0bf41e-1cf9-4c55-9d34-87b07326a6b9.png)



Grade has an exponential effect on price. Therefore, a property owner should focus on inceasing the grade of their property.

![Grade](https://user-images.githubusercontent.com/115169255/206782105-c49deec8-4822-4a33-8bf9-8ba03225b6fd.png)


I made charts to display their relationship to price and to me the most interesting to me was bedrooms. Adding more then eight bedrooms negatively affected prices. I am inferring this is due to a reduction in square foot living.


![Bedrooms](https://user-images.githubusercontent.com/115169255/206782509-9d0c0172-cc79-48b6-bb97-f04fae51987b.png)


Zipcode is a big factor in determining the price of a home, so I wanted to display the zipcodes with the highest average price.


![top10zipcodes](https://user-images.githubusercontent.com/115169255/206782538-680aae56-7195-4890-8479-6b995d802f15.png)


Houses near a waterfront have far higher prices, again not surprising.

![waterfront](https://user-images.githubusercontent.com/115169255/206782646-ca8d1ea1-e812-4963-a21c-5e6f9cd046cf.png)


## Regression Model building

I built a total of 3 models for this project. The first model used the features with the top ten correlated features and the resulting R^2 was 78.49. In order to get an accurate prediction, I had to standardize the data. This is a crucial step because otherwise grade which has values from 0 to 5, would get overpowered by features such as sqft which are in the 1000's.

The coeffients for sqft_living was $142.00 and grade was $49,993. So this model is telling us that for every one unit increase in sqft_living, price will increase by $142.00

print(model_high_corr.intercept_, model_high_corr.score(X_test, y_test))
results = pd.DataFrame(zip(X.columns, model_high_corr.coef_))
58592625769471.2 0.7813683750761602

sqft_living	1.423010e+02
grade	4.999392e+04
sqft_above	8.228229e+01
sqft_living15	4.334325e+00
bathrooms	1.088235e+04
view	8.797149e+04
bedrooms	-3.115914e+04
waterfront	4.884088e+04
floors	-6.281676e+04
zipcode	-5.859263e+13

## Model 2
I only used sqft_living and zipcodes for this model because I wanted to see the effect of these two features on price. The R^2 of this model was only 73.47% and the affect of zipcode is difficult to understand because the model is taking in all zipcodes in Seattle.

print(model_zipcode_living.intercept_, model_zipcode_living.score(X_test, y_test))
pd.DataFrame(zip(X.columns, model_zipcode_living.coef_))
-23359341672402.906 0.7347760577528235

sqft_living	2.501074e+02
zipcode	2.335934e+13

## Model 3, the final model

The final model had all the features available in the data set. It resulted with a R^2 of 0.875, meaning that the model has a 87.5% accuracy level. Coefficients of sqft_living and grade were $132.00 and $58,882.

print(model_all_features.intercept_,  model_all_features.score(X_test, y_test))
results = pd.DataFrame(zip(X.columns, model_all_features.coef_))

sqft_living	1.423010e+02
grade	4.999392e+04
sqft_above	8.228229e+01
sqft_living15	4.334325e+00
bathrooms	1.088235e+04
view	8.797149e+04
bedrooms	-3.115914e+04
waterfront	4.884088e+04
floors	-6.281676e+04
zipcode	-5.859263e+13




