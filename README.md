# ☕ Brewing better coffee with data
This repository contains analysis of data from the coffee quality institute taken from this Kaggle dataset: https://www.kaggle.com/ankurchavda/coffee-beans-reviews-by-coffee-quality-institute.

>Kudos to @jldbc, who initially scraped and cleaned the data:
>https://github.com/jldbc/coffee-quality-database


## Idea / Motivation

As a coffee loving developer and enthusiastic coffee brewer and drinker, I wondered whether there was something interesting to find in data of qualified Q-graders tasting coffee.

Leading questions were:

1. What patterns can we find in coffee tasting data?
1. Can we predict coffe tasting results based on meta data about the bean?
1. How relatable will the results be to our daily coffee drinking experience and purchase decisions?
## Data cleaning
Eventhough the data was precleaned already, upon first review of the data I stumbled over some strange things which needed adjustment. In the end I had 43 features with 874 usable data samples. Some of the features contained less, but I did not use those for my investigations.

### General
1. Removal of unimportant features like: Farm name, Lot Number, Producer, Owner, ...
1. Selection of only Arabica samples (low count of Robusta samples + very different beans)
1. Removal of NaN, empty and zero values
### Altitude
During inspection of the mean altitudes (m), I spotted a weird value of  190164.0, which would be somewhere in space. After a quick Google search of the altitudes in the country of origin, I figured that the measurement must be in centimeters instead of meters. I found a few more which seemed to be done in decimeters. Obviously I corrected these values and afterwards got a new maximum of 4287.0m, which looked better to me.
### Total weight
As we were not given a total weight feature but Bag weight and bag count, I thought I would simply calculate the total weight myself. However I quickly spotted that the values of bag count were not numerical and included both kilogram and pound measurement. So I had to transform pounds to kilograms first and afterwards was able to calculate a new feature with the total weight.
However, looking at a histogram of the data I spotted a unreasonably large range with huge outliers, which was the reason why I decided to exclude those.
### Color
The color one was rather simple, as the only thing were "None" entries instead of blank or NaN values in some samples. They could be easily excluded.

## Data analysis
After cleaning the data, I wanted to closer inspect it and possibly train some machine learning models to predict cupping results of future samples.

### Correlation hunting
I began by looking around for correlation between the total cup points or individual cupping metrics in the data. To do that I calculated the Pearson and Spearman coefficient for continous features and did scatter plots to inspect the data visually. For categorical features, I did one-hot encoding and tried to fit regression models. If I would have succeeded in fitting a regression model to the data predicting the cupping result one could assume that the two features are correlated.
Sadly I didn't find any strong relation between the individual features and the cupping results.
### Regression
To make it short: I tried various regression models with grid search for hyper parameter tuning, but all of them performed really bad and I quickly stopped investigating.
### Classification
After splitting the total cup scores into multiple classes, I applied k nearest neighbors and support vector classification and initially got solid results. However after looking a little closer I had to realize that this was due to skewness of the data and the models just classfying every sample the same.
After performing under and oversampling the results looked better however with slight decreases in overall accuracy. The low sample size now really was a problem and more data would probably have helped.

## Conclusions
Predicting coffee quality and tasting results based on metadata is not feasible. Especially not for everyday purchase decisions.

Besides all the data analysis, please keep supporting your local roasters, try to buy fair traded coffee and do the maths. One kilogram of coffee for less than 10€ cannot be profitable for any farmer.

So to sum all the research up: Buy whatever suits your taste and keep enjoying good coffee!