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
SELECT *
  FROM tutorial.us_housing_units
  WHERE south > midwest + west + northeast
```
The percentage of housing starts that occur in each region since 1990 Note: Use an alias to title the new columns appropriately
```
SELECT year,
       month,
       month_name,
       south/(south+west+midwest+northeast)*100 AS "South",
       west/(south+west+midwest+northeast)*100 AS "West",
       midwest/(south+west+midwest+northeast)*100 AS "Midwest",
       northeast/(south+west+midwest+northeast)*100 AS "Northeast"
  FROM tutorial.us_housing_units
  WHERE year >= 1990
```
## Billboard

All rows where Elvis Presley had a song on the top 100 charts
```
SELECT *
  FROM tutorial.billboard_top_100_year_end 
  WHERE artist = 'Elvis Presley'
```
All rows where the artist's name contained "Tony" (not case sensitive)
```
SELECT *
  FROM tutorial.billboard_top_100_year_end 
  WHERE artist ILIKE '%tony%'
```
All rows where the song title contained the word "love" in any way
```
SELECT *
  FROM tutorial.billboard_top_100_year_end
  WHERE song_name ILIKE '%love%'
```
Allrows where the artist's name begins with the letter "A"
```
SELECT *
  FROM tutorial.billboard_top_100_year_end 
  WHERE artist ILIKE 'a%'
```
The top 3 songs from each year between 1960-1969
```
SELECT *
  FROM tutorial.billboard_top_100_year_end
  WHERE year_rank <= 3
    AND year BETWEEN 1960 AND 1969
```
All rows where either Elvis Presley, The Rolling Stones, or Van Halen were the artist
```
SELECT *
  FROM tutorial.billboard_top_100_year_end 
  WHERE artist IN('Elvis Presley', 'Rolling Stones', 'Van Halen')
```
Which artist has had the most appearances on the top 100 list?
```
SELECT artist,
  COUNT(*) AS count
  FROM tutorial.billboard_top_100_year_end 
 GROUP BY artist
 ORDER BY COUNT(*) DESC
```
Which artist has had the most #1 hits? How many?
``SELECT artist,
  COUNT(*) AS count
FROM tutorial.billboard_top_100_year_end 
WHERE year_rank = 1
GROUP BY artist
ORDER BY COUNT(*) DESC`
```
All rows from 1970 where the songs were ranked 10-20th
``SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE year = 1970 AND year_rank BETWEEN 10 AND 20`
```
All rows from the 1990's where Madonna was not ranked 10-100th
``SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE year BETWEEN 1990 AND 1999 AND 
NOT (artist = 'Madonna' AND year_rank 
BETWEEN 10 AND 100) `
```
All rows from 1985 which do not include Madonna or Phil Collins in the group.
``SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE year = 1985
AND NOT ("group" ILIKE '%Madonna%' OR "group" ILIKE '%phil collins%') `
```
All number 1 songs in the data set.
``SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE year_rank = 1
`
```
All rows where the artist is not listed

```
SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE artist IS NULL
```
All of Madonna's top 100 hits ordered by their ranking (1 to 100)

SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE artist = 'Madonna'
ORDER BY year_rank



All of Madonna's top 100 hits ordered by their ranking within each year

SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE artist = 'Madonna'
ORDER BY year, year_rank


Every number 1 song since 1990 followed by every number 2 song since 1990 and number 3 song since 1990. (Hint: Multiple ordering)

SELECT *
FROM tutorial.billboard_top_100_year_end 
WHERE year >= 1990
ORDER BY year_rank, year
