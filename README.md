### 🦠 COVID-19 Data Analysis using Python

A complete Exploratory Data Analysis (EDA) and visualization project on global COVID-19 data using Python, Pandas, Matplotlib, and Seaborn.

This project answers key analytical questions about the spread, impact, and recovery trends of COVID-19 across different countries and time periods.

## 📌 Project Overview

This project analyzes global COVID-19 data by exploring confirmed cases, deaths, recoveries, monthly trends, country-wise summaries, and recovery rates.
It includes both visualizations and custom functions to generate summary statistics for any selected country or month.

The analysis is performed using the dataset: [Covid19data.xlsx](https://github.com/gulrez-zaidi/covid19-data-analysis-python/blob/main/Covid19data.xlsx)

## 📁 Dataset

The analysis is performed using the dataset: [Covid19data.xlsx](https://github.com/gulrez-zaidi/covid19-data-analysis-python/blob/main/Covid19data.xlsx)

Below is the code used to import the dataset after cloning the repo:

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load dataset from the repo
df = pd.read_excel("Covid19data.xlsx")

df.head()


## 🎯 Key Tasks Completed
✔ Task 1: 3 Most Affected Countries

Identified countries with the highest confirmed cases.

Visualized top 3 countries with the highest deaths.

✔ Task 2: Top 10 Countries with Highest Recovered Cases

Sorted countries by recovery numbers.

Created bar plots to show the top recoveries worldwide.

✔ Task 3: Recovery Rate Summary (Country-wise)

Calculated recovery rates using:
Recovery Rate = Recovered / Confirmed × 100

Generated a summary table for all countries.

✔ Task 4: Top 5 Countries with Highest Recovery Rates

Filtered only countries with significant case counts.

Visualized the top 5 countries with the highest recovery percentages.

✔ Task 5: Month-wise Trend Analysis

Grouped data by month.

Plotted month-wise:

Total Confirmed

Total Deaths

Total Recovered

Visualized how the pandemic evolved month-by-month.

✔ Task 6: Year-wise COVID-19 Trend

Aggregated global data by year.

Plotted:

Confirmed cases trend

Death trend

Recovery trend

✔ Task 7: Country Summary Function

A Python function that takes a country name and displays:

Total Confirmed

Total Deaths

Total Recovered

Recovery Rate

Fatality Rate

✔ Task 8: Month Summary Function

A Python function that takes a month and displays:

Monthly Confirmed

Monthly Deaths

Monthly Recoveries

Monthly recovery rate

🛠️ Technologies Used

Python

Pandas

NumPy

Matplotlib

Seaborn

Jupyter Notebook

📊 Visualizations Included

Bar charts (top affected countries)

Recovery rate comparison charts

Monthly trend line charts

Year-wise COVID-19 summary chart

Heatmaps (optional if implemented)

Custom data summary output
