# Kickstarter_analysis
MAKING ADJUSTMENTS!

## Purpose
To develop a model that can predict the success or failure of a Kickstarter campaign using data downloaded from [here](https://www.icpsr.umich.edu/web/NADAC/studies/38050). If you want the data you will have to download it from here as it was too big for github and created errors in my version history.

## About the Data
Raw data has 21 features and ~507k instances in a tsv file. Data ranges from 2009 to 2020. There are missing values and incorrect classifications like some campaigns have Failed, but the Pledged amount equaled or exceeded the goal. 

## File guide
The raw unclean [data](https://www.icpsr.umich.edu/web/NADAC/studies/38050) was too large to upload so I omitted it, but provided the link for you to download if you wish. the Db I created was also too large to load to githib unfortunately.

## Process

### Data Cleaning Formatting
First step was to clean and format the data. I made the feature names more concise and properly formatted (title case). I dealt with missing values in various columns. Missing values in Backers (#) were dealt with using median imputation provided they were Successful (Pledge > Goal). Location related features were a mess - apparently there are 21,000 countries... - so I used the Project currency feature to map Project Country values. I removed City and State all together as it was too messy. I also formatted monetary values by removing regular expressions. I also formatted values in the Status feature. I changed data types for select features as I loaded the data in string format for ease. I checked for logic of the Status feature - are they properly classified? My definition of Successful here was **Successful campaigns are where Goal >= Pledged**. The raw cleaned data was exported to a sqlite db that I queried to get my data going forward.

#### Abount the DB
The database has four tables: Campaigns, Categories, Subcategories, and Countries. Stay tuned for the schema



### Exploratory Data Analysis
Performed EDA here and made some changes to the data. I extracted Month and Year from Launched and Deadline data. I consolidated European countries and Europe and the European Union as the European countries had a choice of currency. I also changed the Status feature values from four to two - Successful and Failed. The US accounted for 73% of my countries which mmakes sense given Kickstarter is US based. The numerical features took a lot of time to explore as two were countinous while the other two were discrete. I explored log transformation, binning, Yeo-Johnson, and Quantile Transformer.



### Modelling
I explored three models for Binary Classification (predicting Success or Failed). I explored Logistic Regression, Random Forest Classifier, and XGBoost Classifier. I also performed a base model for each consisting of Standard Scaler and the desired model and added features selection and PCA at each step to compare model performance. Kbest and PCA suggested three components for the optimal model.


## Results
- The United States accounted for 73% of the data on I focused soley on this
- Logistic Regression with PCA (3 components) yielded the best model with 88% accuracy and a lower Log loss value on the test data. 
- The Random Forest Classifier and XGBoost classifier were highly prone to over fitting even with pca

## Challenges
- Rabbit holes - Curiosity is good, but evenutally I'm just chasing my own tail
- I think I got over zealous on feature engineering and hurt my model. I should do the base data then slowly add features
- notebook orgainzation!!!! I need to tidy up my work. I am going to revisit my projects over the coming weeks

## Future Goals
- Notebook organization,
- practice more. I'd like to do a project once a week or once every two weeks,


# Kickstarter_Analysis
