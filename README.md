# Ames Housing Data Analysis
---

## Introduction
&ensp;&ensp;&ensp;&ensp;Location, Location, Location. Is that really what is most important in real estate? Is that all that is important? With the Ames housing dataset other than building an effective predictive model we aim to find out which of our features most and least affect prices.

Our goal is to find any significant correlations and insights in the relationship between our respective housing features and what price a given real estate property is valued. In this analysis we will be manipulating two data sets: One training set of Ames housing data from 2007 - 2010 and another smaller dataset to test our model. This second set simply has the actual price feature removed so that we can work to form it from our trained model. 


## Problem Statement
**Which key features in the Ames Housing data most affect housing prices?** 

#### *Questions to Explore*:
- Which features are most important in increasing price?
- Which features are least important in increasing price?
- Are any features completely irrelevant to price on average?
<br><br>
---
## The Data
Two sets of data were used:

- [Ames Training Dataset]('data/train.csv')
- [Ames Testing Dataset]('data/test.csv')


#### Ames Housing Dataset Feature Dictionary

There are 80 differnet features in this set so to best understand them here we include a link to a thurough breakdown:

- [Ames Feature Data Dictionary](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt)


#### Data Cleaning 

Large amount of work to be done in this dataset - almost 3000 total entry rows and many missing values across many features that need to be handled. Here is a great visualizatino of the missing values:

![Missing Values](Visuals/missing_vals.png)

#### Data Cleaning Overview

- Missing categorical values were labeled as 'missing'
- Numerical but non continuous nulls were filled with their respective medians as much of the features had a skewed distribution so the median was a better representation of center. There was also a new binary column made for each numerical column initially having nans to serve as a memory of which were initialy nulls incase this information was ever needed later on.
- Year features were converted from the calendar year into how many years differnce the features had from Sale year. 
- Conintuous skewed numeric columns with values above zero were log transformed and the rest without negatives were root transformed for normality.
- Only a couple of outliers of wildly high living area and low price were removed as considered safe.


---

## Key Insights and Visualizations
--- 
Our Most Important model metric was a cross val R2 score of **0.921**

Here is the distribution of the models residuals which show a decently normal distribution:
![Model Residuals Distribution](Visuals/residual_distribution.png)
Here are the residuals plotted against the predictions to check variance schedasticity which turned out very well and rather homoschedastic.
![Model residuals vs predictions](Visuals/residual_predictions.png)
Here are the top 20 coefficients found from the model, they are represented in logarithmic form as the target variable was initially skewed so this wsa done to improve performace:
![top 20 coefficients](Visuals/top_20.png)
Here are the top 20 correlations to Sale Price found in exploratory data analysis to take into account along with the coefficients found:
![top 20 base correlations](Visuals/corr_heatmap_top20.png)


## Conclusion
While we do now have a rather great and trustworthy model for house price predictions the complexity of the model has made intuition gathering about the features rather difficult. If the priority of the clients in this situation was to receive accurate predictions this would be a big win however if the priority was to gather insights about the independent variables then reducing the model to a simpler version would be the next steps!

We did still find some useful crossover insights between the simple feature to price correlation rankings and the top coefficients ascertained by the model. Here are a 5 which were in the top level of both rankings:
- Kitchen Quality
- Above Grade Living Area
- Garage Quality (Size and Cars)
- Lot Area
- Masonry Veneer (Area, type)

Moving forward, as always, more data would allow us a more comprehensive and accurate model. This would be in terms of either desired priority be it better intuition or better predictions! 
