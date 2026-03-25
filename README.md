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
