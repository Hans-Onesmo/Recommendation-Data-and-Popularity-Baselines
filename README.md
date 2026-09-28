# Recommendation Data and Popularity Baselines

## Task
Clean and explore a movie-ratings dataset, measure how sparse the user-item data is, and build a simple popularity-based recommender that returns the top 10 movies.

## Repository contents
| File | Description |
|---|---|
| `Popularity_Recommender.ipynb` | Completed notebook (all cells executed) |
| `data/ratings.csv` | Ratings dataset provided by the lecturer |
| `top10_recommendations.csv` | Top 10 recommended movies |
| `README.md` | This file |

## Approach
1. **Inspect:** loaded the data, checked dimensions, types, missing values and duplicates.
2. **Clean:** removed exact duplicates and rows with missing IDs (none found); confirmed all ratings are on the 1 to 5 scale. Three users had rated the same movie twice, so the most recent rating was kept to give one rating per user-movie pair (305 to 302 rows).
3. **Explore:** summary statistics and a user-item matrix (users x movies).
4. **Sparsity:** `1 - ratings / (users x movies)`.
5. **Recommend:** for each movie, computed average rating and number of ratings; kept movies with at least 10 ratings and ranked by average rating (ties broken by number of ratings).

## Key findings
| Metric | Value |
|---|---|
| Total ratings (after cleaning) | 302 |
| Unique users | 50 |
| Unique movies | 24 |
| Most active user | U015 (8 ratings) |
| Most-rated movie | Nairobi Nights (15 ratings) |
| Average rating | 3.45 |
| Sparsity | 74.83% (density 25.17%) |

About three quarters of possible user-movie pairs have no rating, which is the central difficulty for recommender systems.

### Top 10 (at least 10 ratings)
| Rank | Movie | Avg rating | Ratings |
|---|---|---|---|
| 1 | Midnight in Mombasa | 4.42 | 12 |
| 2 | Market Day | 4.33 | 12 |
| 3 | Code Breakers | 4.17 | 12 |
| 4 | Home Again | 4.08 | 12 |
| 5 | City of Tomorrow | 4.00 | 12 |
| 6 | Hidden Lake | 4.00 | 12 |
| 7 | Future Africa | 3.92 | 12 |
| 8 | Coastal Dreams | 3.83 | 12 |
| 9 | The Final Goal | 3.83 | 12 |
| 10 | Beyond the Horizon | 3.75 | 12 |

## Interpretation
- **Why they rank highly:** these movies have the highest average scores among raters, and the 10-rating minimum keeps the averages from resting on one or two votes. Every movie in this dataset has at least 12 ratings, so the threshold removed none.
- **Advantage:** simple and works for new users with no history (no cold-start problem for users).
- **Limitations:** (1) no personalisation, every user sees the same list; (2) popularity bias, new or niche movies rarely get enough ratings to surface.
