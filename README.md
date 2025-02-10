# Favorita Store Sales Forecasting

## Project Overview
**Objective:** Develop a custom multivariate time series model to forecast sales for Favorita stores in Ecuador. 

**Competition Context:**  
[Kaggle Store Sales - Time Series Forecasting](https://www.kaggle.com/competitions/store-sales-time-series-forecasting)  
*Evaluation Metric:* Root Mean Squared Logarithmic Error (RMSLE).

**Key Challenges:**
- Complex temporal patterns (daily, weekly, seasonal trends).
- External factors: oil prices, holidays, earthquakes.
- Hierarchical structure (sales by store-family-product).

---

## Dataset Description
Data sourced from Kaggle includes:
- `train.csv`: Historical sales (2013–2017), store/product metadata, promotions.
- `test.csv`: Forecast target for 15 days post-training period.
- Supplementary data: oil prices, holiday events, store metadata.

**Notable Features:**
- `onpromotion`: Promotional impact on sales.
- `transferred` holidays: Affect typical holiday patterns.
- Non-traditional shocks (e.g., 2016 earthquake).

---

## Repository Structure
```bash
├── 01-Cleaning.ipynb # Data preprocessing & consolidation
├── 02-EDA.ipynb # Exploratory analysis & insights
├── 03-SARIMA.ipynb # Baseline univariate time series tests
├── 04-Feature Engineering.ipynb # Feature creation & lag variables
├── 05-Modelling.ipynb # Multivariate model development & validation
├── data/ # Raw and processed datasets
├── data_results/ # Modelling results
└── README.md # Project documentation
```

## Notebook Summaries

### `01-Cleaning.ipynb`

#### Key Actions:

1. **Loading and Initial Inspection:**
    - Verification of dimensions, data types, unique values, and missing values in all datasets (`train`, `test`, `oil`, `holidays`, `stores`, `transactions`).
2. **Date Handling:**
    - Conversion of `date` columns to `datetime` type.
    - Filling of missing dates via daily resampling (`1D`) to ensure temporal continuity:
      - **Train/Test:** Filling by `store_nbr` × `family` combination (forward fill).
      - **Oil**: Interpolation of missing prices (forward/backward fill).
      - **Transactions:** Expansion to all possible dates (2013–2017) per store, with missing transactions filled with 0.
3. **External Data:**
    - **Holidays:** Identification of transferred holidays and special events.
    - **Stores:** Validation of metadata (city, type, cluster) without missing values.
4. **Output:**
    - Generation of cleaned datasets: `train_clean.csv`, `oil_clean.csv`, `transactions_clean.csv`.

#### Key Techniques:

- Daily resampling + forward fill for time series.
- Handling of missing values (interpolation for `oil`, filling with 0 for `transactions`).
- Ensuring integrity in `store` × `family` × `date` combinations.

*Note:* Training/test data were temporally aligned to avoid gaps, critical for time series models.


### `02-EDA.ipynb`

This notebook performs an in-depth Exploratory Data Analysis (EDA) aimed at understanding the behavior of Favorita store sales and identifying patterns, trends, and anomalies that could influence forecasting. The main points covered include:

1. **Descriptive Statistics and Data Distribution:**
    - Calculation of measures of central tendency and dispersion for key variables, such as sales, promotions, and transactions.
    - Analysis of the data distribution by store and product family, allowing for the identification of differences and specific behaviors within each segment.
2. **Time Series Visualization:**
    - Creation of line charts that display the daily evolution of sales, highlighting seasonal patterns (daily, weekly, and annual cycles) and long-term trends.
    - Comparison of time series segmented by store and product family, facilitating the identification of specific seasonalities and peculiarities.
3. **Outlier Detection and Anomaly Analysis:**
    - Identification of abrupt peaks and drops in sales, relating these events to external factors (e.g., holidays, promotions, and atypical events such as the earthquake).
    - Evaluation of the impact these outliers have on the overall behavior of the series.
4. **Correlation Analysis:**
    - Exploration of the relationships between sales and other relevant variables, such as oil prices, the promotion indicator (`onpromotion`), and transaction volumes.
    - Use of heatmaps and scatter plots to visualize and quantify the strength of these correlations.
5. **Insights for Feature Engineering:**
    - The patterns identified during the EDA, such as seasonalities and the influence of external factors, provided the foundation for creating new features (e.g., lag variables, moving averages, and seasonal indicators) that were later utilized in the development of the multivariate model.
   

### `03-SARIMA.ipynb`

This notebook explores a **baseline univariate time series model** using *SARIMA* (Seasonal AutoRegressive Integrated Moving Average) to forecast total sales across Favorita stores. The primary goal is to evaluate the feasibility of traditional time series methods before advancing to more complex multivariate models.

1. **Data Preparation:**
    - The dataset is loaded from `train_clean.csv`, with sales data aggregated at the daily level.
    - The time series is checked for missing values and preprocessed for modeling.

2. **Exploratory Time Series Analysis:**
    - Summary statistics and visualizations of total sales over time.
     -Identification of key seasonal patterns (weekly, monthly, and yearly trends).
    - Detection of outliers and extreme values affecting sales.

3. **SARIMA Model Experiments:**

    - Multiple SARIMA models were tested with different parameter combinations.
    - Grid Search Optimization was applied to determine the best `(p, d, q) × (P, D, Q, s)` configuration.
   - Model selection was based on Akaike Information Criterion (AIC) and Root Mean Squared Logarithmic Error (RMSLE).

4. **Forecasting and Model Evaluation:**

    - Time-based cross-validation using `TimeSeriesSplit`.
    - Comparison of predicted vs. actual sales.
    - Error analysis to assess the model's ability to capture seasonality and trend components.
   
#### Key Findings:

- SARIMA performed reasonably well for short-term forecasting but struggled with long-term trends and external shocks.
- The model highlighted strong weekly and yearly seasonal patterns.
- Given the limitations of univariate approaches, further enhancements were needed through feature engineering and multivariate modeling.

This notebook served as an initial benchmark for forecasting sales and provided valuable insights into the temporal structure of the data before proceeding to more sophisticated machine learning models.

### `04-Feature Enginnering.ipynb`

This notebook focuses on **creating new features** to enhance predictive performance in the sales forecasting model. The feature engineering process was guided by insights from the Exploratory Data Analysis (EDA) and the limitations observed in the SARIMA model.

- **Temporal Features:**
    - Extraction of **year, month, day, and day of the week** from the `date` column.
    - Creation of a **business day indicator** to distinguish weekdays from weekends.
- **Lag Features:**
    - **Rolling window statistics** (e.g., moving averages, standard deviations) to capture historical sales trends.
    - **Lagged sales values** at different time intervals (e.g., 7-day, 14-day, and 30-day lags) to incorporate temporal dependencies.
- **Seasonality Indicators:**
    - Monthly and yearly **sinusoidal transformations** to model cyclical patterns.
    - Encoding of specific **holiday and event effects** using external calendar data.
- **Store-Level and Promotion Features:**
    - Aggregated **store-level sales trends** to account for location-specific dynamics.
    - Inclusion of **onpromotion** data to quantify the impact of promotions on sales.
- **Macroeconomic & External Data:**
    - Integration of **oil price data** as a potential macroeconomic indicator.
    - Analysis of the effect of the **2016 earthquake** on sales behavior.

This feature set laid the foundation for multivariate modeling in the next phase of the project, ensuring the predictive model could leverage structured temporal patterns and external factors effectively.

### `05-Modelling.ipynb`
*Content Overview*  
*(Summary to be added by the user)*  

---

## Setup
**Dependencies:**  
- Python 3.8+

```bash
pip install -r requirements.txt
```

## Key Considerations for Evaluators

- **Custom Model Architecture:** Emphasis on manual feature engineering and model tuning over pre-built solutions.

- **Business Context Integration:** Handling of Ecuador-specific factors (oil prices, holidays).

- **Scalability:** Design choices balancing granularity (store-family level) and computational efficiency.
