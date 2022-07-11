# FIFA-Womens-Rankings

### An easy way to access FIFA Women's Rankings by date from 2003 up to today.

This data is readily available through FIFA's data API, simply made available here as a CSV file for easy access. 

#### However, one major change has been made to the data, and three minor changes. 

## Major differences from the FIFA data API.

#### 1. Four new columns have been added to the dataset, all of them with a column name prefix of `lagged_`

They are as follows.

1. `lagged_ranking_date`
 - As each observation has values for both `previous_rank` and `previous_points`, but **no** information on the date of 
 said previous rank and previous points, this is an attempt to amend that by applying a lag of 1 to the `ranking_date` column. 
2. `lagged_rank`
 - This is the equivalent of `previous_rank` but is achieved by applying a lag of 1 to the `rank` column. 
3. `lagged_points`
 - This is the equivalent of `previous_points` but is achieved by applying a lag of 1 to the `points` column.
4. `lagged_true`
- This column is a complement to the three previous `lagged_` columns. Lagging leaves explicit `NA` values for the first time each national team appears
in the data. For convenience I've filled in those `NA` values with data. This makes it unnecessary to make changes to the actual data in the 
`previous_rank` and `previous_points` columns where it's seemingly erroneous. With `lagged_ranking_date` it's easier, for instance, to do fuzzy joins
with other datasets based on the time intervals between rankings. 

This is how the data is inserted:

| column                | data inserted                         |
|-----------------------|---------------------------------------|
| `lagged_ranking_date` | "2002-12-31"                          |
| `lagged_rank`         | corresponding `previous_rank` value   |
| `lagged_points`       | corresponding `previous_points` value |

the `lagged_true` column only serves to denote which of the rows are the results of the actual lag function, and which ones are the rows with the 
aforementioned inserted data.

## Minor differences from the FIFA data API.

#### 1. `country_name` values have been harmonized to ensure that country name spellings stay consistent throughout all the rankings.
#### 2. `country_code` values have been harmonized to reflect the current country code, not the (now obsolete) country code at the time of each ranking.
#### 3. Column names are now in [snake_case](https://en.wikipedia.org/wiki/Snake_case).
