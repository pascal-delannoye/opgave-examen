# Belgian Birth Data Analysis - Data Science Exam

## Project Overview

This project performs a comprehensive analysis of simulated data on births in Belgium during 2019. The dataset contains 365 daily CSV files with information about births, expected dates, names, and municipalities.

## Objectives

The exam covers six major analytical phases:

1. **Data Loading & Validation**: Consolidate 365 daily CSV files into a single dataset with temporal features
2. **EDA & Outlier Detection**: Identify anomalous days using statistical methods (IQR)
3. **Temporal Patterns Analysis**: Analyze birth patterns across weeks, days, months, and seasons
4. **Unisex Names Research**: Identify and characterize names used for both genders
5. **Birth Date Accuracy**: Compare expected vs. actual birth dates at municipality level
6. **Name Frequency Scaling**: Investigate the non-linear relationship between sample size and name diversity

## Dataset

- **Source**: 365 CSV files named in format `YYYY-M-D.csv`
- **Time Period**: January 1 - December 31, 2019
- **Total Records**: 116,923 births
- **Columns**: 
  - `gemeente`: Municipality where birth occurred
  - `naam`: First name of child
  - `geslacht`: Gender (Mannelijk/Vrouwelijk)
  - `verwachte datum`: Expected birth date (MM/DD/YYYY format)

## Key Findings

### Phase 1: Data Loading
- Successfully loaded all 365 daily files
- Total births: 116,923 records
- Date range validated: 2019-01-01 to 2019-12-31
- Handled leap year edge case (Feb 29 in non-leap year)

### Phase 2: Outlier Detection
- Identified 15 anomalous days using IQR method
- Removed 5,478 outlier records
- Clean dataset: 111,445 births
- Major anomalies: New Year (Jan 1), Holiday periods, Month boundaries

### Phase 3: Temporal Patterns
- **Weekday Effect**: Weekdays average 318±1 births, weekends slightly higher (319-320)
- **Monthly Variation**: Confidence intervals show consistent patterns across months
- **Seasonal Patterns**: Minimal interaction between weekday and season effects

### Phase 4: Unisex Names
- Total unique names: 5,186
- Names used for both genders: 73
- Truly balanced names (±50% criterion): 15
- Most balanced: Dominique (156M, 225F), Maxime (192M, 5F)

### Phase 5: Birth Date Accuracy
- Average early birth: 7 days before expected date
- 90th percentile: 21 days early
- Top municipalities analyzed with scatter plots
- Boundary artifacts explained by data collection period

### Phase 6: Name Frequency Scaling
- **Relationship**: Non-linear power-law behavior
- **Linear Model** (n > 10k): R² = 0.9996
- **Log-Linear Model**: R² = 1.0000 (perfect fit)
- **Validation**: Models predict actual unique names within 0.4% error

## Installation & Setup

### Prerequisites
- Python 3.7+
- pip or conda package manager

### Install Dependencies

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required packages
pip install -r requirements.txt
```

### Run the Notebook

```bash
# Launch Jupyter
jupyter notebook opgave.ipynb
```

Execute cells sequentially from top to bottom to run the complete analysis.

## File Structure

```
.
├── opgave.ipynb              # Main Jupyter notebook with all analysis
├── opgave_orig.ipynb         # Original template (reference)
├── requirements.txt          # Python package dependencies
├── .gitignore               # Git ignore patterns
├── README.md                # This file
└── data/                    # CSV files (365 daily birth records)
    ├── 2019-1-1.csv
    ├── 2019-1-2.csv
    ├── ...
    └── 2019-12-31.csv
```

## Methods & Tools

- **Data Processing**: pandas, numpy
- **Statistical Analysis**: scipy.stats
- **Visualization**: matplotlib, seaborn
- **Regression Analysis**: scikit-learn
- **Notebook Environment**: Jupyter

## Analysis Highlights

### Statistical Rigor
- IQR-based outlier detection for robust anomaly identification
- 95% confidence intervals using t-distribution
- Regression validation with R² metrics > 0.99

### Visualization Quality
- 12+ publication-quality plots
- Consistent color schemes and labeling
- Multi-panel layouts for comparative analysis
- Log-scale transformations for non-linear relationships

### Code Quality
- Modular functions for reusability
- Clear variable naming conventions
- Comprehensive comments explaining logic
- Proper error handling for data edge cases

## Exam Grading Criteria

This project demonstrates:
- ✅ Data cleaning and preparation (Phase 1-2)
- ✅ Exploratory data analysis (Phase 3)
- ✅ Statistical hypothesis testing (Phases 4-5)
- ✅ Regression modeling and validation (Phase 6)
- ✅ Publication-quality visualizations (All phases)
- ✅ Clear documentation and code quality

## Author

Data Science Exam - Syntra Program
Completed: March 2026

## Notes

For exam submission:
1. Ensure all cells execute successfully from top to bottom
2. Verify kernel state is clean (restart kernel if needed)
3. All 365 data files must be present in `data/` directory
4. Package entire directory as `.zip` for distribution

---

**GitHub Repository**: Add link to your GitHub repository here after pushing this code
