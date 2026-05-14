# 📊 Layoffs Data Analysis using SQL

## 🔍 Project Overview

This project explores a real-world layoffs dataset to uncover trends across companies, time periods, industries, and regions.

The goal is to answer key questions such as:

* Which companies laid off the most employees?
* When did layoffs peak?
* Which countries and stages were most affected?
* Are layoffs random or pattern-driven?

---

## 📁 Dataset

The dataset contains:

* Company name
* Date of layoff
* Total employees laid off
* Percentage of workforce laid off
* Company stage
* Country
* Funds raised (in millions)

---

## ⚙️ Tools & Technologies

* SQL (MySQL)
* Window Functions
* Common Table Expressions (CTEs)

---

## 📌 Key Analysis Performed

### 1. Data Exploration

* Checked overall dataset structure
* Identified missing and extreme values

### 2. Company Analysis

* Total layoffs per company
* Companies with repeated layoffs

### 3. Time-Based Analysis

* Layoffs by year and date
* Monthly trend analysis
* Rolling cumulative layoffs over time

### 4. Geographic Analysis

* Layoffs by country

### 5. Stage Analysis

* Layoffs by company stage (Startup, Growth, etc.)

### 6. Extreme Cases

* Companies with 100% layoffs

### 7. Ranking Analysis

* Top 5 companies per year using `DENSE_RANK()`

---

## 📊 Key Insights

* Layoffs are **not random**; they follow clear time-based trends
* Certain months show **significant spikes**, indicating economic events
* Some companies laid off **100% of employees**, even after raising large funds
* A small number of companies contributed to a **large share of total layoffs**
* Layoffs occurred across all stages, including **late-stage companies**

---

## 📈 Advanced SQL Concepts Used

* `GROUP BY` for aggregation
* `DATE_FORMAT()` and `YEAR()` for time analysis
* `SUM() OVER()` for rolling totals
* `DENSE_RANK()` for ranking within groups
* CTEs for structured and readable queries

---

## 🧠 Sample Query (Top Companies Per Year)

```sql
WITH Company_Year AS (
    SELECT company, YEAR(date) AS years, SUM(total_laid_off) AS total_laid_off
    FROM layoff_staging2
    GROUP BY company, YEAR(date)
),
Company_Year_Rank AS (
    SELECT *,
    DENSE_RANK() OVER (PARTITION BY years ORDER BY total_laid_off DESC) AS ranking
    FROM Company_Year
    WHERE years IS NOT NULL
)
SELECT *
FROM Company_Year_Rank
WHERE ranking <= 5;
```

---

## 🚀 Future Improvements

* Add data visualizations (Python / Power BI / Tableau)
* Clean and standardize company & country names
* Combine with external economic indicators
* Build an interactive dashboard

---

## 📌 Conclusion

This project demonstrates how SQL can be used not just for querying data, but for extracting meaningful insights and identifying real-world trends.

---

⭐ If you found this useful, feel free to star the repo!
