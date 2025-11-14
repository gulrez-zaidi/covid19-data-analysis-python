# 🦠 COVID-19 Data Analysis using Python

A complete Exploratory Data Analysis (EDA) and visualization project on global COVID-19 data using Python, Pandas, Matplotlib, and Seaborn.
This project answers key analytical questions about the spread, impact, and recovery trends of COVID-19 across different countries and time periods.

## 📌 Project Overview

This project analyzes global COVID-19 data by exploring confirmed cases, deaths, recoveries, monthly trends, country-wise summaries, and recovery rates.
It includes both visualizations and custom functions to generate summary statistics for any selected country or month.

The analysis is performed using the dataset: [Covid19data.xlsx](https://github.com/gulrez-zaidi/covid19-data-analysis-python/blob/main/Covid19data.xlsx)

## 📁 Dataset

The analysis is performed using the dataset: [Covid19data.xlsx](https://github.com/gulrez-zaidi/covid19-data-analysis-python/blob/main/Covid19data.xlsx)

Below is the code used to import the dataset after cloning the repo:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

**Load dataset from the repo**
```
df = pd.read_excel("Covid19data.xlsx")
df.head()
```

## 🎯 Key Tasks Completed
### Task 1: 3 Most Affected Countries
```
import matplotlib.pyplot as plt
import numpy as np

# Top 3 countries by confirmed cases
df1 = df.groupby('Country')[['Confirmed','Deaths']].sum().sort_values(by="Confirmed", ascending=False).head(3)

# Extract X positions
x = np.arange(len(df1))         # positions: [0,1,2]

# Extract values
confirmed = df1['Confirmed']
deaths = df1['Deaths']

width = 0.35 

plt.figure(figsize=(10,6))      # 10 → width of the chart (in inches) & 6 → height of the chart (in inches)

# Confirmed bars
plt.bar(x - width/2, confirmed, width=0.35, label='Confirmed')  #Bars for Confirmed are placed slightly left.

# Deaths bars
plt.bar(x + width/2, deaths, width=0.35, label='Deaths')       #Bars for Deaths are placed slightly Right.

# X-axis labels
plt.xticks(x, df1.index)    # Show the country names exactly at positions 0, 1, and 2 on the X-axis.

plt.xlabel("Country")
plt.ylabel("Number of Cases")
plt.title("Top 3 Countries Most Affected by COVID-19 (Confirmed & Deaths)", fontsize=14, color='red')

plt.legend()
plt.show()
```

### Task 2: Top 10 Countries with Highest Recovered Cases
```
df2 = df.groupby('Country')['Recovered'].sum().sort_values(ascending=False).head(10)

x = df2.index          # country names
y = df2.values         # recovered numbers

plt.figure(figsize=(10,6))
plt.barh(x, y, color='green', label="Recovered Cases")

plt.xlabel("Recovered Cases")
plt.ylabel("Countries")
plt.title("Top 10 Countries with Highest Recovered Cases", fontsize=14, color='red')
plt.legend()
plt.show()
```

### Task 3: Recovery Rate Summary (Country-wise)

***Calculate the recovery rate for each country using the formula: Recovery Rate=(Recovered Cases/Confirmed Cases)×100***
```
df["Recovery Rate"]=(df["Recovered"]/df["Confirmed"])*100
df
```

### Task 4: Top 5 Countries with Highest Recovery Rates
```
df3 = df.groupby('Country')['Recovery Rate'].sum().sort_values(ascending=False).head(5)

x = df3.index          # country names
y = df3.values         # recovered numbers

plt.figure(figsize=(10,6))
plt.bar(x, y, color='blue', label="Recovery Rate")

plt.xlabel("Countries")
plt.ylabel("Recovery Rate")
plt.title("Top 5 countries with the highest recovery rates", fontsize=14, color='red')
plt.legend()
plt.show()
```

### Task 5: Month-wise Trend Analysis
```
df['Month'] = df['ObservationDate'].dt.to_period('M')
df
```
```
df_monthly = df.groupby("Month")[['Confirmed','Deaths','Recovered']].sum()

x = df_monthly.index.to_timestamp().strftime('%b %Y')   
y1 = df_monthly['Confirmed']
y2 = df_monthly['Deaths']
y3 = df_monthly['Recovered']

plt.figure(figsize=(14,8)) 

plt.plot(x, y1, marker='o', label='Confirmed Cases', linewidth=2)
plt.plot(x, y2, marker='o', label='Deaths', linewidth=2)
plt.plot(x, y3, marker='o', label='Recovered', linewidth=2)

plt.xlabel("Month")
plt.ylabel("Number of Cases")
plt.title("Monthly Trend of COVID-19 Cases (Confirmed, Deaths, Recovered)", fontsize=18, color='red')

plt.xticks(rotation=90)     
plt.grid(True, alpha=0.3)   
plt.legend()
plt.tight_layout()          
plt.show() 
```

### Task 6: Year-wise COVID-19 Trend
```
df['Year'] = df['ObservationDate'].dt.year
df
```
```
df_yearly = df.groupby("Year")[['Confirmed','Deaths','Recovered']].sum()

x = df_yearly.index   
y1 = df_yearly ['Confirmed']
y2 = df_yearly ['Deaths']
y3 = df_yearly ['Recovered']

plt.figure(figsize=(14,8)) 

plt.plot(x, y1, marker='o', label='Confirmed Cases', linewidth=3)
plt.plot(x, y2, marker='o', label='Deaths', linewidth=3)
plt.plot(x, y3, marker='o', label='Recovered', linewidth=3)

plt.xlabel("Year")
plt.ylabel("Number of Cases")
plt.title("Year-wise COVID-19 Trend (Confirmed, Deaths, Recovered)", fontsize=18, color='red')

plt.grid(True, alpha=0.3)   
plt.legend()
plt.xticks(x, x.astype(str))
plt.tight_layout()          
plt.show()
```

### Task 7: Country Summary Function
```
CFR=(Deaths/Confirmed Cases)*100
df['CFR']=df['Deaths']/df['Confirmed']*100
```
```
def country_summary(country):
    # Filter rows for the selected country
    df_country = df[df['Country'] == country]
    
    if df_country.empty:
        print(f"No data found for '{country}'")
        return
    
    # Aggregate totals
    confirmed = df_country['Confirmed'].sum()
    deaths = df_country['Deaths'].sum()
    recovered = df_country['Recovered'].sum()
    
    # Calculate recovery rate
    recovery_rate = (recovered / confirmed) * 100 if confirmed > 0 else 0
    
    # Calculate CFR (Case Fatality Rate)
    cfr = (deaths / confirmed) * 100 if confirmed > 0 else 0
    
    # Print results
    print(f"\nCOVID-19 Summary for: {country}")
    print("-------------------------------------")
    print(f"Total Confirmed Cases : {confirmed}")
    print(f"Total Deaths          : {deaths}")
    print(f"Total Recovered       : {recovered}")
    print(f"Recovery Rate (%)     : {recovery_rate:.2f}%")
    print(f"Case Fatality Rate (%) : {cfr:.2f}%")
```

### Task 8: Month Summary Function
```
def month_summary(month):
    # Filter the dataframe for the selected month
    df_month = df[df['Month'] == month]
    
    if df_month.empty:
        print(f"No data found for month '{month}'")
        return
    
    # Aggregate totals
    confirmed = df_month['Confirmed'].sum()
    deaths = df_month['Deaths'].sum()
    recovered = df_month['Recovered'].sum()
    
    # Calculate recovery rate
    recovery_rate = (recovered / confirmed) * 100 if confirmed > 0 else 0
    
    # Calculate Case Fatality Rate (CFR)
    cfr = (deaths / confirmed) * 100 if confirmed > 0 else 0

    # Print results
    print(f"\nCOVID-19 Summary for Month: {month}")
    print("-------------------------------------")
    print(f"Total Confirmed Cases : {confirmed}")
    print(f"Total Deaths          : {deaths}")
    print(f"Total Recovered       : {recovered}")
    print(f"Recovery Rate (%)     : {recovery_rate:.2f}%")
    print(f"Case Fatality Rate (%) : {cfr:.2f}%")
```

## 🛠️ Technologies Used

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Jupyter Notebook**
