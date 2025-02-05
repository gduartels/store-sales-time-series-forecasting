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
|── data_results/ # Modeling results
└── README.md # Project documentation
```

## Notebook Summaries

### `01-Cleaning.ipynb`
*Content Overview*  
*(Summary to be added by the user)*  

### `02-EDA.ipynb`
*Content Overview*  
*(Summary to be added by the user)*  

### `03-SARIMA.ipynb`
*Content Overview*  
*(Summary to be added by the user)*  

### `04-Feature Enginnering.ipynb`
*Content Overview*  
*(Summary to be added by the user)*  

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
