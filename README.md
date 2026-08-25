# Zomato Restaurant Data Analysis

An Exploratory Data Analysis (EDA) of Zomato's restaurant dataset using Python to uncover customer preferences, pricing dynamics, and dining trends in the food industry.

---

## 📌 Problem Statement

Understanding customer preferences and restaurant trends is vital for making informed business decisions in the food industry. This project analyzes a sample dataset of 148 restaurants from Zomato to address key analytical questions:

1. **Service Mode:** Do more restaurants provide online delivery compared to offline services?
2. **Customer Preferences:** Which types of restaurants are most favored by the general public?
3. **Budget Trends:** What price range do couples prefer for dining out?
4. **Rating Dynamics:** How do ratings compare between restaurants offering online delivery versus offline dining?

---

## 🛠️ Tech Stack & Dependencies

- **Language:** Python 3.x
- **Data Manipulation:** `pandas`, `numpy`
- **Data Visualization:** `matplotlib`, `seaborn`

To install the required dependencies:
```bash
pip install pandas numpy matplotlib seaborn
```

---

## 📊 Workflow & Data Pipeline

### Step 1: Library Import
Import necessary Python libraries for data processing and visual analytics.
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### Step 2: Dataset Loading
Load the dataset into a Pandas DataFrame.
```python
dataframe = pd.read_csv("Zomato-data.csv")
print(dataframe.head())
```

### Step 3: Data Cleaning & Preprocessing
1. **Rating Normalization:** Convert the string-formatted `rate` column (e.g., `4.1/5`) into standard numeric floats using a custom processing function (`handleRate`).
   ```python
   def handleRate(value):
       value = str(value).split('/')
       value = value[0]
       return float(value)

   dataframe['rate'] = dataframe['rate'].apply(handleRate)
   ```
2. **Data Inspection:** Inspect structural details with `dataframe.info()` and check for missing values using `dataframe.isnull().sum()`. (The dataset contains 148 non-null entries across 7 columns).

---

## 💡 Key Analysis & Visual Insights

### 1. Restaurant Distribution by Category
- **Method:** `sns.countplot(x=dataframe['listed_in(type)'], color='red')`
- **Insight:** The vast majority of listed entries fall under the **Dining** category, outnumbering Cafes, Buffets, and other types.

### 2. Total Engagement (Votes) by Category
- **Method:** Grouped summation of votes plotted as a line chart with markers (`plt.plot(result, c='magenta', marker='o')`).
- **Insight:** **Dining** restaurants receive the highest cumulative votes (~20,000+ votes), indicating maximum consumer engagement.

### 3. Most Popular Restaurant
- **Method:** Identify maximum vote count via `dataframe['votes'].max()`.
- **Finding:** **Empire Restaurant** emerged as the single most voted restaurant in the dataset.

### 4. Online Delivery Availability
- **Method:** Count plot on `online_order` availability (`sns.countplot(x=dataframe['online_order'], color='orange')`).
- **Insight:** A majority of the surveyed restaurants do **not** accept online orders (approx. 90 offline vs 58 online).

### 5. Rating Distribution
- **Method:** Histogram analysis (`plt.hist(dataframe['rate'], bins=5, color='purple')`).
- **Insight:** Most restaurants receive ratings heavily concentrated between **3.5 and 4.0**.

### 6. Approximate Cost for Couples
- **Method:** Distribution plot on `approx_cost(for two people)`.
- **Insight:** The modal price point preferred by couples is **300 Rupees**, making budget-friendly dining options the most prevalent.

### 7. Online vs. Offline Ratings Comparison
- **Method:** Boxplot visualization (`sns.boxplot(x='online_order', y='rate', data=dataframe, color='lime')`).
- **Insight:** Restaurants offering **online delivery achieve higher overall ratings** (median rating around 3.9) compared to offline-only restaurants (median rating around 3.4).

### 8. Order Preference vs. Restaurant Type (Heatmap Analysis)
- **Method:** Pivot table matrix analyzed via Seaborn heatmap (`sns.heatmap(pivot_table, annot=True, cmap='YlGnBu', fmt='d')`).
- **Insight:** 
  - **Dining** restaurants primarily operate offline (77 offline vs 33 online).
  - **Cafes** skew towards online delivery orders (15 online vs 8 offline).
  - *Conclusion:* Customers prefer in-person dining for general restaurants but prefer online delivery when ordering from cafes.

---

## 📈 Summary Insights

| Metric / Dimension | Dominant Trend / Outcome |
| :--- | :--- |
| **Most Popular Category** | Dining (Highest count & vote volume) |
| **Top Voted Restaurant** | Empire Restaurant |
| **Preferred Budget (Couples)** | ₹300 for two people |
| **Delivery vs Ratings** | Online delivery restaurants maintain higher ratings |
| **Ordering Behavior** | Offline for Dining, Online for Cafes |
