# Unemployment Rate Analysis — India (Covid-19 Impact)

Analysis of unemployment trends in India using Python, focused on data cleaning, exploratory data analysis, and quantifying the impact of Covid-19 on the labour market. Includes seasonal pattern detection and policy-relevant insights.

## Datasets

| File | Coverage | Granularity |
|---|---|---|
| `Unemployment_in_India.csv` | May 2019 – Jun 2020 | State-level, split by Rural/Urban |
| `Unemployment_Rate_upto_11_2020.csv` | Jan 2020 – Oct 2020 | State-level aggregate, includes Zone + lat/long |

Source: publicly available Indian unemployment datasets (CMIE-style survey data).

## Approach

1. **Cleaning** — stripped whitespace from headers/values, dropped blank rows, parsed dates, standardized column names across both files.
2. **Merging** — the two files have different granularity and an overlapping date range (Jan–Jun 2020), so they were combined into two purpose-built datasets rather than a single naive concat:
   - `df_area`: Rural/Urban level detail (File 1 only)
   - `df_state`: continuous state-level timeline, May 2019–Oct 2020 (File 1 aggregated + File 2 appended only for months beyond File 1's range)
3. **EDA** — national and state-level trends, rural vs urban comparison, labour participation rate overlay.
4. **Covid-19 impact** — data segmented into Pre-Covid, Lockdown Peak (Mar–Jun 2020), and Recovery periods for comparison.
5. **Seasonality** — month-wise boxplots and `statsmodels` seasonal decomposition.

## Key Findings

- Unemployment rose from a pre-Covid baseline of **9.59%** to a peak of **25.62% in May 2020**.
- By **October 2020**, the rate had recovered to **8.03%** — below the pre-Covid baseline, indicating a sharp but largely temporary (V-shaped) shock rather than a structural one.
- Rural and urban areas were affected differently during the lockdown period.
- Certain states were hit substantially harder than others at the peak, pointing to differences in sectoral exposure (informal labour, tourism, manufacturing).
- Recurring month-to-month patterns suggest seasonal effects independent of Covid-19.

## Tech Stack

- Python 3
- pandas, numpy
- matplotlib, seaborn
- statsmodels (seasonal decomposition)
