<div align="center">

# 🐍 Python Data Analysis & Projects Portfolio

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)](https://numpy.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge&logo=python&logoColor=white)](https://matplotlib.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://seaborn.pydata.org/)
[![Profile Views](https://komarev.com/ghpvc/?username=FarisDataAnalysts&color=3776AB&style=flat-square&label=Profile+Views)](https://github.com/FarisDataAnalysts)

> *Python projects spanning data analysis, HR analytics, API integration & automation — from EDA to end-to-end applications.*

**4 Projects · Data Analysis · Automation · Application Development**

</div>

---

## 📌 Table of Contents

- [About This Repository](#-about-this-repository)
- [Projects](#-projects)
  - [Amazon Sales Analysis](#1️⃣-amazon-sales-analysis)
  - [HR Analytics using Python](#2️⃣-hr-analytics-using-python)
  - [Weather Chatbot](#3️⃣-weather-chatbot)
  - [Number Guessing Game](#4️⃣-number-guessing-game)
- [Python Concepts Covered](#-python-concepts-covered)
- [Tech Stack](#️-tech-stack)
- [Skills Demonstrated](#-skills-demonstrated)
- [Getting Started](#-getting-started)
- [Connect With Me](#-connect-with-me)

---

## 🎯 About This Repository

This repository is a portfolio of **Python projects** that span real-world data analysis, API-driven automation, and application development. Projects range from full exploratory data analysis (EDA) pipelines to interactive chatbots — showcasing both analytical depth and programming breadth.

Each project was built to solve a genuine problem: understanding sales patterns, explaining workforce attrition, retrieving live weather data, or simply writing clean, functional Python logic.

---

## 📁 Projects

---

### 1️⃣ Amazon Sales Analysis

> 📦 File: `Amazon_Sale_Analysis.rar`

**Objective:** Perform end-to-end exploratory data analysis on Amazon e-commerce sales data to uncover revenue trends, customer behaviour, and product performance insights.

#### Business Questions Answered
- Which product categories drive the most revenue?
- What are the peak sales periods throughout the year?
- How does discount rate affect units sold and profit margin?
- Which customer segments generate the highest lifetime value?
- What are the top 10 best-selling products by volume and revenue?

#### Analysis Pipeline

```python
# Analysis workflow
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Data Loading & Inspection
df = pd.read_csv('amazon_sales.csv')
df.info(), df.describe(), df.isnull().sum()

# 2. Data Cleaning
df.dropna(subset=['order_id', 'revenue'], inplace=True)
df['order_date'] = pd.to_datetime(df['order_date'])

# 3. Feature Engineering
df['month'] = df['order_date'].dt.to_period('M')
df['profit_margin'] = (df['revenue'] - df['cost']) / df['revenue'] * 100

# 4. EDA & Visualisation
monthly_revenue = df.groupby('month')['revenue'].sum()
sns.lineplot(data=monthly_revenue)
plt.title('Monthly Revenue Trend')
plt.show()
```

#### Key Analysis Areas

| Area | Details |
|------|---------|
| 🛒 Sales Trends | Monthly/quarterly revenue patterns and seasonality |
| 📦 Products | Category performance, top sellers, margin analysis |
| 👥 Customers | Segmentation by order frequency and spend |
| 🏷️ Discounts | Discount elasticity — how offers affect revenue |
| 📊 Visualisations | Heatmaps, trend lines, bar charts, distribution plots |

**Libraries:** Pandas · NumPy · Matplotlib · Seaborn
**Concepts:** EDA · Data Cleaning · Feature Engineering · Statistical Analysis · Data Visualisation

---

### 2️⃣ HR Analytics using Python

> 📄 File: `HR_Analysis_using_Python.pdf`

**Objective:** Analyse employee data to identify attrition drivers, understand workforce demographics, and surface insights that support better HR decision-making.

#### Business Questions Answered
- What is the overall and department-level attrition rate?
- Which factors most strongly correlate with employee resignation?
- How does salary level relate to satisfaction and retention?
- Which departments have the highest performance ratings?
- What does the workforce age and tenure distribution look like?

#### Analysis Pipeline

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Attrition rate by department
attrition_rate = (
    df.groupby('Department')['Attrition']
    .value_counts(normalize=True)
    .unstack()
    .rename(columns={'Yes': 'Attrition_Rate'})
)

# Correlation heatmap for numeric HR features
numeric_cols = df.select_dtypes(include='number')
sns.heatmap(numeric_cols.corr(), annot=True, cmap='coolwarm', fmt='.2f')
plt.title('HR Feature Correlation Matrix')
plt.show()
```

#### Key Analysis Areas

| Area | Details |
|------|---------|
| 📉 Attrition | Attrition rate, resignation drivers, risk segmentation |
| 💵 Compensation | Salary band distribution and pay equity analysis |
| 🏆 Performance | Rating distribution across departments and roles |
| 🧑‍🤝‍🧑 Demographics | Age group, gender, and tenure analysis |
| 🔗 Correlations | Feature correlation matrix to identify key attrition signals |

**Libraries:** Pandas · NumPy · Matplotlib · Seaborn
**Concepts:** Statistical Analysis · Correlation Analysis · Categorical Encoding · Data Visualisation · HR Domain Analytics

---

### 3️⃣ Weather Chatbot

> 📄 File: `Weather Chatbot Python Mini Project.pdf`

**Objective:** Build a conversational Python chatbot that fetches real-time weather data for any location using a public weather API, with a clean and user-friendly interface.

#### Features

| Feature | Description |
|---------|-------------|
| 🌍 Location Search | Query weather for any city worldwide |
| 🌡️ Temperature | Current temp with Celsius/Fahrenheit toggle |
| ☁️ Conditions | Weather condition description and humidity |
| 💨 Wind | Wind speed and direction data |
| 🔄 Live Data | Real-time data fetched via API on each request |
| ⚠️ Error Handling | Graceful handling of invalid cities and API failures |

#### Application Structure

```python
import requests

def get_weather(city: str) -> dict:
    """Fetch current weather data for a given city."""
    API_KEY = "your_api_key"
    BASE_URL = "https://api.openweathermap.org/data/2.5/weather"
    
    params = {"q": city, "appid": API_KEY, "units": "metric"}
    response = requests.get(BASE_URL, params=params)
    
    if response.status_code == 200:
        return response.json()
    else:
        raise ValueError(f"City '{city}' not found. Please try again.")

def chatbot():
    """Main chatbot loop."""
    print("🤖 Weather Bot: Hi! Which city's weather would you like to check?")
    while True:
        city = input("You: ").strip()
        if city.lower() in ['exit', 'quit']:
            break
        try:
            data = get_weather(city)
            temp = data['main']['temp']
            desc = data['weather'][0]['description']
            print(f"🤖 Weather Bot: It's {temp}°C and {desc} in {city}.")
        except ValueError as e:
            print(f"🤖 Weather Bot: {e}")
```

**Libraries:** Requests · Built-in Python (`json`, `os`)
**Concepts:** REST API Integration · JSON Parsing · Error Handling · Conversational Flow · Input Validation

---

### 4️⃣ Number Guessing Game

> 📄 File: `Number Guessing Game in Python.pdf`

**Objective:** Build a clean, interactive Python game that demonstrates core programming fundamentals — control flow, functions, input handling, and user experience design.

#### Features

| Feature | Description |
|---------|-------------|
| 🎲 Random Generation | A secret number is randomly generated each round |
| 💡 Hints | "Too high" / "Too low" feedback on every guess |
| 🔢 Attempt Counter | Tracks and displays the number of guesses |
| 🏆 Scoring | Rates performance based on number of attempts |
| 🔁 Replay | Option to play multiple rounds without restarting |
| ⚠️ Input Validation | Handles non-numeric and out-of-range inputs gracefully |

#### Application Structure

```python
import random

def play_game(lower: int = 1, upper: int = 100) -> None:
    """Run a single round of the number guessing game."""
    secret = random.randint(lower, upper)
    attempts = 0
    
    print(f"🎮 Guess a number between {lower} and {upper}!")
    
    while True:
        try:
            guess = int(input("Your guess: "))
            attempts += 1
            
            if guess < secret:
                print("📉 Too low! Try higher.")
            elif guess > secret:
                print("📈 Too high! Try lower.")
            else:
                print(f"🎉 Correct! You got it in {attempts} attempt(s).")
                rate_performance(attempts)
                break
        except ValueError:
            print("⚠️ Please enter a valid number.")

def rate_performance(attempts: int) -> None:
    if attempts <= 3:
        print("⭐⭐⭐ Excellent!")
    elif attempts <= 6:
        print("⭐⭐ Good job!")
    else:
        print("⭐ Keep practising!")

if __name__ == "__main__":
    play_game()
```

**Libraries:** `random` · Built-in Python
**Concepts:** Control Flow · Functions · Input Validation · Error Handling · Game Logic · User Interaction Design

---

## 🧠 Python Concepts Covered

<div align="center">

| Category | Concepts |
|----------|---------|
| **Core Python** | Functions · Loops · Conditionals · Error Handling · File I/O |
| **Data Structures** | Lists · Dictionaries · DataFrames · Series |
| **Data Analysis** | EDA · Aggregation · GroupBy · Pivot Tables · Merging |
| **Data Cleaning** | Missing values · Duplicates · Type conversion · Outlier detection |
| **Visualisation** | Line plots · Bar charts · Heatmaps · Histograms · Scatter plots |
| **API & Web** | REST API calls · JSON parsing · HTTP error handling |
| **OOP** | Classes · Methods · Encapsulation (where applied) |
| **Statistics** | Correlation · Distribution analysis · Descriptive statistics |

</div>

---

## 🛠️ Tech Stack

<div align="center">

![Python](https://img.shields.io/badge/Python%203.x-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge&logo=python&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white)

</div>

| Layer | Tools |
|-------|-------|
| **Language** | Python 3.x |
| **Analysis** | Pandas, NumPy |
| **Visualisation** | Matplotlib, Seaborn |
| **API / Web** | Requests, JSON |
| **Environment** | Jupyter Notebook, VS Code |
| **Output Formats** | `.rar`, `.pdf` |

---

## 📈 Skills Demonstrated

<div align="center">

| Data Analysis | Programming | Application Dev |
|:------------:|:-----------:|:---------------:|
| ✅ Exploratory Data Analysis | ✅ Clean, readable Python code | ✅ API Integration |
| ✅ Data Cleaning & Wrangling | ✅ Function design & modularity | ✅ Chatbot Development |
| ✅ Statistical Analysis | ✅ Error handling & validation | ✅ Interactive CLI apps |
| ✅ Feature Engineering | ✅ OOP principles | ✅ User experience design |
| ✅ Data Visualisation | ✅ Loops & control flow | ✅ Real-time data retrieval |

</div>

---

## 📊 Project Summary

| Project | Domain | Libraries | Complexity |
|---------|--------|-----------|-----------|
| 🛒 Amazon Sales Analysis | E-commerce | Pandas, Matplotlib, Seaborn | ⭐⭐⭐ |
| 👔 HR Analytics | Human Resources | Pandas, Seaborn, NumPy | ⭐⭐⭐ |
| 🤖 Weather Chatbot | Automation / API | Requests, JSON | ⭐⭐⭐ |
| 🎮 Number Guessing Game | Core Python | Built-in modules | ⭐⭐ |

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/FarisDataAnalysts/Python_Projects.git

# Navigate to the project directory
cd Python_Projects

# Install required libraries
pip install pandas numpy matplotlib seaborn requests jupyter

# Launch Jupyter Notebook (for analysis projects)
jupyter notebook

# Run the chatbot or game directly
python weather_chatbot.py
python number_guessing_game.py
```

> **Note:** For `Amazon_Sale_Analysis.rar`, extract the archive first using WinRAR or 7-Zip before opening the notebook.

---

## 🔗 Explore More Projects

[![SQL Projects](https://img.shields.io/badge/🗄️_SQL%20Projects-CC2927?style=for-the-badge&logo=mysql&logoColor=white)](https://github.com/FarisDataAnalysts/SQL_Projects)
[![Power BI Projects](https://img.shields.io/badge/📊_Power%20BI%20Projects-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://github.com/FarisDataAnalysts/Power-BI_Projects)
[![Portfolio](https://img.shields.io/badge/👤_Main%20Portfolio-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/FarisDataAnalysts)

---

## 📫 Connect With Me

<div align="center">

[![Email](https://img.shields.io/badge/Gmail-farisbilal96@gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:farisbilal96@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-FarisDataAnalysts-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/FarisDataAnalysts)

---

⭐ **Found something useful? Star this repo — it helps others discover this work too!**

*"Every line of Python should answer a question or solve a problem."*

*Last Updated: April 2026*

</div>
