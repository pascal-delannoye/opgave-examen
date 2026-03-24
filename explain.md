# Explanation of opgave_v2.ipynb

This notebook is a **Python data analysis exam** about simulated Belgian birth data from 2019.

## Structure Overview

The notebook has 3 main parts: **data loading**, **exploratory data analysis (EDA)**, and **research questions**.

---

## Setup (cells 1–3)

Imports pandas, numpy, matplotlib, seaborn, scipy, and sklearn. Defines a `get_season()` helper that maps months to seasons, plus ordered lists for seasons and weekdays.

## Step 1: Data Loading (cells 4–5)

- Reads all CSV files from `data/` — each file is named `YYYY-M-D.csv` (e.g., `2019-1-1.csv`), where the filename **is** the actual birth date.
- Each CSV contains columns: `gemeente` (municipality), `naam` (first name), `geslacht` (gender), `verwachte datum` (expected due date).
- Parses the date from each filename, concatenates all CSVs into one `df_births` DataFrame, and adds `dag_van_jaar` (day-of-year 1–365).
- Validation checks confirm row count, date range, year range, and no missing days.

## Step 2: EDA

**Vraag 1** — Plots births per day-of-year with a red dashed mean line.

**Vraag 2.1** — Outlier detection using **z-scores** (|z| > 3). Identifies days with abnormally high/low birth counts.

**Vraag 2.2** — Removes the 2 most extreme days (suspected data corruption/duplicates), stores them in `df_wrong`, and recreates the cleaned plot as `df_births_clean`.

**Vraag 2.3** — Finds the 8 most extreme days in H2 (day ≥ 183) by deviation from the median — more robust than using the mean.

**Vraag 3.1** — Smooths the daily curve by plotting **average births per day per ISO week** — removes daily noise to reveal weekly trends.

**Vraag 3.2** — Bar chart of **average births per weekday** — tests whether weekends have fewer births.

**Vraag 3.3** — Seaborn `barplot` with **95% confidence intervals** per month, showing both monthly averages and uncertainty.

**Vraag 3.4** — **Pointplot** of weekday × season interaction — shows whether the weekday effect (e.g., weekend dip) is consistent across all four seasons.

## Step 3: Research Questions

### Research 1: Unisex Names (cells 33–39)

- **1.1**: Builds `df_name_gender` (one row per name, counts per gender). Reports names occurring in both genders, with top-3 by male/female/total.
- **1.2**: Defines "truly unisex" as x ≤ 1.5y AND y ≤ 1.5x — filters to `df_real_unisex`.
- **1.3**: Computes % of males vs females carrying a unisex name to see which gender uses them more.
- **1.4**: Horizontal stacked bar chart showing male/female split per unisex name.

### Research 2: Due Date Accuracy (cells 42–48)

- **2.1**: Overlays actual vs expected births per day-of-year on one plot.
- **2.2**: Explains the **edge effect** — expected dates for January births can fall in Dec 2018 (before data range), and December births can have due dates in Jan 2020 (after data range).
- **2.3**: Defines `days_early = expected − actual` (positive = born before due date). Histograms only early births with **median** and **P90** lines.
- **2.4**: Scatterplot of actual vs expected day-of-year for the **8 largest municipalities**, with a red diagonal reference line (perfect prediction). Uses shared axes for fair comparison.

### Research 3: Names vs Births — Sublinear Growth (cells 51–69)

- **3.1 (per municipality)**: Scatter of unique names vs births per municipality — strong correlation.
- **Random sampling**: Draws repeated random samples of increasing size from all names, counting unique names each time.
- **Direct plot**: Shows the curve of unique names vs sample size — initially steep, then flattening (sublinear).
- **Derived variable**: Plots average frequency per name (n_births / n_unique) — becomes approximately linear for n > 10,000.
- **Linear regression** on frequency per name for n > 10,000 — good R².
- **Log-log regression**: Fits log(n_unique) ~ log(n_births), revealing a **power law**: n_unique ≈ c · n_births^α with α < 1, confirming sublinear growth. Near-perfect R².
- **Validation**: Compares predicted vs actual unique names and frequency per name — the power-law model fits well across the full range.
