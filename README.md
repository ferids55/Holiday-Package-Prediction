# Holiday Package Prediction

## Project Overview
The company **Trips&Travel.com** wants to offer a new vacation package. Currently, there are 5 types of packages offered by the company, namely **Basic, Standard, Deluxe, Super Deluxe, King** . Based on last year's data, it was found that **only 18% of customers bought the package. However, the marketing costs are quite high because customers are contacted randomly** without seeing the available information. The company plans to launch a new product called **Wellness Tourism** . Companies want to leverage available data from existing and potential customers to make marketing spending more efficient.

## Business Problems
- Only 18% of customers bought holiday packages because the marketing was done randomly in the last year so that the marketing costs used were quite high.
- The company wants to use data on existing and potential customers for marketing new holiday packages.

## Objectives
- Create a system that can help companies predict which customers will be targeted for new product offerings in order to increase conversion rates and reduce marketing costs.
- Knowing the characteristics of potential customers who will buy holiday packages to find new customers.

## Analytics Approach
Perform **predictive analysis with supervised learning (classification)** to predict customers who will buy vacation packages.

<hr>

## Data Requirement
The dataset used is from [Kaggle](https://www.kaggle.com/datasets/susant4learning/holiday-package-purchase-prediction). The dataset consists of 4888 rows and 20 columns with the following attributes.berikut.

- **CustomerID** : Unique customer ID
- **ProdTaken** : Product taken or not (0: No, 1: Yes)
- **Age** : Age of customer
- **TypeofContact** : How customer was contacted (Company Invited or Self Inquiry)
- **CityTier** : City tier depends on the development of a city, population, facilities, and living standards. The categories are ordered i.e.
- **DurationOfPitch** : Duration of the pitch by a salesperson to the customer
- **Occupation** : Occupation of customer
- **Gender** : Gender of customer
- **NumberOfPersonVisiting** : Total number of persons planning to take the trip with the customer
- **NumberOfFollowups** : Total number of follow-ups has been done by the salesperson after the sales pitch
- **ProductPitched** : Product pitched by the salesperson
- **PreferredPropertyStar** : Preferred hotel property rating by customer
- **MaritalStatus** : Marital status of customer
- **NumberOfTrips** : Average number of trips in a year by customer
- **Passport** : The customer has a passport or not (0: No, 1: Yes)
- **PitchSatisfactionScore** : Sales pitch satisfaction score
- **OwnCar** : Whether the customers own a car or not (0: No, 1: Yes)
- **NumberOfChildrenVisiting** : Total number of children with age less than 5 planning to take the trip with the customer
- **Designation** : Designation of the customer in the current organization
- **MonthlyIncome** : Gross monthly income of the customer

Of the 20 columns that will be selected as targets are columns `ProdTaken` while the other columns are used as features and will be re-selected which ones are suitable.

## Exploratory Data Analysis
1. Multivariate Analysis (numeric column against target)
![multivariate1](/fig/multivariate_analysis_num.png)

2. Multivariate Analysis (categorical column against target)
![multivariate2](/fig/multivariate_analysis_cat.png)

3. More basic products are bought by customers
![produk](/fig/insight1.png)

4. Each type of product is only offered in 1 position only
![jabatan](/fig/04.png)

5. Teenagers (17-25 years old) tend to prefer to buy holiday packages
![umur](/fig/01.png)

6. The increasing number of follow-ups greatly affects the purchase of holiday packages
![followup](/fig/insight2.png)


## Preprocessing
1. Inconsistent data found
    - In the column `Gender` it should be **"Fe Male"** to **"Female"**
    - In the column `MaritalStatus`, **"Single"** should be interpreted the same as **"Unmarried"**
2. Missing values ​​were found in 8 columns and will be handled with the following imputation method
    - Column `Age` will be filled with mean value
    - Column `TypeofContact` will be filled with value "Unknown"
    - Column `DurationOfPitch` will be filled with median value
    - Column `NumberOfFollowups` will be filled with min value
    - Column `PreferredPropertyStar` will be filled with value 3
    - Column `NumberOfTrips` will be filled with median value
    - Column `NumberOfChildrenVisiting` will be filled with value 0
    - Column `MonthlyIncome` will be filled with median value
3. Found 141 duplicate data rows that need to be deleted
4. Found some data that are considered outliers with the **Z-Score approach**
5. Create a new column named `TotalVisiting` = `NumberOfPersonVisiting` + `NumberOfChildrenVisiting`
6. Encoding data in categorical columns
    - Column `Gender`, `ProductPitched` and `Designation` performed **Label Encoding**
    - Column `TypeofContact`, `Occupation`, and `MaritalStatus` performed **One Hot Encoding**
7. Perform data transformations on numeric columns
    - Column `Age` transformed by **normalization**
    - Column `DurationOfPitch` and `MonthlyIncome` transformed by **standardization**
8. Feature selection using **Pearson Correlation** and **Chi Square Test**

## Modelling
- The data is divided into train set and test set with the **proportion of 80:20**
- The algorithms used in the modeling are **Logistic Regression, Decision Tree, Random Forest, AdaBoost, and XGBoost**
- The evaluation metrics chosen are **F1-Score and AUC**
- Performing hyperparameter tuning
- Making feature importance of the best model

<hr>

## Result

### Best Model
![result](/fig/model_result.PNG)

XGBoost is the best model with the highest **F1-Score of 82.39% and AUC of 0.9707** with confusion matrix results, namely

    - True Positive 131
    - False Positive 17
    - True Negative 760
    - False Negative 39

### Modelling Insights
1. There are 4 features that are quite influential, namely `Passport`, `ProductPitched`, `MaritalStatus`, and `CityTier`
![feat_importance](/fig/feature_importance.png)

2. Only Standard products tend to be bought by people who don't have a passport
![passport](/fig/06.png)

3. Product types are offered based on job title or monthly income
![income](/fig/05.png)

4. Basic products are mostly bought by unmarried customers
![status](/fig/07.png)

5. Customers who live in City Tier 1 or 2 buy more Basic products while those in City Tier 3 buy more Deluxe products
![city](/fig/08.png)

### Business Impact
Based on testing on test data, the machine learning model created succeeded in **increasing the conversion rate by 88.5%** (148 people out of 170 people) and **reducing marketing costs by 83%** (35097 USD).

![impact](/fig/model_impact.PNG)

<hr>

## Recommendation
1. **Conduct marketing campaigns for potential customers for Wellness Tourism** packages with the following conditions:
    - If the Wellness package consists of several types, it can be prioritized **from the cheapest according to the customer's job title**.
    - Prioritize **teenagers (18-25 years old)** with pitch durations under 20 minutes .
    - **The cheapest Wellness package** can be offered to customers with **unmarried status or living in city tier 1 or 2**.
    - **The medium Wellness package** can be offered to customers who **do not have a passport or live in city tier 3**.
    - Other Wellness packages can be **offered according to the customer's monthly income**.
    - Don't forget to **follow up more than 3 times**.
2. If we use this model, **the revenue you get is less**, so we recommend that the **remaining marketing costs be used to find a new customer base** so that the revenue generated increases.