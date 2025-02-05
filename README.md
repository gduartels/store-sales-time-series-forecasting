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

## Key Considerations for Evaluators

- **Custom Model Architecture:** Emphasis on manual feature engineering and model tuning over pre-built solutions.

- **Business Context Integration:** Handling of Ecuador-specific factors (oil prices, holidays).

- **Scalability:** Design choices balancing granularity (store-family level) and computational efficiency.
