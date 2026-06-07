# Global Tech Products: Executive Sales Performance & Forecast Analysis

## 📊 Dashboard Preview
![Sales Analysis Dashboard](Screenshots/sales_analysis_dashboard.png)

## 🎯 Project Overview & Business Problem
The sales leadership team of a global technology retail corporation required an operational intelligence solution to evaluate historical sales trends, understand customer purchasing behavior, and measure actual performance against target forecasts. 

This project delivers a comprehensive, interactive **one-page executive dashboard** built in Power BI that synthesizes two years of historical sales transactions (2008–2009) alongside a high-level 2009 sales forecast. The final solution empowers the sales department to identify top revenue-driving products, flag underperforming categories, and optimize regional inventory strategies.

---

## 🛠️ Tech Stack & Technical Skills Demonstrated
* **Business Intelligence & Visualization:** Power BI Desktop
* **Data Modeling:** Star Schema Optimization, Granularity Reconciliation, Bridge Tables
* **Data Transformation (Power Query):** Customer data deduplication, error handling, attribute renaming, and data type casting.
* **Calculations & Analytics:** Advanced DAX (Time Intelligence, Dynamic Totals, Divergent Target Variances)

---

## 📐 Data Modeling & Architectural Challenges

### 🔗 Handling Mixed Granularity (Actuals vs. Forecast)
A major technical challenge in this project was connecting the **Sales Transactions** table and the **Forecast** table, as they exist at different granularities:
* **Sales Table:** Low granularity (Daily transactions per specific customer and unique product).
* **Forecast Table:** High granularity (Aggregated targets at the **Brand** and **Country** level for the entire year of 2009).

**Solution Implemented:**
To avoid standard many-to-many relationship traps and prevent artificial data inflation, a robust **Star Schema** was built:
1.  Created a dedicated, marked **Dim_Date** dimension table using DAX to bridge the temporal gaps.
2.  Utilized dimension tables for **Product/Brand** and **Geography/Country** to serve as shared dimensions.
3.  Modeled relationships such that filters flow downstream cleanly from the dimensions to both fact tables, ensuring that 2009 Actuals perfectly align with 2009 Forecasts when sliced by Brand or Country.

---

## 🧪 Advanced DAX Calculations Implemented

To deliver the precise comparative analytics requested by the sales department, the following key metrics were engineered using DAX:

* **Year-over-Year Sales Comparison:**
    ```dax
    2008 Total Sales = 
    CALCULATE(
        [Total Sales], 
        FILTER(ALL('Dim_Date'), 'Dim_Date'[Year] = 2008)
    )
    ```
* **Sales Growth % (2009 vs 2008):**
    ```dax
    Sales Growth % = 
    DIVIDE(
        [2009 Sales] - [2008 Sales], 
        [2008 Sales], 
        0
    )
    ```
* **Actual vs. Forecast Variance %:**
    ```dax
    Forecast Variance % = 
    DIVIDE(
        [2009 Sales Actual] - [2009 Forecast], 
        [2009 Forecast], 
        0
    )
    ```
* **Product Share percentage:**
    ```dax
    Product Share % = 
    DIVIDE(
        [Total Sales], 
        CALCULATE([Total Sales], ALL('Dim_Product')), 
        0
    )
    ```

---

## 💡 Key Business Insights Delivered

* **Growth Performance:** Total sales hit **$83.54M** across the two-year span. However, performance dipped in 2009, showing a **-5.4% decline** (-$2.29M) compared to 2008.
* **Forecast Target Evaluation:** Despite the Year-over-Year decline, the sales team effectively managed realistic targets—beating the 2009 sales forecast by **+4.1%** (an extra +$1.61M over the predicted $39M target).
* **Category Dominance:** "Home Appliances" and "Computers" represent the overwhelming majority of visual real estate in sales share (visualized via Treemap), meaning supply chain health in these categories is critical.
* **Pareto Principle Check:** The Top 10 products account for **$2.98M** which constitutes only **3.57%** of total sales, revealing an incredibly diversified long-tail product catalog rather than heavy reliance on a few single items.
* **Customer Concentration:** Highly concentrated customer behavior is visible in the top tier, led by Customer Code **CS623** at **$2.24M** in historical purchases.

---

## 🚀 How to Interact with this Project
1.  Download the `My_Awesome_Report.pbix` (or `.pbip` directory) from this repository.
2.  Open it in **Power BI Desktop**.
3.  Use the global left-hand filter pane to slice data by **Country** (China, Germany, United States) and **State** to see regional performance update dynamically.

*Alternatively, view my live interactive profile on [Insert your NovyPro or Power BI Publish to Web link here].*
