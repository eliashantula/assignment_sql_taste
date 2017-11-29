# assignment_sql_taste
A delicious appetizer of SQL-ey goodness


## Queries

### Example

10 results with information on all columns
```
SELECT *
  FROM tutorial.us_housing_units
  LIMIT 10
```
Housing starts in the Midwest
```
SELECT midwest
  FROM tutorial.us_housing_units
```
All housing starts in December since 1985
```
SELECT *
  FROM tutorial.us_housing_units
  WHERE month_name = 'December' AND year >= 1985
```
All housing starts in the second half of the year since 1990
``SELECT *
  FROM tutorial.us_housing_units
  WHERE month_name IN ('July', 'August', 'September', 'October', 'November', 'December') 
  AND year >= 1990`
```
All rows where housing starts were above 30,000 in the South region
`SELECT *
  FROM tutorial.us_housing_units
  WHERE south > 30``
```
The sum of housing starts across all regions for each row
`SELECT *,
  (south + west + midwest + northeast) as "total" 
  FROM tutorial.us_housing_units``
```
All rows where the sum of all housing starts is above 70,000 Note: You can't use an alias in a WHERE clause.
`SELECT *
  FROM tutorial.us_housing_units
  WHERE south + west + midwest + northeast > 70  ``
```
All rows where the sum of all housing starts is between 50-80k
``SELECT *
  FROM tutorial.us_housing_units
  WHERE (south + west + midwest + northeast) BETWEEN 50 AND 80 `
```
The average of all housing starts across all regions for each row
`SELECT *,
  (south + west + midwest + northeast) / 4 as average
  FROM tutorial.us_housing_units``
```
All rows where the housing starts in the South are above the sum of the other three regions
```
```
The percentage of housing starts that occur in each region since 1990 Note: Use an alias to title the new columns appropriately
```
```
