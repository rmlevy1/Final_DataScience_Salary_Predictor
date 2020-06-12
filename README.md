# Data Science Salary Predictor

## Goal: 
Create a prediction model that will predict Data Analyst, Data Engineer, Machine Learning Engineer, Data Scientist salaries based off personalized criteria (i.e.experience, skills, location, size of company, revenue of company, state)

## Social Case: 
Help those landing a Data Science job negotiate their salary based off personalized criteria.


## Process:
#### Acquiring Data
Scraped ~1,500 jobs from Glassdoor via selenium\
(Received help from this blog post https://towardsdatascience.com/selenium-tutorial-scraping-glassdoor-com-in-10-minutes-3d0915c6d905) \
Scraped the following information from each job posting
* Job Title
* Salary Estimate
* Job Description
* Rating
* Company Name
* Location
* Headquarters Location
* Company Size (Employees)
* Year company founded
* Type of Ownership
* Sector
* Revenue

#### Data Cleaning & Feature Engineering
* Created a function to categorize job titles in to either:
  * data analyst
  * data scientist
  * data engineer 
  * machine learning engineer
* Created a feature for average salary by taking a the min of salary range and max of salary range from salary estimate and dividing by 2 
* Created a feature for job description word count
* Filled in all missing company size, sector, and type of ownership values with data fromn LinkedIn
* Filled in all missing values in revenue with data from Owler
* Created a feature for job being located in headquarters or not
* Created a feature for company having internation heaquarters or not
* Created a feature for company age
* Created a function to categorize jobs into 3 different seniority groups 
  * 0-2 Yrs Experience
  * 2-5 Yrs Experience
  * 5+ Yrs Experience
* Created a feature for mentions of Bachelor's, Master's or PhD in job description
* Created features for a variety of skills mentioned in job descriptions(i.e. python, sql, scipy, pytorch, docker, aws and etc)

#### EDA
I looked at the Features vs Average Salary and Features vs Value Counts.
A few highlights below.
<img src="Project%20Images/Comp_Size.png" width="300">
<img src="Project%20Images/Job_Titles.png" width="300">
<img src="Project%20Images/Seniority.png" width="300">

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
