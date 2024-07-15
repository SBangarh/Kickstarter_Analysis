# Kickstarter_analysis
MAKING ADJUSTMENTS!

## Purpose
To develop a model that can predict the success or failure of a Kickstarter campaign using data downloaded from [here](https://www.icpsr.umich.edu/web/NADAC/studies/38050). If you want the data you will have to download it from here as it was too big for github and created errors in my version history.

## Business Case
Kickstarter is a [Public Benefit Corporation](https://www.kickstarter.com/about?ref=global-footer) and donates 5% of after tax profits to public causes like fighting systemic inequality. My goal with this project was to be able to predict the success of a project with limited input as a proof of concept. By being able to predict the success of a campaign, Kickstarter would be better able to forecast revenue, budget, and ultimately donate more to public causes as their revenue is derived as a percentage of the total pledged amount for successful projects. This data was limited and did not include potential features like social media metrics for creators, but this is a good stepping stone to show potential and improve the model.

## About the Data
Raw data has 21 features and ~507k instances in a tsv file. Data ranges from 2009 to 2020. There are missing values and incorrect classifications like some campaigns have Failed, but the Pledged amount equaled or exceeded the goal. 

## File guide
The raw unclean [data](https://www.icpsr.umich.edu/web/NADAC/studies/38050) was too large to upload so I omitted it, but provided the link for you to download if you wish. the database I created was also too large to load to githib unfortunately.

## Process

### Data Cleaning Formatting
First step was to clean and format the data. I made the feature names more concise and properly formatted (title case). I dealt with missing values in various columns. Missing values in Backers (#) were dealt with using median imputation provided they were Successful (Pledge > Goal). Location related features were a mess - apparently there are 21,000 countries... - so I used the Project currency feature to map Project Country values. I removed City and State all together as it was too messy. I also formatted monetary values by removing regular expressions. I also formatted values in the Status feature. I changed data types for select features as I loaded the data in string format for ease. I checked for logic of the Status feature - are they properly classified? My definition of Successful here was **Successful campaigns are where Goal >= Pledged**. The raw cleaned data was exported to a sqlite db that I queried to get my data going forward.

#### Abount the DB
The database has four tables: Campaigns, Categories, Subcategories, and Countries. Stay tuned for the schema

### Exploratory Data Analysis
Performed EDA here and made some changes to the data. I extracted Month and Year from Launched and Deadline data. I consolidated European countries and Europe and the European Union as the European countries had a choice of currency. I also changed the Status feature values from four to two - Successful and Failed. The US accounted for 73% of my countries which mmakes sense given Kickstarter is US based. The numerical features took a lot of time to explore as two were countinous while the other two were discrete. I explored log transformation, binning, Yeo-Johnson, square root, and Quantile Transformer. Some features required two transformations. I also performed some statistical tests in relation to the target variable (Status).

### Modelling
I explored three models for Binary Classification (predicting Success or Failed). I explored Logistic Regression just as a starting point. My base model was the raw data for the numerical features only. I omitted the categorical data as encoding would lead to a dimensionality curse. I then passed the transformed data to the model. Prior to evaluating the model, I used cross validation to determine how my model would react to unseen data in both cases. If the scores were "acceptable" - above 70%, I proceeded with the model.


## Results
- The USA accounted for 73% of my data and given Kickstarter is an American company I focused on the Campaigns specific to the US.
- The cross validation scores for the raw data ranged from 0.86 to less than 0.88, but applying the applicable transformation it increased to in between 0.98 and 0.99
- Logistic Regression with the transformed data yielded a model with a 0.99% accuracy and a balanced accuracy score of 0.9896 on the training data and 0.9887 on the test data





