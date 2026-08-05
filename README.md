# synent-Task3-Exploratory-Data-Analysis-EDA--Amish-Awasthi

# Netflix Exploratory Data Analysis (EDA)

## Problem Statement
Over the past decade, streaming platforms have transformed how global entertainment is produced and consumed. Understanding catalog composition, content strategy, target audience distribution, and historical content acquisitions is vital for media analysts and content strategists. 

This project performs a comprehensive Exploratory Data Analysis (EDA) on the Netflix catalog to uncover key content trends, geographic hubs of production, maturity rating distributions, and runtime dynamics.

---

## Dataset Details
* **Source:** Netflix Movies and TV Shows Dataset (`netflix_titles.csv`)
* **Total Records:** 8,807 titles (prior to cleaning)
* **Key Attributes:**
  * `show_id`: Unique identifier for each movie/show
  * `type`: Identifier (Movie or TV Show)
  * `title`: Title of the content
  * `director` / `cast`: Directors and actors involved
  * `country`: Country or countries of production
  * `date_added`: Date the content was added to Netflix
  * `release_year`: Original release year of the content
  * `rating`: Maturity rating (e.g., TV-MA, PG-13)
  * `duration`: Runtime in minutes (Movies) or number of seasons (TV Shows)
  * `listed_in`: Genres and categories

---

## Approach

1. **Data Cleaning & Missing Value Handling:**
   * Replaced missing values in high-cardinality categorical columns (`director`, `cast`, `country`, `rating`) with `'Unknown'`.
   * Handled data anomaly rows where `duration` values were stored in the `rating` column.
   * Dropped rows missing critical temporal data (`date_added`).
   
2. **Feature Engineering:**
   * Parsed `date_added` into standard datetime objects and extracted `added_year`, `added_month`, and `added_month_name`.
   * Created `release_to_added_delay` (`added_year - release_year`) to measure content lag.
   * Extracted numerical values (`duration_num` / `duration_min` / `seasons`) from text strings for runtime analysis.
   * Exploded comma-separated fields (`listed_in`, `country`) to accurately analyze individual multi-value categories.

3. **Statistical Analysis & Visualization:**
   * Computed tailored summary statistics for skewed metrics (Median, IQR) and unnested categorical distributions.
   * Analyzed trend distributions over time (yearly additions, monthly release seasonality).
   * Constructed separated correlation heatmaps for Movies (Minutes) vs. TV Shows (Seasons) to prevent unit mixing.

---

## Key Results & Insights

* **Catalog Split:** Movies dominate the platform, accounting for **~69.6%** of titles, while TV Shows comprise **~30.4%**.
* **Global Content Leaders:** The **United States** leads content production by a wide margin, followed by **India** and the **United Kingdom**.
* **Target Audience:** Content labeled **TV-MA** (Mature Audiences) and **TV-14** forms the vast majority of the catalog, reflecting a focus on adult/young-adult demographics.
* **Movie Runtime Dynamics:** The average movie duration centers around **~99 minutes**, following a near-normal distribution.
* **TV Show Longevity:** Most TV shows on the platform consist of **1 Season** (~67%), with rapid drop-offs for multi-season shows.
* **Content Acquisition Lag:** The median delay between original release year and Netflix addition date is **1.0 year**, though legacy titles extend up to a **93-year** delay gap.
