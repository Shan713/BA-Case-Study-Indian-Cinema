# Supporting Pre-Release Decision Making in Indian Cinema

A Data-Driven Analysis of Certification, Content, and Release Timing on Opening Weekend Box Office Performance

**Business Analytics — Individual Case Study**
Shantharam P · CB.SC.U4CSE23146 · CSE-B · Amrita School of Computing

## Problem Statement

Producers, distributors, and multiplex chains in India commit to costly, high-stakes decisions — certification category (U/UA/A), release timing, and scale of theatrical distribution — weeks before a film's actual audience response is known, often relying on intuition and star power rather than evidence from historical performance. Screens, release slots, and marketing budgets are scarce, expensive resources, and post-pandemic shifts in theatrical habits and OTT adoption have made pre-2020 intuition an increasingly unreliable guide.

## Objectives

1. Identify which pre-release factors (genre, language, certification, runtime, cast track record, sequel status, release timing) significantly influence opening-weekend box-office performance.
2. Build a predictive model that estimates an expected opening-weekend collection range from attributes known before release.
3. Determine whether the effect of certification on opening-weekend performance has changed between the pre-COVID (2013–2019) and post-COVID (2022–2026) periods, and derive decision-support recommendations for producers, distributors, and multiplex chains.

## Data Collection

A dataset of **1,900 Indian films** across nine language industries (Hindi, Tamil, Telugu, Malayalam, Kannada, Punjabi, Gujarati, Marathi, Bengali) and the years 2013–2026 was self-scraped and enriched from three sources:

- **[Sacnilk](https://sacnilk.com)** — an Indian box-office data platform. Box-office figures were pulled by querying Sacnilk's internal records API directly (discovered via network-traffic inspection), which returns exact, pre-computed opening-weekend figures per film and eliminated the ~85% failure rate of an initial URL-slug-guessing approach.
- **Wikipedia** — yearly film-list pages (for candidate titles) and film infoboxes (to backfill certification and runtime).
- **[TMDb](https://www.themoviedb.org/documentation/api)** — India-specific certification (cross-check), audience rating, budget, genres, and cast popularity, via its public API.

See [`data/README.md`](data/README.md) for the dataset, and Section 2 of the [report](Case_Study_Report.pdf) for the full data-collection narrative, including data-quality issues found and corrected along the way (wrong-language duplicate scrapes, a ratings placeholder, a budget placeholder).

## Analytics Methods

- **Exploratory data analysis** across certification, language, genre, cast, rating, and budget, with 18 plots.
- **Model A** — OLS regression (standard errors clustered by film) identifying general drivers of opening weekend: star power, sequel status, runtime, festival-window timing, language, and genre.
- **Model B** — OLS regression testing a certification × pre-/post-COVID period interaction, with a transparent sensitivity analysis of how the finding responds to added controls.
- **Random Forest** predictive model, with a film-grouped (not row-grouped) train/test split to prevent leakage between language versions of the same film.
- Comparison against three published studies on Indian/international box-office prediction (Section 5 of the report).

## Key Results

- Star power (a time-aware measure of a lead cast's own earlier box-office track record), sequel status, runtime, and festival-window release timing are robust, statistically significant drivers of opening weekend (Model A, R² = 0.519).
- **Certification's effect has reversed since COVID-19**: A-certified films, the weakest-opening category pre-pandemic, are the strongest-opening category post-pandemic, while U-certified films have fallen the furthest (interaction coefficient −0.667, p = 0.004). This holds across four successive dataset expansions and within Hindi alone, though it attenuates once general content controls are added — reported transparently in the report's sensitivity analysis.
- The Random Forest model explains **60% of the variance** in log opening weekend on a rigorously film-grouped test split.
- Business recommendations are given for certification strategy, release timing, screen allocation, and market-specific benchmarking (Section 6 of the report).

## Repository Structure

```
├── README.md
├── Case_Study_Report.pdf      # Final report
├── analysis.ipynb             # Analysis notebook (EDA, models, plots)
└── data/
    ├── README.md
    └── processed/movies_master.csv   # Final cleaned dataset (1,900 films)
```

## Running the Notebook

```bash
pip install pandas numpy matplotlib seaborn statsmodels scikit-learn jupyter
jupyter notebook analysis.ipynb
```

Run it from the repository root; it reads `data/processed/movies_master.csv`.

## References

Full bibliography and in-text citations are in Section 7 of [`Case_Study_Report.pdf`](Case_Study_Report.pdf), covering the three comparison studies (Verma & Sarkar 2020; Paul & Stella 2023; Lampe & McRae 2021), Rammal 2023 on post-pandemic theatrical habits, and the primary data sources (Sacnilk, Wikipedia, TMDb).
