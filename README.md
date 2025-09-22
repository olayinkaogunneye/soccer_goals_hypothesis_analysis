# ⚽ Soccer Goals Analysis: Men's vs. Women's FIFA World Cup Matches

## 📌 Project Overview

This project investigates whether more goals are scored in women's international soccer matches than men's, using official FIFA World Cup match data since January 1, 2002. The analysis is conducted as part of a sports journalism initiative for a major online media outlet specializing in soccer analytics.

## 🎯 Research Question

> Are more goals scored in women's international soccer matches than men's?

We use statistical hypothesis testing to determine whether the average number of goals per match is significantly higher in women's FIFA World Cup games compared to men's.
---
## 🛠️ Requirements
- R (≥ 4.0)
- R packages:
  - `dplyr`
  - `lubridate`
  - `ggplot2`
  - `here`

Install missing packages with:
```r
install.packages(c("dplyr", "lubridate", "ggplot2", "here"))

## 🚀 Analysis Workflow
1. Load and Inspect Data
• 	Import men’s and women’s international match results.
• 	Inspect structure and preview rows.

## 2. Filter for Relevant Matches
• 	Keep only FIFA World Cup matches (not qualifiers).
• 	Restrict to matches after 2002-01-01.

## 3. Feature Engineering
•  Create a total_goals column = home_score + away_score


## 4. Exploratory Data Analysis (EDA)
• 	Summary statistics (mean, median, standard deviation).
• 	Histograms comparing distributions.
• 	Boxplots comparing men vs women.

## 5. Hypothesis Testing
• 	Null (H₀): μ_women ≤ μ_men
• 	Alternative (H₁): μ_women > μ_men
• 	One-tailed Welch’s t-test.
• 	Robustness check with Wilcoxon rank-sum test.

## 📊 Key Results
- Women’s matches average 2.98 goals per game.
- Men’s matches average 2.51 goals per game.
- t-test p-value = 0.0026 → reject H₀ at 10% significance.
- Women’s matches score at least 0.19 more goals per match (95% CI).
- Wilcoxon test confirms the distribution is also shifted upward.

## 👉 Conclusion: Women’s World Cup matches are statistically higher scoring than men’s.

## 📈 Outputs
- Figures:
- Distribution_of_Total_Goals.png (histogram)
- Boxplot_Goals_by_Gender.png
- Statistical Results:
- t-test and Wilcoxon test outputs stored in result_df (optional CSV export).

## ✨ Next Steps
- Extend analysis to include qualifiers or continental tournaments.
- Explore variance in scorelines (e.g., frequency of blowouts).
- Add time trends (are matches becoming higher or lower scoring over time?).

👤 Author
- Olayinka
