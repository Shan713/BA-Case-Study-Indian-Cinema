# Data

`processed/movies_master.csv` is the final cleaned dataset used in `analysis.ipynb` (1,900 Indian films, 2013-2026, nine language industries).

It was built by scraping Sacnilk (box office), Wikipedia (film lists, certification and runtime backfill) and the TMDb API (certification, rating, budget, genres, cast popularity), then merging, deduplicating and cleaning. See Section 2 of `Case_Study_Report.pdf` for the full collection method and the data-quality fixes.
