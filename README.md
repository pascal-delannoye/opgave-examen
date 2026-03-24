# Belgian Birth Data Analysis - Data Science Exam

## Project Overview

This project performs a comprehensive analysis of simulated data on births in Belgium during 2019. The dataset contains 366 CSV files (365 valid daily files + 1 invalid `2019-2-29.csv`) with information about births, expected dates, names, and municipalities.

## Objectives

The exam covers three major research investigations, preceded by data loading and exploratory analysis:

1. **Data Loading & EDA**: Consolidate daily CSV files, detect and remove outliers, analyse temporal patterns (weekly, monthly, seasonal)
2. **Onderzoek 1 — Unisex Names**: Identify names used for both genders, define "truly unisex" names, and compare popularity
3. **Onderzoek 2 — Birth Date Accuracy**: Compare expected vs. actual birth dates, analyse edge effects, and examine municipality-level patterns
4. **Onderzoek 3 — Name Frequency Scaling**: Investigate the non-linear (power-law) relationship between sample size and name diversity

## Dataset

- **Source**: 366 CSV files named in format `YYYY-M-D.csv` (non-zero-padded)
- **Time Period**: January 1 – December 31, 2019
- **Note**: `2019-2-29.csv` is invalid (2019 is not a leap year) and is skipped during loading
- **Columns**:
  - `gemeente`: Municipality where birth occurred
  - `naam`: First name of child
  - `geslacht`: Gender (Mannelijk/Vrouwelijk)
  - `verwachte datum`: Expected birth date (MM/DD/YYYY format)

## Key Findings

### Data Loading & Outlier Detection
- Successfully loaded 365 valid daily files (skipped invalid Feb 29)
- Outlier detection via z-scores (|z| > 3): identified **2 extreme days**
  - **Jan 1** (dag 1): 534 births (z = 6.0)
  - **Jul 1** (dag 182): 923 births (z = 16.8)
- Both days removed as suspected data corruption (double registration)

### Temporal Patterns (EDA)
- Weekly smoothing reveals seasonal trend with summer dip
- Clear weekday effect visible in bar charts
- Monthly confidence interval barplot shows consistent birth rates
- Weekday × season interaction analysed via pointplot

### Onderzoek 1: Unisex Names
- Names used for both genders identified
- "Truly unisex" defined as: x ≤ 1.5y and y ≤ 1.5x
- Popularity comparison: percentage of M vs F births with a unisex name
- Stacked horizontal bar chart visualises gender split per unisex name

### Onderzoek 2: Birth Date Accuracy
- Dual line plot: actual vs expected births per day
- Edge effects at start/end of year explained (boundary artifact)
- Histogram of days-early distribution with median and P90 annotated
- Scatter plots for top 8 municipalities with reference line

### Onderzoek 3: Name Frequency Scaling
- Sublinear (power-law) relationship: n_unique ~ n_births^α with α < 1
- Linear regression on freq_per_name for n > 10,000 births
- Log-log regression on all data achieves near-perfect fit (R² ≈ 1.0)
- Validation plots confirm model accuracy

## Installation & Setup

### Prerequisites
- Python 3.7+
- pip or conda package manager

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run the Notebook

```bash
jupyter notebook opgave_v2.ipynb
```

Execute cells sequentially from top to bottom.

## File Structure

```
.
├── opgave_v2.ipynb           # Main Jupyter notebook with all analysis
├── opgave_orig.ipynb         # Original exam template (reference)
├── requirements.txt          # Python package dependencies
├── README.md                 # This file
└── data/                     # CSV files (366 files, 365 valid)
    ├── 2019-1-1.csv
    ├── 2019-1-2.csv
    ├── ...
    └── 2019-12-31.csv
```

## Methods & Tools

- **Data Processing**: pandas, numpy
- **Visualization**: matplotlib, seaborn
- **Regression Analysis**: scikit-learn (LinearRegression)
- **Outlier Detection**: z-score method (|z| > 3)
- **Notebook Environment**: Jupyter / VS Code
4. Package entire directory as `.zip` for distribution

---

**GitHub Repository**: Add link to your GitHub repository here after pushing this code
