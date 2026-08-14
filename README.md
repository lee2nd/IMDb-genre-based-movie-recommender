# IMDb Genre-Based Movie Recommender

A movie recommendation project built on **IMDb's public datasets**, clustering films by genre and filtering for high-quality, well-reviewed titles. The project enriches top-tier recommendations with localized Taiwanese titles, poster images, and YouTube trailer links via the TMDB API.

## Data Source
Download the following files from [IMDb Data Files Available for Download](https://datasets.imdbws.com/):
- `title.ratings.tsv.gz`
- `title.basics.tsv.gz`

## Pipeline

1. **Data Preprocessing**
   - Loads and filters IMDb datasets for movies (`titleType == 'movie'`).
   - Merges title basics and ratings.
   - Applies a global base filter: `numVotes > 1500` and `averageRating > 6.5`.
   - Outputs the consolidated dataset to `raw_imdb.csv`.

2. **Analysis & Enrichment**
   - Reads the preprocessed `raw_imdb.csv`.
   - Splits movies into separate datasets based on their genres (26 categories, including handling for empty genres).
   - Applies a dynamic threshold per genre: `numVotes > min(60th percentile, 10000)` and `averageRating >= 6.5`.
   - **Enrichment:** Identifies the top 10% highest-rated movies (≥ 90th percentile) in each genre and fetches their Taiwanese localized title, poster image path, and YouTube trailer link using the TMDB API.
   - Exports the enriched data to `all_genres.xlsx`.
   - Sorts the final data by rating (descending) and saves it as `movie recommendation.xlsx`.

## File Structure & Outputs
- `raw_imdb.csv` — Merged base dataset after initial global filtering.
- `all genres/` directory — Contains per-genre filtered movie lists (`Action.csv`, `Comedy.csv`, `Drama.csv`, `empty.csv`, etc.).
- `all_genres.xlsx` — Consolidated Excel workbook with a separate sheet for each genre, enriched with TMDB API data for the top 10% titles.
- `movie recommendation.xlsx` — Final recommendation output, identical to `all_genres.xlsx` but strictly sorted by `averageRating` descending.