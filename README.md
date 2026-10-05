# Customer Churn Analysis

An end-to-end customer churn and revenue-impact analysis project built using Python, pandas, NumPy, Matplotlib, Seaborn, and Jupyter Notebook.

This project analyses customer demographics, subscription behaviour, plan types, contract structures, cancellation patterns, customer support interactions, and satisfaction scores to identify churn drivers and quantify the financial impact of customer attrition.

> **Built by Himanshu Taneja**

---

## Table of Contents

- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [Objectives](#objectives)
- [Files in This Repository](#files-in-this-repository)
- [Dataset Overview](#dataset-overview)
- [Technology Stack](#technology-stack)
- [Analysis Workflow](#analysis-workflow)
- [Key Metrics](#key-metrics)
- [Key Findings](#key-findings)
- [Business Recommendations](#business-recommendations)
- [How to Run the Project](#how-to-run-the-project)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Author](#author)

---

## Project Overview

Customer churn is a major challenge for subscription-based businesses. When customers leave, businesses lose recurring revenue, customer lifetime value, and future growth opportunities.

This project explores customer churn in a subscription-based OTT-style dataset. The analysis combines customer, subscription, and support data to answer three core questions:

- **Who** is most likely to churn?
- **Why** are customers leaving?
- **When** are churn levels highest?

The project follows a complete data analytics workflow, from importing and cleaning raw data to generating business insights and recommendations.

---

## Business Problem

The purpose of this project is to help a subscription business understand its churn problem and identify opportunities to improve customer retention.

The analysis investigates:

- Overall churn and retention performance.
- Churn by plan type and contract type.
- Churn by subscription or acquisition type.
- Geographic differences in churn.
- Monthly churn trends.
- Revenue loss associated with churned customers.
- Customer lifetime value lost through churn.
- The relationship between complaints, escalations, CSAT, and churn.

The final outputs are intended to support decisions across retention, customer success, pricing, product, and growth teams.

---

## Objectives

The project aims to:

1. Import customer churn data from Excel and CSV files.
2. Inspect and understand the structure of the dataset.
3. Clean inconsistent values, missing data, and date fields.
4. Combine customer, subscription, and support information.
5. Create calculated features such as churn flags, tenure, and cancellation month.
6. Calculate churn, retention, revenue, ARPU, and CLTV metrics.
7. Analyse churn by customer and subscription segments.
8. Visualise churn patterns using Matplotlib and Seaborn.
9. Identify customer segments at higher risk of churn.
10. Translate analytical findings into practical business recommendations.

---

## Files in This Repository

This repository intentionally contains three files.

### `CHURN_ANALYSIS.ipynb`

The main Jupyter Notebook containing the complete analysis workflow, including:

- Library imports.
- Data loading.
- Data inspection.
- Data cleaning.
- Feature engineering.
- Exploratory data analysis.
- Churn calculations.
- Revenue analysis.
- Visualisations.
- Correlation analysis.
- Business insights and recommendations.

### `exported_churn_data-2.csv`

A processed/exported customer churn dataset used for analysis.

The file contains customer-level subscription information combined with demographic and support-related fields, including:

- Customer ID.
- Subscription dates.
- Subscription type.
- Plan type.
- Contract type.
- Cancellation information.
- Monthly charges.
- CLTV.
- Churn score.
- Churn flag.
- Customer demographics.
- Complaint data.
- Escalation data.
- CSAT score.

### `customer_churn_data_raw-3.xlsx`

The raw source workbook containing the original data across three logical sections:

- Customer information.
- Subscription information.
- Customer support information.

This file is included to show the original source data before processing and analysis.

---

## Dataset Overview

The dataset contains information from three business areas.

### Customer data

Customer demographic and profile fields include:

- `customerid`
- `name`
- `country`
- `state`
- `gender`
- `dob`
- `interests`
- `pincode`

### Subscription data

Subscription and revenue fields include:

- `subscription_start_date`
- `subscription_type`
- `renewal_date`
- `plan_type`
- `contract_type`
- `cancellation_date`
- `cancellation_reason`
- `monthly_charges`
- `cltv`
- `churn_score`
- `churn_flag`

### Support data

Customer support fields include:

- `complaint_date`
- `escalations`
- `csat_score`
- `comment`
- `complaint_count`

The processed CSV combines relevant fields from these areas to create a customer-level analytical dataset.

---

## Technology Stack

- **Python** — Core programming language.
- **Jupyter Notebook** — Interactive analysis environment.
- **pandas** — Data loading, cleaning, transformation, and aggregation.
- **NumPy** — Numerical operations and array handling.
- **Matplotlib** — Chart creation and visual customisation.
- **Seaborn** — Statistical visualisation and heatmaps.
- **openpyxl** — Excel file support where required by pandas.

---

## Analysis Workflow

### 1. Import libraries

The notebook imports the main data analytics and visualisation libraries:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

### 2. Load the data

The raw Excel file and processed CSV file can be loaded using pandas:

```python
raw_data = pd.read_excel("customer_churn_data_raw-3.xlsx")
df = pd.read_csv("exported_churn_data-2.csv")
```

The exact loading method may vary depending on the structure of the workbook.

### 3. Inspect the dataset

The analysis checks:

- Number of rows and columns.
- Column names.
- Data types.
- Missing values.
- Duplicate records.
- Unique category values.
- Numerical distributions.

Typical inspection commands include:

```python
df.head()
df.info()
df.shape
df.isna().sum()
df.describe()
```

### 4. Clean the data

The cleaning process includes:

- Converting date columns into datetime format.
- Standardising column names.
- Handling missing values.
- Correcting inconsistent categorical labels.
- Normalising gender values such as `Male`, `Men`, `Female`, and `Women`.
- Validating churn indicators.
- Checking cancellation dates against churn flags.
- Reviewing duplicate customer and support records.

### 5. Engineer analytical features

The notebook creates features such as:

- Churn status.
- Cancellation month.
- Customer tenure.
- Revenue loss.
- Customer risk groups.
- Encoded categorical variables.
- Complaint and escalation indicators.

Example:

```python
df_visual["cancellation_month"] = (
    df_visual["cancellation_date"].dt.to_period("M")
)
```

### 6. Analyse churn

The project analyses churn across:

- Plan type.
- Contract type.
- Subscription type.
- State.
- Country.
- Cancellation month.
- Customer support activity.
- Churn-risk category.

### 7. Visualise results

The notebook creates:

- Churn-rate bar charts.
- Monthly churn trend charts.
- Churn-by-state visualisations.
- Revenue and CLTV comparisons.
- Distribution charts.
- Correlation heatmaps.

Example:

```python
churn_by_plan = (
    df.groupby("plan_type")["churn_flag"]
      .mean()
      .mul(100)
      .round(2)
      .reset_index(name="churn_rate_pct")
)
```

---

## Key Metrics

| Metric | Definition |
|---|---|
| Churn rate | Churned customers divided by total customers |
| Retention rate | \(1 - \text{churn rate}\) |
| Churn by plan | Churn rate grouped by plan type |
| Churn by state | Churn rate grouped by state |
| ARPU | Total revenue divided by number of users |
| Average tenure | Average duration between subscription start and cancellation or current date |
| Revenue loss | Sum of monthly charges associated with churned customers |
| CLTV lost | Total CLTV associated with churned customers |
| Complaint count | Total recorded complaints |
| Escalation rate | Escalated cases divided by total support cases |
| Average CSAT | Average customer satisfaction score |
| Revenue at risk | Revenue associated with customers classified as high risk |

---

## Key Findings

The analysis identified the following findings from the available dataset:

- Overall churn rate: **28.6%**.
- Retention rate: **71.4%**.
- Monthly-contract churn: **55.6%**.
- Annual-contract churn: **8.3%**.
- Monthly-contract customers churned at approximately **6.7 times** the rate of annual-contract customers.
- Average customer tenure: approximately **1,451 days**.
- Average revenue per user: approximately **18.8**.
- Total revenue represented in the analysis: approximately **395**.
- Monthly revenue associated with churned customers: approximately **73.94**.
- CLTV associated with churned customers: approximately **2,047**.
- Estimated revenue loss from churn: approximately **18%**.
- The highest concentration of cancellations occurred in **September 2024**.
- **Karnataka** was identified as the most affected state.
- The Basic plan recorded the highest number of churned customers.
- Cancellation reasons included competitor switching, pricing concerns, content dissatisfaction, streaming quality, and trial cancellation behaviour.

These findings are specific to the available sample and should be validated against a larger production dataset before commercial decisions are made.

---

## Business Recommendations

### Encourage annual subscriptions

Annual-contract customers show significantly lower churn than monthly-contract customers.

Recommended actions:

- Offer incentives for monthly-to-annual upgrades.
- Introduce annual plans with flexible payment options.
- Provide renewal discounts for long-term customers.
- Create targeted upgrade campaigns before renewal dates.

### Investigate regional churn

The high churn concentration in Karnataka should be investigated further.

Potential areas to review:

- Customer complaint volume.
- Support escalations.
- Streaming or technical issues.
- Pricing changes.
- Content availability.
- Competitor activity.
- Regional payment or renewal issues.

### Review the Basic plan experience

The Basic plan has the highest number of churned customers. The business should compare:

- Churn rate.
- Revenue contribution.
- Customer lifetime value.
- Complaint frequency.
- Feature access.
- Price sensitivity.
- Upgrade behaviour.

The plan with the highest number of churned users is not necessarily the plan causing the greatest revenue loss.

### Prioritise high-risk customers

Customers with high or medium churn scores should be segmented using:

- Churn score.
- Contract type.
- Plan type.
- CLTV.
- Complaint history.
- Escalation status.
- CSAT score.
- Recent cancellation signals.

High-value customers with high churn risk should receive the earliest retention intervention.

### Improve support-led retention

Support data should be used to identify customers who may be approaching churn.

Useful comparisons include:

- Churn among customers with no complaints.
- Churn among customers with complaints.
- Churn among customers with escalations.
- Churn among customers with low CSAT scores.
- Churn after unresolved support issues.

---

## How to Run the Project

### Prerequisites

Install Python 3.9 or later.

### Clone the repository

```bash
git clone [https://github.com/your-username/customer-churn-analysis.git](https://github.com/your-username/customer-churn-analysis.git)
cd customer-churn-analysis
```

### Create a virtual environment

#### macOS or Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### Install dependencies

```bash
pip install pandas numpy matplotlib seaborn jupyter openpyxl
```

Alternatively, create a `requirements.txt` file containing:

```text
pandas
numpy
matplotlib
seaborn
jupyter
openpyxl
```

Then install the dependencies:

```bash
pip install -r requirements.txt
```

### Launch Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
CHURN_ANALYSIS.ipynb
```

Run the notebook cells from top to bottom.

Make sure the following files are in the same directory as the notebook:

```text
CHURN_ANALYSIS.ipynb
exported_churn_data-2.csv
customer_churn_data_raw-3.xlsx
```

---

## Limitations

The analysis has several limitations:

- The dataset is relatively small and may not represent the full customer base.
- Revenue loss is estimated using available monthly charges.
- The analysis does not necessarily represent cumulative future revenue loss.
- Duplicate support records may affect complaint-related metrics.
- Correlation does not establish causation.
- Label encoding categorical fields can create artificial numerical relationships.
- Missing values may affect calculated averages and rates.
- Churn scores should be validated against future customer behaviour.
- State-level findings should be validated with a larger regional sample.
- The available data does not include complete product usage, payment failure, or engagement data.

---

## Future Improvements

Future versions of this project could include:

- A predictive churn classification model.
- Logistic regression, random forest, and gradient boosting models.
- Model evaluation using precision, recall, F1 score, and ROC-AUC.
- One-hot encoding for nominal categorical variables.
- Customer-level retention prioritisation.
- Monthly cohort retention analysis.
- Product-usage and engagement features.
- Automated data-quality checks.
- Interactive dashboards using Power BI, Tableau, Streamlit, or Plotly.
- A recurring churn monitoring report.
- More detailed revenue retention and customer lifetime value analysis.

---

## Author

This project was built by **Himanshu Taneja**.

The project demonstrates practical skills in:

- Python.
- pandas and NumPy.
- Data cleaning.
- Feature engineering.
- Exploratory data analysis.
- Customer churn analysis.
- Revenue-impact analysis.
- Matplotlib and Seaborn visualisation.
- Business insight generation.
- Data-driven retention recommendations.

---

## Licence

No licence has been specified for this repository.

If you want others to reuse, modify, or distribute the project, add an appropriate licence file such as the MIT Licence.

---

## Acknowledgements

This project was created as a portfolio data analytics project focused on customer churn, subscription behaviour, customer support, retention, and revenue impact.
