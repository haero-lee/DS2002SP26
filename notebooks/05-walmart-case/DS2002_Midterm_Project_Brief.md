# DS2002 Midterm Project: Walmart Hurricane Analytics

**University of Virginia | DS2002 Data Science Systems**
**Midterm Group Project — 3 Weeks**

---

## Background

In 2004, Walmart's data science team discovered that Strawberry Pop-Tarts sales surged **sevenfold** before hurricanes hit Florida. This insight — buried inside messy, fragmented point-of-sale data — became company legend and a textbook example of how data pipelines unlock business value.

Your team has been hired as Walmart's data science consultants. A new hurricane is approaching Florida, and leadership needs answers **fast**. You have raw transaction data, store records, product catalogs, distribution center info, and an inventory database — but the data is **messy** and needs serious wrangling before it can tell you anything useful.

You must also enrich your analysis with **real weather data** pulled from a free API.

**Read the full case study** (`Walmart Case.pdf`) before starting. It provides essential context for every question you will answer.

---

## Team Requirements

- **Group size:** 2–4 students
- **Duration:** 3 weeks
- **Language:** Python (all work must be in Python)
- **Environment:** Jupyter Notebook or Kaggle Notebook
- **Required libraries:** `pandas`, `matplotlib` and/or `seaborn`, `sqlite3`, `requests` (for API calls)

---

## Supplied Data Files

You are provided with **5 data files** in the `data/` directory. All files contain **intentional data quality issues** that you must identify and fix.

| File | Format | Description | Approximate Size |
|------|--------|-------------|-----------------|
| `walmart_transactions.csv` | CSV | Point-of-sale transaction records across Florida stores (Sept 2024) | ~25,000 rows |
| `store_locations.csv` | CSV | Walmart store metadata (Florida locations) | ~14 rows |
| `product_catalog.csv` | CSV | Master product/SKU reference list | ~45 rows |
| `distribution_centers.csv` | CSV | Distribution center capacity and logistics | 5 rows |
| `inventory_and_sales.db` | SQLite | Database with `daily_sales_summary` and `inventory_levels` tables | ~7,900 rows total |

### Known Data Issues (You Must Discover and Fix These)

The data is messy on purpose. Expect problems such as:

- Duplicate records
- Missing values (empty strings, "NULL", "N/A", NaN)
- Inconsistent date/time formats
- The same product appearing under **multiple SKUs and product names**
- Inconsistent capitalization and spacing
- Category naming inconsistencies
- Data type issues (numbers stored as strings, prices with `$` symbols)
- Negative quantities (data entry errors)
- Store ID format inconsistencies across files
- Timezone misalignment between weather data and sales data

---

## Weather API Requirement

You **must** pull real weather data from a **free API** and integrate it into your analysis. This is not optional — Question 3 depends on it entirely, and weather context strengthens your answers to other questions.

### Suggested Free Weather APIs (Pick One)

