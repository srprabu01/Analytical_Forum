# Steam Games Analytics — Discussion-to-Report

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](#license) [![Made with R](https://img.shields.io/badge/Made%20with-R-blue)](#reproducibility) [![Dataset: Kaggle](https://img.shields.io/badge/Dataset-Kaggle-orange)](#data)


This repository consolidates my course **discussion posts** into a single, well‑structured **report-style README** that
documents the **Steam Games Dataset** analysis: objectives, questions, methods, results, visuals, and takeaways.

> Why this repo?  
> - Turn scattered discussion entries into a cohesive artifact.  
> - Preserve the original images/figures.  
> - Provide clear guidance for reproduction and future extension.


## Table of Contents
- [Project Snapshot](#project-snapshot)
- [Data](#data)
- [Research Questions](#research-questions)
- [Methods](#methods)
- [Key Findings](#key-findings)
  - [Popularity Drivers](#popularity-drivers)
  - [Pricing, Engagement, and Reviews](#pricing-engagement-and-reviews)
  - [Seasonality of Releases](#seasonality-of-releases)
- [Figures (Imported from Discussions)](#figures-imported-from-discussions)
- [Reflections & Learning](#reflections--learning)
- [Reproducibility](#reproducibility)
- [References](#references)
- [License](#license)


## Project Snapshot
- **Topic**: Exploratory analysis of video games on the Steam platform.
- **Core Artifacts**: Summaries, questions, and results originally shared as Module 1–6 discussions; now restructured.
- **Primary Outcomes**: A concise set of **questions**, **analytical approaches**, and **evidence-backed inferences**.


## Data
- **Source**: *Steam Games Dataset* (Kaggle). Includes games' release dates, pricing, reviews/ratings, average playtime,
  estimated owners, concurrent users (CCU), platform availability, tags/languages, etc.
- **Scale**: Multiple mentions of dataset size occur across posts (≈27k rows in an early subset; ≈97k+ in later versions).
- **Data Quality Considerations**:
  - Missing values for **price** or **ratings** in some entries.
  - **Text-heavy fields** (e.g., tags, languages) require preprocessing.
  - **Outliers** in average playtime; needs capping/winsorization or robust summary stats.

- **Additional Computable Features** (engineered for insight):
  - **Review Ratio** = positive / total reviews.
  - **Cost per Hour** = price / average playtime.
  - **Genre Popularity** via aggregated playtime or review counts.


## Research Questions
1. **What factors contribute most to a game's popularity?**  
   *Operationalization*: Popularity proxied by **Estimated Owners** and **Peak Concurrent Users (CCU)**.

2. **How does pricing affect player engagement and reviews?**  
   *Operationalization*: Compare **free vs. paid**; analyze **price bands** vs. **playtime** and **review volume**.

3. **Are there seasonal trends in game releases?**  
   *Operationalization*: Extract **release month** and analyze **temporal patterns** over years.


## Methods
- **EDA**: Summary statistics, distribution checks, correlation matrices.
- **Modeling**: Correlation analysis and basic regression to identify predictors of popularity.
- **Feature Engineering**: Review ratio, cost per hour, monthly release bins.
- **Visualization**: Heatmaps, scatter plots, boxplots, and line/bar charts for temporal trends and comparisons.


## Key Findings

### Popularity Drivers
- **Estimated Owners** strongly correlates with **Peak Concurrent Users (CCU)** (reported r ≈ 0.78).  
- **Metacritic** and **User Scores** show **weak correlation** with popularity proxies, suggesting marketing/genre/platform
  mix may exert stronger influence than review scores alone.
- Genres like **Action** and **RPG** frequently appear among top CCU counts.

### Pricing, Engagement, and Reviews
- **Free-to-play** titles show **higher median playtime** than paid titles.
- **Paid games in the $10–$30 band** garner **more positive reviews**, potentially reflecting perceived value.
- **Price vs. Reviews** shows a **downward trend**—higher prices often coincide with fewer reviews (elasticity/selection).

### Seasonality of Releases
- Releases **cluster in October–November**, aligning with Q4/holiday cycles.
- **February** often has **fewer** releases (post‑holiday cooldown).
- Long‑term trend shows **growth since 2015**, with a **COVID‑era peak around 2020**.

## Figures (Imported from Discussions)

**Figure 1.**  
<img width="940" height="599" alt="image" src="https://github.com/user-attachments/assets/85224815-2134-4bfa-94af-d00715f576c9" />


**Figure 2.**  
<img width="940" height="602" alt="image" src="https://github.com/user-attachments/assets/1ce9a78a-36e7-40bc-94ec-1dc828285ca6" />


**Figure 3.**  
<img width="816" height="519" alt="image" src="https://github.com/user-attachments/assets/96f08010-42f0-4fa3-8fe8-1ffdbb3717ff" />


**Figure 4.**  
<img width="940" height="516" alt="image" src="https://github.com/user-attachments/assets/23312692-e089-47d7-acfb-56e4f6aec672" />


**Figure 5.**  
<img width="940" height="579" alt="image" src="https://github.com/user-attachments/assets/1bbe4129-0ff3-42fd-9eee-9642e2a87057" />



## Reflections & Learning
- **Data cleaning** is frequently the **most time‑consuming** and **critical** phase.
- **Correlation ≠ Causation**: Signal requires careful interpretation and, where possible, causal design or robust controls.
- **Visualization = Storytelling**: Choices of chart types, scales, and labeling materially affect interpretation.


## Reproducibility
- **Language/Tools**: R (tidyverse, ggplot2), plus spreadsheet/meta checks.
- **Suggested Steps**:
  1. Acquire the Kaggle dataset (see link below).
  2. Clean and transform: handle NAs, standardize types, engineer features.
  3. Run EDA and build correlation/regression summaries.
  4. Recreate visuals (heatmap, price–engagement boxplots, seasonal release charts).
- **Outputs**: Update `/figures` or `/images` with regenerated plots for versioning.


## References
- Kaggle — *Steam Games Dataset*.
- R Project for Statistical Computing — CRAN.
- James, Witten, Hastie, Tibshirani (2013) — *An Introduction to Statistical Learning*.
- Indiana University Libraries — *Evaluating Data Visualizations* Guides.
- HBS Online — *Bad Data Visualization: Misleading Examples*.


## License
This project is released under the **MIT License**. See `LICENSE` for details.
