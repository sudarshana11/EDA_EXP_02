# Experiment 2: Netflix Shows & Movies Analysis

```text
Name: Akshaya N 
Reg.No: 212223050003 
```

## Aim
To analyze the Netflix titles dataset to understand the distribution of content types (Movies vs. TV Shows), identify the top content-producing countries, and visualize the trends in content release years.

## Algorithm / Procedure

1. **Load Data**  
   - Import the `netflix_titles.csv` dataset using Pandas.

2. **Data Inspection**  
   - Use `.head()`, `.info()`, and `.describe()` to understand the dataset structure and check for missing values.

3. **Content Analysis**  
   - Count the number of unique content types: `"Movie"` and `"TV Show"`.

4. **Country Analysis**  
   - Handle missing values in the `country` column.  
   - Split entries containing multiple countries (e.g., `"USA, UK"`) into individual rows.  
   - Count occurrences to find the top contributing countries.

5. **Trend Analysis**  
   - Create a pivot table to aggregate the count of shows released per year, separated by type.

6. **Visualization**  
   - Plot a bar chart for content type distribution.  
   - Plot a bar chart for content released per year (2000–2020).  
   - Plot a line chart to show the growth trend over time.


## Program (Python)

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Load Dataset
url = 'https://raw.githubusercontent.com/allenkong221/netflix-titles-dataset/main/netflix_titles.csv'
df = pd.read_csv(url)

# 2. Inspect Data
print(df.head())
print(df.shape)
print(df.info())

# 3. Content Type Analysis
type_counts = df['type'].value_counts()
print("\nCounts by type:\n", type_counts)

# 4. Country Analysis (Preprocessing)
df_country = df.dropna(subset=['country']).copy()

# Split entries with multiple countries
df_country['country_list'] = df_country['country'].str.split(r',\s*')
df_exploded = df_country.explode('country_list')
df_exploded['country_list'] = df_exploded['country_list'].str.strip()

country_counts = df_exploded['country_list'].value_counts().reset_index()
country_counts.columns = ['country', 'count']
print("\nTop contributing countries:\n", country_counts.head(10))

# 5. Pivot Table for Trends
pivot = pd.pivot_table(
    df,
    index='release_year',
    columns='type',
    values='show_id',
    aggfunc='count',
    fill_value=0
)

# 6. Visualization
sns.set_style("whitegrid")

# Plot 1: Movies vs TV Shows
plt.figure(figsize=(6, 4))
sns.barplot(x=type_counts.index, y=type_counts.values, palette='pastel')
plt.title("Count of Movies vs TV Shows")
plt.xlabel("Type")
plt.ylabel("Count")
plt.tight_layout()
plt.show()

# Plot 2: Content by Release Year (Recent History)
if 2000 in pivot.index:
    years_to_plot = pivot.loc[2000:2020]
else:
    years_to_plot = pivot.iloc[-20:]

years_to_plot.plot(kind='bar', figsize=(12, 6), stacked=True)
plt.title("Count by Release Year and Type (2000-2020)")
plt.xlabel("Release Year")
plt.ylabel("Count")
plt.legend(title="Type")
plt.tight_layout()
plt.show()

# Plot 3: Growth Trend Line
plt.figure(figsize=(12, 6))
sns.lineplot(data=pivot)
plt.title("Trend of Movies vs TV Shows Over Years")
plt.xlabel("Release Year")
plt.ylabel("Count")
plt.legend(title='Type')
plt.tight_layout()
plt.show()
````

## Output
<img width="1680" height="1050" alt="1" src="https://github.com/user-attachments/assets/24df4906-0362-443c-a6fc-b265ec67c0e7" />
<img width="1680" height="1050" alt="2" src="https://github.com/user-attachments/assets/251076eb-9a47-41f7-9046-08f222938f93" />
<img width="1680" height="1050" alt="3" src="https://github.com/user-attachments/assets/0db21b32-0cf7-41c3-bc6b-4e6891b645c4" />
<img width="1680" height="1050" alt="4" src="https://github.com/user-attachments/assets/d992a279-1fee-43de-b816-43c859722969" />
<img width="1680" height="1050" alt="5" src="https://github.com/user-attachments/assets/1200c33c-6251-4267-9ae4-1a0ea2a1610b" />
<img width="1680" height="1050" alt="6" src="https://github.com/user-attachments/assets/59d9ee5e-1f2b-4d7a-a853-d191e3b8eb2f" />
(Visual outputs shown as bar charts and line charts in the referenced screenshots.)

## Inference

> ### Inference
>
> * **Dominance of Movies:**
>   There are significantly more Movies than TV Shows in the Netflix library.
>
> * **Geographical Leaders:**
>   The United States is the largest producer of content, followed by India and the United Kingdom.
>
> * **Exponential Growth:**
>   There was a massive surge in content production and acquisition starting around 2015–2016, correlating with the global expansion of streaming services.
>
> * **Recent Trends:**
>   While movies have historically dominated, the gap between Movies and TV Shows has been narrowing in recent years as original series production has increased.

---

## Result

The Netflix dataset was successfully analyzed to determine content distribution and trends.
This analysis helps in understanding the global streaming landscape and can guide content planning and investment strategies.

```
```
