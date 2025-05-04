---
layout: post
title: "Peeking into the Developer World: Insights from Stack Overflow's 2024 Survey" 
---

Hi there! This time, I explored the data from the annual survey conducted by Stack Overflow (2024 edition), a site used by developers worldwide, to look for developer trends. 
I'd like to share some of the analysis I worked on as part of Udacity's Data Science program!

---

## What I Wanted to Know from this Analysis (Questions of Interest)

In this analysis, I focused particularly on these three questions:

1.  **What programming languages are commonly used right now?**
2.  **How much do developer salaries differ by country?**
3.  **What characteristics are associated with higher salaries? (Experience? Education?)**

---

## What the Analysis Revealed (Findings)

Let's take a look at what the data showed, along with some graphs!

### 1. Commonly Used Programming Languages

First, here are the top 10 programming languages that developers reported using professionally in the past year.

![Top 10 Programming Languages](../assets/images/q1_languages_plot.png)
*Graph 1: Top 10 Most Commonly Used Programming Languages*

As expected, **JavaScript** is the most popular! HTML/CSS, often used for website creation, and **Python**, popular in data analysis and AI, are also high on the list. 
This shows that web development and data-related technologies are widely used.

### 2. Salary Differences by Country

Next, let's look at the median annual salary (the value for the person in the middle when everyone is lined up by salary) by country on a world map. (Note: Countries with too few responses were excluded).

![Median Compensation by Country Map](../assets/images/q2_country_map.png)
*Graph 2: Median Annual Compensation by Country (Darker color means higher)*

The map clearly shows a trend where salaries tend to be higher in North American and European countries like the **United States** and **Switzerland**. On the other hand, countries in Asia and South America showed relatively lower tendencies.

*(Optional: Add a screenshot of the boxplot and mention the variation)*
![Compensation Distribution by Country Boxplot](../assets/images/q2_country_dist.png)
*Graph 3: Annual Compensation Distribution for Key Countries (Box Plot)*

The box plot also shows that the *range* or spread of salaries varies from country to country.

### 3. Factors Related to Higher Salaries

Finally, I explored what factors might be related to higher salaries. Let's look specifically at the relationship between "years of experience" and salary.

![Compensation vs Years of Professional Experience](../assets/images/q3_experience_scatter.png)
*Graph 4: Relationship between Years of Professional Experience and Annual Compensation (Scatter Plot)*

Looking at this graph, we can see a trend where **longer professional experience tends to correlate with higher annual income**. However, it's also clear that there's quite a wide range of salaries even for the same level of experience.

I also tried building a simple prediction model, but it seems difficult to explain salaries fully just based on factors like experience, country, and education. It suggests that many other factors (like specific technologies used, company size, individual skills, etc.) are involved in determining salary in complex ways.

```
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import root_mean_squared_error, r2_score

# Define features based on selection justification above
features_for_model = [
    'WorkExp', 'YearsCodePro', # Selected Numeric
    'EdLevel', 'DevType', 'Country', 'RemoteWork', 'OrgSize' # Selected Categorical
]

# Ensure df_cleaned is ready (use the dataframe prepared in section 4)
X = df_cleaned[features_for_model].copy()
y = df_cleaned['ConvertedCompYearly']

# --- One-Hot Encoding (Should ideally be in Data Prep, but can be here if needed just before splitting) ---
# Rationale: Convert categorical features into a format suitable for the linear model.
categorical_cols_model = X.select_dtypes(include='object').columns
print(f"\n--- One-Hot Encoding features for model: {list(categorical_cols_model)} ---")
X = pd.get_dummies(X, columns=categorical_cols_model, drop_first=True)
print(f"Shape of X after One-Hot Encoding: {X.shape}")

# --- Final Check for NaNs in final X before splitting ---
# Rationale: Crucial check to ensure no NaNs remain after all preprocessing.
if X.isnull().sum().sum() > 0:
    print("Warning! NaNs detected in final feature matrix X:")
    print(X.isnull().sum()[X.isnull().sum() > 0])
    # Add emergency handling if needed, e.g., X.fillna(0, inplace=True)
else:
    print("Final feature matrix X contains no NaNs.")

# --- データの分割 ---
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# --- モデルのトレーニング（Linear Regression） ---
lr_model = LinearRegression()
lr_model.fit(X_train, y_train)

# --- 予測と評価 ---
y_pred = lr_model.predict(X_test)
rmse = root_mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f"\nLinear Regression RMSE: {rmse:.2f}")
print(f"Linear Regression R-squared: {r2:.2f}")
```

```
--- One-Hot Encoding features for model: ['EdLevel', 'DevType', 'Country', 'RemoteWork', 'OrgSize'] ---
Shape of X after One-Hot Encoding: (23435, 221)
Final feature matrix X contains no NaNs.

Linear Regression RMSE: 91018.08
Linear Regression R-squared: 0.19
```

---

## Conclusion

From this analysis, I found that:

*   Web development technologies remain very popular.
*   There are significant salary differences depending on the country where developers work.
*   Years of professional experience are strongly related to salary.

At the same time, I felt that the way salaries are determined seems quite complex.

Data analysis is interesting! I look forward to exploring more data in the future.

*(Optional: Link to the project repository)*
You can find the detailed analysis code on the [GitHub repository](https://github.com/keadachik/udacity-dsblogpost).

---
