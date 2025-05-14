# Week-8-Python-


import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px  # For optional world map


%matplotlib inline

# IS to load the COVID-19 dataset directly from Our World in Data
url = 'https://covid.ourworldindata.org/data/owid-covid-data.csv'
df = pd.read_csv(url)

df.head() 

# Data Loading & Exploration
countries = ['South Africa', 'China', 'United States']

df = df[df['location'].isin(countries)]

df = df.dropna(subset=['date', 'total_cases'])

df['date'] = pd.to_datetime(df['date'])


df.fillna(0, inplace=True)
# Data Cleaning
plt.figure(figsize=(10, 5))

for country in countries:
    country_df = df[df['location'] == country]
    plt.plot(country_df['date'], country_df['total_cases'], label=country)
    
# Total Cases Over Time
plt.title('Total COVID-19 Cases Over Time')
plt.xlabel('Date')
plt.ylabel('Total Cases')
plt.legend()
plt.grid(True)
plt.show()

# Total Deaths Over Time
plt.figure(figsize=(10, 5))

for country in countries:
    country_df = df[df['location'] == country]
    plt.plot(country_df['date'], country_df['total_deaths'], label=country)

plt.title('Total COVID-19 Deaths Over Time')
plt.xlabel('Date')
plt.ylabel('Total Deaths')
plt.legend()
plt.grid(True)
plt.show()

#  Daily New Cases
plt.figure(figsize=(12, 6))

for country in countries:
    country_df = df[df['location'] == country]
    plt.plot(country_df['date'], country_df['new_cases'], label=country)

plt.title('Daily New COVID-19 Cases')
plt.xlabel('Date')
plt.ylabel('New Cases')
plt.legend()
plt.grid(True)
plt.show()

# Death Rate Over Time
df['death_rate'] = df['total_deaths'] / df['total_cases']

plt.figure(figsize=(10, 5))

for country in countries:
    country_df = df[df['location'] == country]
    plt.plot(country_df['date'], country_df['death_rate'], label=country)

plt.title('COVID-19 Death Rate Over Time')
plt.xlabel('Date')
plt.ylabel('Death Rate')
plt.legend()
plt.grid(True)
plt.show()

# Total Vaccinations Over Time
plt.figure(figsize=(10, 5))

for country in countries:
    country_df = df[df['location'] == country]
    plt.plot(country_df['date'], country_df['total_vaccinations'], label=country)

plt.title('Total COVID-19 Vaccinations Over Time')
plt.xlabel('Date')
plt.ylabel('Vaccinations')
plt.legend()
plt.grid(True)
plt.show()

# Add Insights in Markdown Cell
- 🇺🇸 The United States experienced the highest total number of cases and deaths.
- 🇨🇳 China had relatively flat reported cases due to early control and different reporting policies.
- 🇿🇦 South Africa had visible spikes during the Delta and Omicron waves.
- Vaccination progress was fastest in the United States, followed by China and then South Africa.
