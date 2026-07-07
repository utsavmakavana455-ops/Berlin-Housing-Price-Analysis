# Berlin Housing Price Analysis

Exploratory data analysis of the Berlin housing market, examining how property size and living area relate to sale price. The project covers data cleaning, outlier treatment, feature engineering, and correlation analysis using Python.

## Dataset

- **Source file:** `BerlinHousing4049.csv`
- **Size:** 9,999 property records, 11 columns
- **Columns:** `price`, `bedrooms`, `bathrooms`, `sqft_living`, `sqft_total`, `floors`, `condition`, `grade`, `built`, `renovated`, `living_area_sqft`

## Tools Used

- **pandas** — data loading, cleaning, aggregation
- **numpy** — numerical operations
- **matplotlib / seaborn** — visualizations
- **scipy.stats** — Pearson correlation and significance testing

## Project Workflow

### 1. Data Loading & Initial Inspection
Loaded the dataset with an auto-detecting reader (handles multiple encodings and delimiters). Checked shape, data types, duplicates, missing values, and descriptive statistics.

### 2. Data Cleaning
- Removed 2 duplicate rows
- Dropped rows with missing `price` (the target variable)
- Imputed missing values: median for `bedrooms`, `bathrooms`, `sqft_total`, `built`; mode for `condition`
- Merged `sqft_living` and `living_area_sqft` into a single unified `living_area` column

### 3. Outlier Detection & Treatment
Applied the IQR method (1.5×IQR rule) and winsorized (capped) rather than removed outliers, preserving all 9,988 rows:

| Column | Outliers Detected |
|---|---|
| `price` | 499 (5.0%) |
| `sqft_total` | 1,194 (12.0%) |
| `living_area` | 253 (2.5%) |

Skewness reduced significantly after capping:
- `price`: 5.01 → 0.95
- `sqft_total`: 14.7 → 0.88

### 4. Feature Engineering
Created four new features: `price_per_sqft`, `property_age`, `is_renovated`, `total_rooms`.

### 5. Exploratory Data Analysis
Tested correlation between price and two size-related variables using Pearson's r:

| Relationship | r | Significance |
|---|---|---|
| Price vs. `sqft_total` | 0.178 | p < 0.001 |
| Price vs. `living_area` | 0.636 | p < 0.001 |

**Key finding:** Living area is a much stronger predictor of price than total square footage, likely because `sqft_total` includes non-living space (garages, land, etc.) that doesn't directly translate to value.





## Author

*Makavana Utsav/25174056*
