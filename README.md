# IMDb SQL Analysis — six-table relational schema

Analytical SQL against a six-table IMDb schema (movies, genres, ratings, and the supporting
tables), written to answer a set of business questions about film output, ratings, and genre
trends. Completed during my business-analyst internship at OESON, where the queries and the ERD
were the deliverables.

## Schema

The dataset models films relationally rather than as a single flat file: a movie table keyed on
`movie_id`, a genre bridge table (a film can hold several genres, so genre analysis requires a join
per genre), a ratings table carrying average rating and vote count, and the supporting lookup
tables. Working against a normalised schema is the point of the exercise — most of the analytical
questions cannot be answered from one table.

An entity-relationship diagram is included in `IMDb_Data_and_ERD.xlsx`.

## What the queries demonstrate

`imdb_analysis_queries.sql` contains the full question set with comments. Across the file:

| Technique | Count | Used for |
|---|---|---|
| Joins | 13 | Assembling movie, genre, and rating context across the normalised tables |
| GROUP BY aggregations | 11 | Genre-level and period-level rollups (film counts, average ratings, vote totals) |
| Window functions | 5 | Ranking within groups — top films per genre, rating rank against the period average |
| CTEs | 2 | Staging intermediate results so the ranking question stays readable |
| Subqueries | yes | Filtering against aggregates computed in the same statement |

## Questions answered

- Which genres consistently produce the highest-rated films, and does that hold once vote volume
  is taken into account?
- Who are the highest-rated directors or lead performers, ranked within genre?
- How have film output and average ratings shifted across decades?
- Which films are outliers — very high rating on very low vote count, or the reverse?
- How do genre mixes change over time?

## Running it

The dataset itself is not redistributed here (it is a public IMDb-derived set, and the import file
is seeded data rather than my work). To run the queries, load the IMDb dataset into MySQL and
execute `imdb_analysis_queries.sql` against the resulting schema; the table and column names the
queries expect are documented in the file's header comments.

## Files

| File | What it is |
|---|---|
| `imdb_analysis_queries.sql` | The question set, with CTEs, window functions, and join logic |
| `IMDb_Data_and_ERD.xlsx` | ERD plus the working analysis workbook |
