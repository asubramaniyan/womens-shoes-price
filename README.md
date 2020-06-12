**Prediction of women's shoe price**

**Objective:** To predict the average price of women's shoes based on the brand, model, size, color and the merchant

**Performance metric used:** Mean squared error and mean absolute error

**Model Results:** The data was fitted via linear regression with L2 regularization. The Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE) of the fitted model is 0.09 and 0.07 respectively.

**Approach:**

The data was split into train and test (70:30) and the train data was analyzed. 

**Feature Extraction:**
The following features were removed:

Feature | Removal reason|
--- | --- |
prices.returnPolicy	| All missing values
asins |	Only 2 non-null values
prices.currency	|	0 variance
primaryCategories	|	After data cleaning, zero variance
categories	|	Redundant information
dateAdded, dateUpdated, prices.dateAdded, prices.dateSeen	|	These indicate the dates the record or its price were added or updated in the source database where this data was collected
prices.amountMax and prices.amountMin	|	A new column named average price was created and these prices were moved
colors	|	The price of a shoe can vary with color. The specific color of the shoe is specified by another feature prices.color. This is redundant information
prices.sourceURLs	|	Name of the e-commerce site is added to the feature named ‘prices.merchant’ from this field
sourceURLs	|	Link from where this product is obtained. Captured in prices.merchant
imageURLs	|	Picture of shoe. Not required for price prediction
manufacturer	|	Features manufacturer and brand are the same. Feature brand is retained and this will be dropped
manufacturerNumber |	Features manufacturerNumber and name are the same. Feature name is retained and this will be dropped
Sizes	|	This feature lists all the sizes made by manufacturer. There is another feature named prices.size, where provides the specific size of the shoe for the given price
upc	|	These are unique barcode number specific to product. More than one upc for an observation indicates the variation of the product. Let us remove it for now.
keys	|	These are keys for data infiniti internal usage and not relevant for shoe price
prices.shipping, weight, prices.availability, dimension, prices.condition, prices.offer, prices.isSale |	>90% of the data missing
Id	|	There is 1:1 correlation between id and name feature. Name represents the model name of the shoes. Thus, this feature does not provide any new information
Brand	|	There is 1:1 correlation between brand and name feature. Name represents the model name of the shoes. Thus, this feature does not provide any new information

The dataset is reduced from 47 to 4 features. The retained features are: name (brand and model name), color, merchant and size. All of the 4 features are categorical in nature. 

**Feature Engineering of size feature:** The size of the shoe is represented in different units: US and UK size, Europe size, mens and women’s size
  - Men’s sizes and UK sizes were removed
  - Europe to US size information was scraped from wikipedia and used to convert size in Europe unit to US.

All four categorical variables were one-hot encoded and the final number of features is 1163

