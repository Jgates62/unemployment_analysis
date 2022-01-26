
## Project_5
#### van Possum group - Jordan Gates, Joomart Achekeev, Brian Kim

[Executive Summary](./exec_summary.md)

### Intro
Given a wide selection of topics to work on for the project 5, van Possum group (Joomart, Jordan and Brian) has selected the vital issue of unemployment. In an attempt to model a real life project the group members have decided to ignore the available datasets and collect raw, uneddited and uncleaned data from numerous sources. The collected data included maximum information possible on such topics as numer of police per capita, number of enterprises per capita, population breakdown per capita and other related topics. The data was collected by US county for 2010, excluding the 2008 presidential election results, that have been used to derive the democrat/republican percentage of local population.

We set a very optimistic goal before actually touching the project to determine if it is possible to predict unemployment rate depending on the certain characteristics of a standalone county.

The project problem statement is as follows: What factors correlate with the unemployment and can they be used to predict the unemployment rate in a random US county? 

And as a consequence, by tweaking these factors would it be possible to influence the unemployment rate?

##### (parts of the readme are in the exact order how the python codebooks are to be executed)

### Used tools and Python libraries

First code notebook, “01_Data_load_and_cleaning.ipynb” used libraries such as pandas and numpy for bringing in data and changing the types of the columns.
The Second code notebook, “02_EDA.ipynb”, required pandas, numpy, seaborn, and matplotlib to bring in data and graphing the outcomes of our findings. 
Third notebook, “03_Preprocessing_and_Feature_engineering.ipynb”, used more libraries because it required us to train test split. Along with pandas, numpy, and matplotlib, we brought in various sklearn imports to perform initial imports. In sklearn imports, there were LinearRegression, StandardScalar, PolynomialFeatures, train_test_split, cross_val_score and predict, Pipeline, GridSearchCV and PCA for our feature modeling. Using these, we were able to break down our data, scale it and analyze how our model performed with different data.
Last notebook, “04_Modeling.ipynb”, we had the same imports as above in addition to the Tensorflow, keras libraries. With these, we performed neural network predictions to make our already existing model better. Through all the research, we were able to product a feasible model for our data. 

### 01 Data loading and cleaning

Due to the fact that the data was extracted from various sources, around 4.2% of the data was corrupted and was eveluated as impossible to use in the modeling, this data was dropped. Other values have been imputed with average statewide data since the rows where they were located contained other important information that would help our models learn important dependencies. The final dataset prepared for futher processing has 28 columns of which 3 are location data (state, county, population) and 1 is the target data - unemployment.

##### Main Data Sources:

US Census (www.census.gov):
 - economic data
 - population data
 - unemployment data
USDA (www.nass.usda.gov):
 - rural/urban population data
Harvard University (www.dataverse.harvard.edu):
 - elections data
FBI (ucr.fbi.gov)
 - police data
 - crimes data



### 02 EDA
During our data exploration, we were able to visually show what our findings looked like. For example, we first looked at the correlation of the whole data. With this, we were able to tell, which columns might have more impact towards our target variable ‘unemployment_rate_2010’. There are a few graphs that we took a look at in more detail. 

A few scatter plots in this notebook show how the Democratic votes in 2008 graphed generally in a positive trend while Republican votes graphed in a negative trend. We have also graphed the relationship between population in different counties and the unemployment rate. But, in general, it did not give sufficient evidence that population has much to do with unemployment rate. Same goes for the crimes per capita and unemployment rate. 

One surprising insight we found was how many liquor stores per 10,000 people were in counties with the lowest and highest unemployment rates. The number of liquor stores per 10,000 people in counties with unemployment rate less than 5% was 2.06 liquor stores per 10,000. While counties with unemployment rate more than 15% had 0.78 liquor stores per 10,000 people. Now of course we can't say that one definitely caused the other, (Correlation does not imply causation) but it is interesting nonetheless.

### 03 Preprocessing and Feature Engineering

This is the part where it got challenging and interesting. The original data showed low scores (train: 0.4299, test: 0.3938, cross_val: 0.3593) while the fully polynomial transformed dataset showed extreme variance with over 600 columns. This is where the team had an idea to create grid search analog for the linear model in terms of correlation percentages of the numeric columns (see codebook 03 for more details). 

The model had nested double loop with sufficient code inside and took some time to run but yielded better scores with indication of which column interaction will return better results in the linear regression model.

The final dataset with certain data interaction had 101 columns and was saveed for future use in the modeling step. 

### 04 Modeling
The modeling process was faster then the previous steps where the team decided to compare the basic Linear Regression and Neural Network Performance. Even though the amount of data was limited by 3015 rows, neural network performed significantly better.
    The Linear Regression model returned Test R2 score: 0.4836, Cross_val 0.4572
    The Neural Network model returned Test R2 score: 0.6344
Even though there where other models such as Linear regression on the original not preprocessed dataset, and linear regression on PCA tuned dataset, they were not used to train second level model because of their poor performance.

Second level Linear Regression model was hand fed train test split predictions from first level models and returned even better results Test 0.935, Cross_val 0.921 (the team was very surprised by the result and went through the code several times to eliminate the possibility of mistakes)

### Conclusion

Given a task to select a project, find data, and pick a model to train is a very broad task. In real world data science projects, the constraints that are provided by the employer, be that a company, or a research institution actually are greatly helpful in terms of the work flow, and let the Data Scientist focus on the work rather then searching for a question to research.

### Data Dictionary

| *Column Name* | *Description* |
| :----------- | :----------- |
| state | Name of State |
| county_name | Name of County |
| unemployment_rate_2010 | County Unemployment Rate in 2010|
| urban_population_prc | County Urban Population % |
| rural_population_prc | County Rural Population % |
| crime_per_capita | County Crime Per Capita |
| per_capita_sme_num |County small and medium enterprises per capita |
| per_capita_large_num | County large enterprises per capita |
| avg_ann_pay_per_emp_sme | County average annual pay per small/medium size employer |
| avg_ann_pay_per_emp_large | County average annual pay per large size employer |
| avg_ann_pay_per_emp_total | County average annual pay per employer |
| population_jail_prc | County percentage of populatoin in jail |
| 2008_dem_%_vote | County percentage of population that voted Democrat in 2008 |
| 2008_rep_%_vote | County percentage of population that voted Republican in 2008 |
| 2008_other_%_vote | County percentage of population that voted other in 2008 |
| smoke_percent_2010 | County percentage of population that smokes |
| popul_hs_grad_prc | County percentage of population that graduated high school |
| popul_college_grad_prc | County percentage of population that graduated college |
| popul_single_paren_prc | County percentage of population that are single parents |
| liquor_stores_per10k | County number of liquor stores per 10,000 people |
| police_per_1000 | County number of police per 1,000 people |
| WhiteNonHispanicPct2010 | County percentage of white, non-hispanic people |
| BlackNonHispanicPct2010 | County percentage of black, non-hispanic people |
| AsianNonHispanicPct2010 |  County percentage of asian, non-hispanic people |
| NativeAmericanNonHispanicPct2010 | County percentage of native american, non-hispanic people |
| HispanicPct2010 | County percentage of hispanic people |
| MultipleRacePct2010 | County percentage of multi race people |

### Proper codebook execution order

01 Data loading and cleaning
02 EDA
03 Preprocessing and feature engineering
04 Modeling

Actual code is located in the code subfolder of the project root directory

### Additional resources

##### Graphs
Graphs derived from the codebooks and saved for use in presentation

##### Tableau
Graphs and maps derived from Tableau public for use in presentation

##### Data
Actual folder of the initial dataset and the datasets that were created during the execution of this project