# Prediction-of-Product-Sales
- **Author**: Lara Mohammed Mutair

## Project Overview
The project talks about sales prediction for food items sold at various stores. The goal of this is to help the retailer understand the properties of products and outlets that play crucial roles in increasing sales.
The project covers the full data science workflow: loading and inspecting the data, cleaning and standardizing inconsistent values, handling missing data, and performing exploratory data analysis (EDA) through univariate and multivariate visualizations.

## Dataset

**Features:**

| Feature | Description |
|---------|-------------|
| `Item_Identifier` | Unique ID for each product |
| `Item_Weight` | Weight of the product |
| `Item_Fat_Content` | Type of fat content (Low Fat / Regular) |
| `Item_Visibility` | Percentage of display area allocated to the product in the store |
| `Item_Type` | Product category |
| `Item_MRP` | Maximum Retail Price of the product |
| `Outlet_Identifier` | Unique ID for each store |
| `Outlet_Establishment_Year` | Year the store was established |
| `Outlet_Size` | Physical size of the store |
| `Outlet_Location_Type` | Type of area where the store is located (Tier 1/2/3) |
| `Outlet_Type` | Type of retail store (Supermarket / Grocery Store) |
| `Item_Outlet_Sales` | Target variable: sales of the product in that outlet |


## Methods
 
### Data Preparation
 
**1. Dropped Identifier Columns**
`Item_Identifier` and `Outlet_Identifier` were dropped as they are unique IDs with no predictive value for unseen data.
 
**2. Removed Duplicates**
Checked for duplicate rows and removed any found to ensure data integrity.
 
**3. Fixed Inconsistent Labels in `Item_Fat_Content`**
The column contained 5 variations of only 2 intended values (`"LF"`, `"low fat"` → `"Low Fat"` and `"reg"` → `"Regular"`). All variants were standardized to ensure the model treats them as the same category.
 
**4. Handled Missing Values**
- `Item_Weight` had **17.2% missing values** → imputed using the **median** (robust to outliers) inside a sklearn pipeline.
- `Outlet_Size` had **28.3% missing values** → imputed using the **most frequent value** strategy, as it is an ordinal variable.
**5. Feature Splitting**
Features were divided into three groups for tailored preprocessing:
- **Numeric:** `Item_Weight`, `Item_Visibility`, `Item_MRP`, `Outlet_Establishment_Year` → Imputed (median) + StandardScaler
- **Ordinal:** `Outlet_Size` → Imputed (most frequent) + OrdinalEncoder (Small=0, Medium=1, High=2)
- **Categorical:** `Item_Fat_Content`, `Item_Type`, `Outlet_Location_Type`, `Outlet_Type` → Imputed (most frequent) + OneHotEncoder
**6. Train / Test Split**
Data was split 75% training (6,392 rows) / 25% test (2,131 rows) with a fixed random state for reproducibility.
 
---

## Visualizations
### Univariate Visualization
**Sales Distribution (Histogram)** 
<img width="571" height="432" alt="hist_for_sales" src="https://github.com/user-attachments/assets/d9baf214-fae5-4af4-ad16-61ff7e1abd42" />

The histogram indicates that the majority of sales values fall within the range of 40 to 2000, suggesting that most products generate relatively low to moderate sales.

### Multivariate Visualization
**Sales by Location Type and Outlet Type (Barplot)**
<img width="580" height="461" alt="location and type VS sales" src="https://github.com/user-attachments/assets/4820eb9b-9c8d-4bae-b59d-7fb38aab7d0e" />


The bar plot shows the relationship between location type and sales, with different outlet types represented by different colors.
From the visualization, Supermarket Type3 in Tier 3 locations has the highest average sales, reaching around 3700, which is significantly higher than other outlet types.
Supermarket Type1 shows relatively similar sales across Tier 1, Tier 2, and Tier 3, with sales around 2300
In contrast, Grocery Stores have the lowest sales, with values around 300–350, suggesting that they generate much lower sales compared to supermarkets.


---
 
## Model
 
Three models were trained and evaluated: a baseline Linear Regression, a default Random Forest, and a tuned Random Forest.
 
### Final Model: Tuned Random Forest Regressor
 
The **Tuned Random Forest** was selected as the final model after hyperparameter tuning via `GridSearchCV`.
 
| | MAE | RMSE | R² |
|---|---|---|---|
| **Training Data** | $666.24 | $940.45 | 0.701 |
| **Test Data** | $754.63 | $1,066.85 | 0.587 |
 
**Why Random Forest over Linear Regression?**
Linear Regression achieved R² = 0.561 (train) / 0.567 (test) — both low, indicating underfitting and an inability to capture nonlinear relationships in the data. The default Random Forest improved generalization but suffered from severe overfitting (train R² = 0.938 vs test R² = 0.544). After tuning, overfitting was significantly reduced (train-test R² gap dropped from 0.394 to 0.114).
 
**Model Performance Interpretation:**
The tuned model explains **58.7% of the variance in sales** on unseen data. On average, predictions deviate from actual sales by approximately **$1,067 (RMSE)**. To put this in perspective: if the model predicts sales of $1,900 for a product, the actual value typically falls somewhere between $835 and $2,965. While this level of accuracy is useful for high-level planning, there is still room to improve generalization.
 
**Why RMSE was chosen as the primary metric:**
RMSE was selected because it penalizes large prediction errors more heavily than MAE, making it more sensitive to significant mistakes. Additionally, since RMSE is expressed in the same unit as the target variable (dollars), it is more interpretable for business stakeholders than MSE.
 
---
 
