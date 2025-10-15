# Trufflow-Breakthrough-Task1

Exploratory Data Analysis (EDA) - Ira Dharia

- For this part I previewed the tables for transactions, daily, and monthly using pandas and matplotlib + seaborn. There are no null values or duplicate rows as far as I can tell with my analysis. I visualized the relationship between transactions/data (x) and transactions/cost (y) in a scatterplot. For daily and monthly metrics I visualized the relationship between x='daily/metric', y='daily/value' in a boxplot which shows that "outage duration" and "cost" were the highest value.

Feature Engineering (FE) - Sydni Yang

- For the second part, I performed feature engineering on the transactions, daily metrics, and monthly metrics datasets. I pivoted the datasets to a wide format and renamed columns to standard labels (req_count, cost_sum, data_sum, cost_mean, and data). I cleaned the datasets by dropping constant and duplicate columns. I selected the best core features based on correlation, with cost_sum for transactions and req_count, cost_sum, and cost_mean for daily and monthly metrics. After feature engineering, the datasets were shaped and cleaned (values can be shown in the file).  
