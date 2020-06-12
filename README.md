# Data Science Salary Predictor

## Goal: 
Create a prediction model that will predict Data Analyst, Data Engineer, Machine Learning Engineer, Data Scientist salaries based off personalized criteria (i.e.experience, skills, location, size of company, revenue of company, state)

## Social Case: 
Help those landing a Data Science job negotiate their salary based off personalized criteria.

## Repository 
1. Data Cleaning & Feature Engineering
2. EDA & Feature Engineering
3. Modeling

## Process:
#### Acquiring Data
Scraped ~1,500 jobs from Glassdoor via selenium.\
(Credit to: https://towardsdatascience.com/selenium-tutorial-scraping-glassdoor-com-in-10-minutes-3d0915c6d905) 

Scraped the following information from each job posting: \
Job Title, Salary Estimate, Job Description, Rating, Company Name, Location, Headquarters Location, Company Size (Employees), Year company founded, Type of Ownership, Sector, Revenue

#### Data Cleaning & Feature Engineering
Check Data Cleaning & Feature Engineering file.

#### EDA
I inspected Features vs Average Salary to check for impact of features on target variable. 
I checked Features vs Value Counts to check for sparsity of data and to check hiring trends for data scientists.
A few highlights below.
<img src="Project%20Images/Comp_Size.png" width="300">
<img src="Project%20Images/Job_Titles.png" width="300">
<img src="Project%20Images/Seniority.png" width="300">
For further EDA, check the EDA & Feature Engineering file.

#### Modeling
One hot encoded all the categorical variables, creating 140 columns. \
Performed a train-test split of 80-20. 

I tried four different models and evaluated them based on Mean Absolute Error due to its interpretability.
 * Multiple Linear Regression - Due to its simplicity and interpretability of feature value and significance. 
 * Ridge & Lasso - Due to the sparse data in the many categorical features, I thought that a normalized regression would be effective.
 * Random Forest Regressor - Because of the sparsity associated with the data.
 
 Using GridSearchCV I found that the optimal alpha for Ridge was 27 and for Lasso 0.3.

#### Model Results (Mean Absolute Error)
* Baseline Model - 25.71
* Multiple Linear Regression - 22.16
* Ridge - 20.88
* Lasso - 20.37
* Random Forest Regressor - 21.05


The Lasso model performed the best with a mean absolute error of 20.37, meaning that its predictions were off by an average of $20,370.00 from othe actual salaries.

#### Slides
https://docs.google.com/presentation/d/1XiKExI6fY0AYU-il6l1-6o2bkgk8NSuOgG5JwhFysVg/edit?usp=sharing

## Further Work:
A lot more data is required for this model to be very accurate.
Around ~1,500 jobs is not enough. \
Would like to create an web facing api for people to enter their personalized job criteria and the interface would spit out a predicted salary based off a large set of data (~1,000,000).
