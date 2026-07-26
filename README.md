# Experiment 1: EDA in IPL Dataset

```text
Name:Sudarshana S
Reg.No: 212223050054
```

## Aim
To perform Exploratory Data Analysis (EDA) on the Indian Premier League (IPL) matches dataset to derive meaningful insights regarding match statistics, team performance, toss decisions, and venue popularity over various seasons.


## Introduction
Exploratory Data Analysis (EDA) is a crucial first step in understanding any dataset.  
For the **IPL dataset**, EDA helps uncover patterns such as:

- Whether winning the toss influences match outcome  
- Which teams dominate across seasons  
- Which venues host most matches  
- Seasonal trends in number of matches  

Using Python libraries like **Pandas**, **Matplotlib**, and **Seaborn**, these insights can be visualized effectively.


## Algorithm / Procedure

1. **Import Libraries**  
   - `pandas` for data handling  
   - `matplotlib` and `seaborn` for visualization  

2. **Load Dataset**  
   - Load `matches.csv` into a DataFrame  
   - Inspect dataset shape and first few rows  

3. **Matches per Season Analysis**  
   - Group by season  
   - Plot match frequency  

4. **Team Performance Analysis**  
   - Count wins per team  
   - Visualize top performers  

5. **Toss Decision Analysis**  
   - Analyze distribution of bat vs field decisions  

6. **Venue Analysis**  
   - Identify and plot top venues  


## Program (Python)

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Load Dataset
matches = pd.read_csv('matches.csv')
print("Dataset Shape:", matches.shape)
print(matches.head())

# 2. Matches per Season
season_counts = matches['season'].value_counts().sort_index()
print("\nMatches per season:\n", season_counts)

plt.figure(figsize=(10, 5))
sns.barplot(x=season_counts.index, y=season_counts.values, palette="viridis")
plt.title("Number of Matches per Season")
plt.xlabel("Season")
plt.ylabel("Matches")
plt.show()

# 3. Top 5 Winning Teams
winner_counts = matches['winner'].value_counts().head(5)
plt.figure(figsize=(10, 5))
sns.barplot(x=winner_counts.values, y=winner_counts.index, palette="coolwarm")
plt.title("Top 5 Winning Teams")
plt.xlabel("Number of Wins")
plt.show()

# 4. Toss Decisions
toss_counts = matches['toss_decision'].value_counts()
plt.figure(figsize=(6, 4))
sns.barplot(x=toss_counts.index, y=toss_counts.values, palette="pastel")
plt.title("Toss Decision Distribution")
plt.ylabel("Count")
plt.show()

# 5. Top Venues
venue_counts = matches['venue'].value_counts().head(5)
plt.figure(figsize=(12, 6))
sns.barplot(x=venue_counts.values, y=venue_counts.index, palette="magma")
plt.title("Top 5 Venues Hosting Matches")
plt.xlabel("Number of Matches")
plt.show()
```

## Output

<img width="1680" height="1050" alt="1" src="https://github.com/user-attachments/assets/47f3edf4-1ab7-44a4-957e-a09143a66a9b" />
<img width="1680" height="1050" alt="2" src="https://github.com/user-attachments/assets/c32236c6-e7ee-4cb6-9394-5aa46a6ecec2" />
<img width="1680" height="1050" alt="3" src="https://github.com/user-attachments/assets/c56e36b0-7d28-4530-8792-7b0ced262468" />
<img width="1680" height="1050" alt="4" src="https://github.com/user-attachments/assets/b7b154b7-fb85-4550-b0f6-910eaf3e4789" />

> ## **Inference**
> ---
> ### **Season Density**
> Match count varies across seasons, increasing during years featuring more franchises.
>
> ### **Dominant Teams**
> Teams like **Mumbai Indians** and **Chennai Super Kings** consistently top the win charts, showing long-term dominance.
>
> ### **Toss Trends**
> Captains prefer **Fielding first**, often due to the dew factor and the strategic advantage of chasing.
>
> ### **Venue Bias**
> Venues such as **Eden Gardens** and **Wankhede Stadium** host a significantly higher number of matches.


## Result
The Exploratory Data Analysis on the IPL dataset was successfully performed.
Key insights on match distribution, team performance, toss decisions, and venue dominance were extracted and visualized using Python.