1. **Open-Meteo** — [https://open-meteo.com/](https://open-meteo.com/)
   - Completely free, no API key required
   - Excellent historical weather data (temperature, wind speed, precipitation)
   - Simple REST API with JSON responses
   - *Recommended for ease of use*

2. **NOAA Climate Data Online** — [https://www.ncdc.noaa.gov/cdo-web/webservices/v2](https://www.ncdc.noaa.gov/cdo-web/webservices/v2)
   - Free with token registration
   - Official U.S. government weather and hurricane data
   - Rich historical dataset

3. **Visual Crossing Weather** — [https://www.visualcrossing.com/weather-api](https://www.visualcrossing.com/weather-api)
   - Free tier: 1,000 records/day
   - Clean JSON/CSV responses
   - Good documentation and tutorials

4. **OpenWeatherMap** — [https://openweathermap.org/api](https://openweathermap.org/api)
   - Free tier available
   - Widely documented with community examples
   - Historical data available

### What You Must Demonstrate

- Python code that calls the API (using `requests` or similar)
- Parsing the API response into a pandas DataFrame
- Joining weather data with your sales/transaction data
- Handling timezone alignment (weather data may be in UTC; sales data is in EST)

---

## Analytical Questions

Your notebook must answer all 5 questions below. Each answer should include **code, a visualization, and a written explanation** in markdown cells.

### Question 1: Demand Surge Identification

> Which product categories experienced the greatest sales surge in the 7 days before hurricane landfall compared to the prior baseline period? Quantify the percentage increase and visualize the daily trend for the top 5 categories.

**Requires:** Cleaning transaction data (deduplication, fixing SKUs, fixing timestamps), grouping by category, computing baseline vs. surge periods, line chart or bar chart.

---

### Question 2: The Pop-Tarts Effect (SKU Consolidation)

> After standardizing all Pop-Tart SKU variants into a single product, what is the true daily sales volume? How does the uncleaned (fragmented) view compare to the cleaned (consolidated) view? What business decisions would differ between the two views?

**Requires:** Building an SKU mapping table, consolidating fragmented products, side-by-side visualization (before vs. after cleaning), written analysis of business impact.

---

### Question 3: Weather Correlation Analysis

> Using weather data pulled from your chosen free API, how do specific weather indicators (wind speed, precipitation, barometric pressure) correlate with daily sales volume across categories? Is there a detectable lag between weather severity escalation and purchasing spikes?

**Requires:** Weather API integration, timestamp/timezone alignment, correlation analysis (scatter plot, heatmap, or time-series overlay), lag analysis discussion.

---

### Question 4: Store-Level Geographic Patterns

> Do all Florida store locations experience the same surge patterns, or do stores closer to the predicted hurricane path show earlier and larger spikes? Identify any stores that appear to be outliers.

**Requires:** Joining store location data with transactions, geographic grouping, comparing surge timing and magnitude across stores, bar chart or grouped comparison, outlier identification.

---

### Question 5: Signal vs. Artifact — The Board Games Investigation

> The board games/entertainment category shows a +250% sales increase. Using the SQLite inventory and sales database, investigate whether this is a genuine demand signal or a data artifact (e.g., SKU miscoding, category lumping, inventory reporting lag). Present your evidence and make a recommendation: should Walmart stock extra board games for the next storm?

**Requires:** Querying the SQLite database with `sqlite3` + `pandas`, cross-referencing with the transaction CSV, SKU/category audit, evidence-based written argument, supporting visualization.

---

## Deliverables

### 1. Python Notebook

A single Jupyter or Kaggle notebook (`.ipynb`) containing:

- **Data Loading:** All CSVs loaded with pandas, SQLite queried with `sqlite3`, weather data pulled from API
- **Data Cleaning Pipeline:** A clear section showing your wrangling steps (dedup, SKU standardization, timestamp fixes, missing value handling, type conversions)
- **Analysis:** All 5 questions answered with code, visualizations, and markdown explanations
- **Visualizations:** Minimum **6 plots** using `matplotlib`, `seaborn`, and/or `plotly`
- **Markdown Cells:** Explain your methodology, findings, and reasoning throughout

### 2. Reflection Write-Up

Included in your notebook (at the end) or as a separate markdown file. Each team member should contribute. Answer all 5 reflection questions below.

---

## Reflection Questions

Answer each question thoughtfully (one solid paragraph minimum per question).

**1. Data Quality Impact**
> Describe a specific data quality issue you encountered in the supplied data. How did your cleaning decision change the outcome of your analysis? What would have happened if you had not caught it?

**2. ETL Trade-offs**
> You made choices about how to standardize SKUs, handle missing timestamps, and join weather data. Pick one decision and explain: what alternative approach could you have taken, and how might it have changed your results?

**3. Pipeline Trust**
> The Walmart CDO argued that the biggest risk is not the model — it is the pipeline. Based on your experience in this project, do you agree or disagree? What was the most fragile part of your data pipeline?

**4. Business vs. Data**
> For Question 5 (board games), your team had to make a recommendation with imperfect data. How did you weigh statistical evidence against business risk? Would you have decided differently with more time or more data?

**5. Team Collaboration**
> How did your team divide the work? What would you do differently if you had another week? What was the most valuable skill each team member contributed?

---

## 3-Week Timeline (This is only a suggested cadence) 

### Week 1: Data Ingestion, Exploration, and Cleaning

- Read the Walmart case study thoroughly
- Load all CSV files and the SQLite database into pandas DataFrames
- Explore the data: `.shape`, `.dtypes`, `.info()`, `.describe()`, `.isnull().sum()`
- Identify all data quality issues (duplicates, missing values, inconsistent SKUs, etc.)
- Build your cleaning pipeline: dedup, standardize SKUs, fix timestamps, normalize categories, handle missing values, fix data types
- Set up your weather API: register if needed, test API calls, pull historical weather data for Florida (September 2024)
- **Milestone:** Clean DataFrames ready for analysis; weather data retrieved and parsed into a DataFrame

### Week 2: Analysis and Visualization

- Answer Questions 1–5 using your cleaned data
- Join weather API data with sales data (handle timezone alignment)
- Query the SQLite database for Question 5
- Create all required visualizations (minimum 6 charts/plots)
- Write markdown explanations for each question
- **Milestone:** All 5 questions answered with supporting code, visuals, and written analysis

### Week 3: Polish, Reflect, and Submit

- Organize your notebook: clear section headers, clean code, no leftover debugging cells
- Write reflection responses (all 5 questions, every team member contributes)
- Peer review within your team — check each other's code and explanations
- Final run: Restart kernel and run all cells top-to-bottom to confirm everything executes
- **Milestone:** Final notebook submitted

---

## Grading Rubric

| Component | Weight | What We're Looking For |
|-----------|--------|----------------------|
| **Data Cleaning** | 25% | Thoroughness of cleaning pipeline; handling of duplicates, missing values, SKU consolidation, type fixes; code clarity |
| **Weather API Integration** | 15% | Working API calls, proper parsing, timezone handling, meaningful join with sales data |
| **Analytical Questions (1–5)** | 30% | Correct methodology, sound reasoning, clear answers supported by data |
| **Visualizations** | 15% | Minimum 6 plots; appropriate chart types; clear labels, titles, and legends; visual storytelling |
| **Reflection Write-Up** | 15% | Thoughtful, specific responses; demonstrates understanding of ETL trade-offs and data pipeline risks |

---

## Important Notes

- **Do not fabricate data.** All weather data must come from a real API call demonstrated in your notebook.
- **Show your work.** We want to see the messy data, your cleaning steps, and the clean result. Do not just show the final output.
- **Comment your code** where logic is non-obvious, but avoid narrating every line.
- **Cite your weather API source** and include the base URL you used.
- This project is inspired by a real Walmart case study. The supplied data is synthetic but designed to mirror the patterns described in the case.

---

## Repository Structure

```
walmart-hurricane-project/
├── DS2002_Midterm_Project_Brief.md    <- You are here
├── Walmart Case.pdf                   <- Required reading
├── data/
│   ├── walmart_transactions.csv       <- ~25,000 messy POS records
│   ├── store_locations.csv            <- Florida store metadata
│   ├── product_catalog.csv            <- Product/SKU reference
│   ├── distribution_centers.csv       <- Distribution center info
│   └── inventory_and_sales.db         <- SQLite: daily_sales_summary + inventory_levels
└── notebooks/
    └── [your_team_notebook].ipynb     <- Your deliverable goes here
```

Good luck. Stock the Pop-Tarts.
