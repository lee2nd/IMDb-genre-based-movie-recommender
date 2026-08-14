# IMDb Genre-Based Movie Recommender

A movie recommendation project built on **IMDb's public datasets**, clustering films by genre and filtering for high-quality, well-reviewed titles — enriched with poster images and trailer links for a more visual browsing experience.

## Data Source

Download the following files from [IMDb Data Files Available for Download](https://datasets.imdbws.com/):
- `title.ratings.tsv.gz`
- `title.basics.tsv.gz`

## Pipeline

1. **`imdb_preprocessing.ipynb`** — cleans and merges raw IMDb data, splits titles into per-genre datasets
2. **`imdb_analysis.ipynb`** — applies filtering and clustering logic, and compiles the final recommendation list

## Recommendation Logic

- **Cluster by genre** — movies are grouped into individual genre files (Action, Comedy, Drama, Sci-Fi, etc.)
- **Enrichment** — adds poster images and trailer video links for each title
- **Filtering criteria:**
  - Number of votes ≥ min(60th percentile, 10,000)
  - Rating ≥ 6.5

## Contents

- `raw_imdb.csv` — merged raw dataset from IMDb source files
- `Action.csv`, `Comedy.csv`, `Drama.csv`, ... — per-genre filtered movie lists (24 genres total)
- `all_genres.xlsx` — consolidated view across all genres
- `movie recommendation.xlsx` — final recommendation output
- `empty.csv` — placeholder/edge-case handling for genres with no qualifying titles
