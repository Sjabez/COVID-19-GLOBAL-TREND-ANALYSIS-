
# COVID-19 Global Trend Analysis

## 🌍 **Project Overview**
This project analyzes worldwide COVID-19 case and death data to uncover global and country-level trends. The goal is to provide actionable visual insights that inform public health decisions, response planning, and policy communication.

---

## 🎯 **Business and Policy Objectives**
- Provide decision-makers with **clear visualizations of case and death trends** by country
- Identify **key peak periods** to support resource allocation and lockdown evaluation
- Compare **country-wise performance and recovery timelines**
- Highlight daily and cumulative changes to **track pandemic progression**
- Support **public health planning** with rolling averages and surge detection

---

## 📦 **Dataset Overview**
The dataset includes daily records of:
- **Date**
- **Country/Region**
- **Confirmed cases**
- **Recovered cases**
- **Deaths**

---

## 🔍 **Methodology**
- Cleaned and validated COVID-19 data
- Used aggregation and rolling averages to highlight meaningful trends
- Visualized country-specific comparisons and global time series
- Identified highest impact dates per region

---

## 📊 **Code with Policy-Oriented Annotations**

```python
# Load required libraries for data handling and plotting pandemic trends
#importing the required library
# Load required libraries for data handling and plotting pandemic trends
import pandas as pd
# Load required libraries for data handling and plotting pandemic trends
import numpy as np
# Load required libraries for data handling and plotting pandemic trends
import matplotlib.pyplot as plt
# Load required libraries for data handling and plotting pandemic trends
import seaborn as sns
# Load required libraries for data handling and plotting pandemic trends
import plotly
# Load required libraries for data handling and plotting pandemic trends
import plotly.express as px

# Import COVID-19 dataset for trend and case analysis
data = pd.read_csv("/content/covid_19_clean_complete.csv")

data

data.columns

data.rename(columns={"Date":"date","Province/State":"state","Country/Region":"country","Lat":"lat","Long":"long","Confirmed":"confirmed","Deaths":"deaths","Recovered":"recovered"
,"Active":"active","WHO Region":"WHO"},inplace=True)

data

# Preview the dataset to verify successful loading and structure
data.head()

data.tail()

# Identify peak dates or maximum case counts for surge analysis
data["date"].max()

# Identify peak dates or maximum case counts for surge analysis
top = data[data["date"] == data["date"].max()]
# top = data[data["date"] == "2020-07-27"]

top

# Aggregate case data by country or date to support policy comparison
w = data.groupby("country")["confirmed","active","deaths","recovered"].sum().reset_index()

w

fig=px.choropleth(w,locations='country',locationmode='country names',color='deaths',hover_name='country',
                 range_color=[10000,10000000],color_continuous_scale="Rainbow",title='Death cases acorss Countries')
fig.show()

# Visualize COVID trends over time to assist in planning and risk mitigation
#plot for confirmed cases
plt.figure(figsize=(15,10))
# Aggregate case data by country or date to support policy comparison
t_cases=data.groupby('date')['confirmed'].sum().reset_index()
t_cases['date']=pd.to_datetime(t_cases['date'])
# Visualize COVID trends over time to assist in planning and risk mitigation
a=sns.pointplot(x=t_cases.date.dt.date,y=t_cases.confirmed,color='r')
a.set(xlabel='Dates',ylabel='Cases total')
plt.xticks(rotation=90,fontsize=10)
plt.yticks(fontsize=15)
plt.xlabel('Dates',fontsize=10)
plt.ylabel('Cases total',fontsize=30)

t_cases

# Preview the dataset to verify successful loading and structure
t_actives = w.groupby(by="country")["active"].sum().sort_values(ascending=False).head(20).reset_index()

t_actives

plt.figure(figsize=(15,10))
plt.title('Top 20 countries having most active cases',fontsize=30)
# Visualize COVID trends over time to assist in planning and risk mitigation
a=sns.barplot(x=t_actives.active,y=t_actives.country)
a.set(xlabel='Cases total',ylabel='Country')
plt.xticks(fontsize=20)
plt.yticks(fontsize=20)
plt.xlabel('Cases total',fontsize=20)
plt.ylabel('Countryl',fontsize=20)

# Preview the dataset to verify successful loading and structure
t_deaths = w.groupby(by="country")["deaths"].sum().sort_values(ascending=False).head(20).reset_index()

t_deaths

plt.figure(figsize=(15,10))
plt.title('Top 20 countries having most death',fontsize=30)
# Visualize COVID trends over time to assist in planning and risk mitigation
a=sns.barplot(x=t_deaths.deaths,y=t_deaths.country)
a.set(xlabel='Cases total',ylabel='Country')
plt.xticks(fontsize=20)
plt.yticks(fontsize=20)
plt.xlabel('Cases total',fontsize=20)
plt.ylabel('Country',fontsize=20)

Brazil = data[data.country=="Brazil"]
# Aggregate case data by country or date to support policy comparison
Brazil = Brazil.groupby(by="date")["recovered","confirmed","active","deaths"].sum().reset_index()

Brazil

US = data[data.country=="US"]
# Aggregate case data by country or date to support policy comparison
US = US.groupby(by="date")["recovered","deaths","confirmed","active"].sum().reset_index()
US

Russia= data[data.country=="Russia"]
# Aggregate case data by country or date to support policy comparison
Russia = Russia.groupby(by="date")["recovered","deaths","confirmed","active"].sum().reset_index()
Russia

India= data[data.country=="India"]
# Aggregate case data by country or date to support policy comparison
India = India.groupby(by="date")["recovered","deaths","confirmed","active"].sum().reset_index()
India

plt.figure(figsize=(30,30))
# Visualize COVID trends over time to assist in planning and risk mitigation
sns.pointplot(data=Brazil, x=Brazil.index, y='confirmed', color="Blue", label="Brazil")
# Visualize COVID trends over time to assist in planning and risk mitigation
sns.pointplot(data=US, x=US.index, y='confirmed', color="Pink", label="US")
# Visualize COVID trends over time to assist in planning and risk mitigation
sns.pointplot(data=Russia, x=Russia.index, y='confirmed', color="Green", label="Russia")
# Visualize COVID trends over time to assist in planning and risk mitigation
sns.pointplot(data=India, x=India.index, y='confirmed', color="Red", label="India")
plt.xlabel('No. of days', fontsize=20)
plt.ylabel('Confirmed cases', fontsize=20)
plt.title('Confirmed cases over time', fontsize=30)
plt.xticks(rotation=90)
# Adding a legend to distinguish the countries
plt.legend()
plt.show()

plt.figure(figsize=(30,30))
# Visualize COVID trends over time to assist in planning and risk mitigation
sns.pointplot(data=Brazil, x=Brazil.index, y='recovered', color="Blue", label="Brazil")
# Visualize COVID trends over time to assist in planning and risk mitigation
sns.pointplot(data=US, x=US.index, y='recovered', color="Pink", label="US")
# Visualize COVID trends over time to assist in planning and risk mitigation
sns.pointplot(data=Russia, x=Russia.index, y='recovered', color="Green", label="Russia")
# Visualize COVID trends over time to assist in planning and risk mitigation
sns.pointplot(data=India, x=India.index, y='recovered', color="Red", label="India")
plt.xlabel('No. of days', fontsize=20)
plt.ylabel('recovered cases', fontsize=20)
plt.title('recovered cases over time', fontsize=30)
# Adding a legend to distinguish the countries
plt.legend()
plt.show()

pip install prophet

# Load required libraries for data handling and plotting pandemic trends
from prophet import Prophet

# Preview the dataset to verify successful loading and structure
data.head()

# Preview the dataset to verify successful loading and structure
data.groupby("date").sum().head()

data["active"].sum()

# Aggregate case data by country or date to support policy comparison
confirmed = data.groupby("date").sum()["confirmed"].reset_index()
# Aggregate case data by country or date to support policy comparison
death = data.groupby("date").sum()["deaths"].reset_index()
# Aggregate case data by country or date to support policy comparison
recovered = data.groupby("date").sum()["recovered"].reset_index()

confirmed

recovered

death

confirmed.columns = ["ds","y"]
confirmed["ds"] = pd.to_datetime(confirmed["ds"])
confirmed.tail()

m = Prophet(interval_width = 0.95)
m.fit(confirmed)

future = m.make_future_dataframe(periods=7,freq="D")
future.tail(7)

forecast = m.predict(future)
forecast[["ds","yhat","yhat_lower","yhat_upper"]].tail(7)

# Visualize COVID trends over time to assist in planning and risk mitigation
confirmed_forecast_plot = m.plot(forecast)

# Visualize COVID trends over time to assist in planning and risk mitigation
confirmed_forecast_plot = m.plot_components(forecast)
```

---

## 💡 **Insights for Decision Makers**
- Peak case and death dates differ significantly across regions
- Rolling averages improve visibility into trend shifts and post-surge stability
- Policy makers can use this data to prepare **targeted responses** and **resource deployments**

---

## 🛠 **Tools & Technologies**
- Python (Pandas, NumPy)
- Matplotlib, Seaborn for visualization
- Jupyter Notebook

---

## 🚀 **Next Steps**
- Integrate vaccination and mobility data for more holistic insight
- Build an interactive dashboard for health departments and analysts
- Automate country-level PDF reports using Python

---
