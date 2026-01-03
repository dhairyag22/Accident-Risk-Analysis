# Accident Risk Analysis

## Overview

This project focuses on analyzing accident risk using a structured dataset containing road, traffic, environmental, and temporal features. The objective is to understand the key factors contributing to accident risk through detailed **exploratory data analysis (EDA)** and to enhance the dataset using **feature engineering techniques**.

## Dataset Description

The dataset consists of multiple numerical and categorical features related to road conditions, traffic characteristics, weather and time.

The **target variable** is:     
`accident_risk` – represents the risk or severity associated with accidents.

**Libraries Used**

* *Pandas* and *NumPy* for data manipulation
* *Matplotlib* and *Seaborn* for data visualization

## Step 1: Data Loading and Initial Inspection

A **custom summary function** was created to display:

* Data type of each column
* Number and percentage of missing values
* Cardinality of features

```
def column_summary(df):
    summary = pd.DataFrame({
        'col_name' : df.columns,
        'col_dtype' : df.dtypes.values,
        'num_of_nulls' : df.isnull().sum().values,
        'null%' : round((df.isnull().sum()/df.shape[0])*100, 2).values,
        'num_of_distinct_values' : df.nunique().values
    })
    return summary
```

**Initial inspection** included:

* Dataset shape
* Column names and data types
* Missing values
* Unique value counts per feature

## Step 2: Data Cleaning

**Duplicate Handling**: 
Duplicate rows were identified using `df.duplicated()`.
All duplicate entries were removed to maintain data integrity.

## Step 3: Exploratory Data Analysis (EDA)

1. **Univariate Analysis**
This helped in understanding the distribution and frequency of values across the dataset.

2. **Outlier Detection and Removal**
Boxplots were used to detect outliers in numerical features. Extreme values that could distort statistical analysis were identified. *Outliers* were removed to improve data quality and stability.

3. **Bivariate Analysis**
Relationships between independent variables and the target variable (`accident_risk`) were analyzed.

* Bar plots were used for categorical features.
* Scatter plots were used for continuous features such as road curvature.

This analysis helped identify:

* High-risk categories
* Influential variables
* Non-linear relationships affecting accident risk

## Step 4: Feature Engineering

### Risk-Based Binary Indices

Several categorical features were transformed into binary risk indicators based on domain logic:


| Feature Index | Risk Interpretation |
|--------------|--------------------|
| Lighting Index | Higher risk during night conditions |
| Weather Index | Higher risk during adverse weather (rain, fog) |
| Time of Day Index | Higher risk during afternoon and evening hours |
| Urbanization Index | Higher risk in urban areas and highways |
| Speed Index | Higher risk at higher speed limits |

### Interaction Features

To capture complex real-world relationships, interaction features were created, including:

* Curvature–speed interaction
* Traffic density
* Accident density

These features provide better representation of combined risk factors than raw variables alone.

* Overall Risk Index

Multiple engineered risk indicators were aggregated into a single `overall_risk_index`.

## Step 5: Correlation Analysis

Important numerical and engineered features were selected.
A **correlation heatmap** was generated to:

* Identify strong relationships between features and accident risk
* Validate the effectiveness of feature engineering
* Detect multicollinearity among predictors

Key observations showed that engineered risk indices had stronger correlations with the target variable compared to many raw features.

## Key Outcomes

* Cleaned and preprocessed dataset with no duplicates
* Comprehensive understanding of accident-related risk factors
* Meaningful engineered features reflecting real-world conditions
* Clear visual insights into feature–target relationships
* A strong analytical foundation suitable for predictive modeling or risk assessment systems