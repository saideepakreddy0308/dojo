---
title: Introduction to SQL
tags: database,structured-query-language
url: https://campus.datacamp.com/courses/introduction-to-sql
---

# 1. Selecting columns
## Onboarding | Query Result
```sql
SELECT name FROM people;
```

## Onboarding | Errors
```sql
-- Try running me!
SELECT 'DataCamp <3 SQL' AS result;
```

## Onboarding | Multi-step Exercises
```sql
SELECT 'SQL is cool'
AS result;
```

## Beginning your SQL journey
```sql
##
SELECT title
FROM tilms;

##
SELECT release_year
FROM films;

##
SELECT name
FROM people;
```

## SELECTing multiple columns
```sql
##
SELECT * FROM films;

##
SELECT title, release_year
FROM films;

##
SELECT title, release_year, country
FROM films;
```

## SELECT DISTINCT
```sql
##
SELECT DISTINCT country FROM films;

##
SELECT DISTINCT certification FROM films;

##
SELECT DISTINCT role FROM roles;
```

## Learning to COUNT
```sql
SELECT COUNT(*) FROM reviews;
-- 4968
```

## Practice with COUNT
```sql
##
SELECT COUNT(*) FROM people;

##
SELECT COUNT(birthdate)
FROM people;

##
SELECT COUNT(DISTINCT birthdate)
FROM people;

##
SELECT COUNT(DISTINCT language) FROM films;

##
SELECT COUNT(DISTINCT country) FROM films;
```




# 2. Filtering rows
## Simple filtering of numeric values
```sql
##
SELECT *
FROM films
WHERE release_year = 2016;

##
SELECT COUNT(*)
FROM films
WHERE release_year < 2000;

##
SELECT title, release_year
FROM films
WHERE release_year > 2000;
```

## Simple filtering of text
```sql
##
SELECT *
FROM films
WHERE language = 'French';

##
SELECT name, birthdate
FROM people
WHERE birthdate = '1974-11-11';

##
SELECT COUNT(*)
FROM films
WHERE language = 'Hindi';

##
SELECT *
FROM films
WHERE certification = 'R';
```

## WHERE AND
```sql
##
SELECT title, release_year
FROM films
WHERE language = 'Spanish' AND release_year < 2000;

##
SELECT *
FROM films
WHERE language = 'Spanish' AND release_year > 2000;

##
SELECT *
FROM films
WHERE language = 'Spanish'
  AND release_year > 2000
  AND release_year < 2010;
```

## WHERE AND OR (2)
```sql
##
SELECT title, release_year
FROM films
WHERE release_year >= 1990 AND release_year < 2000;

##
SELECT title, release_year
FROM films
WHERE (release_year >= 1990 AND release_year < 2000)
AND (language = 'French' OR language = 'Spanish');

##
SELECT title, release_year
FROM films
WHERE (release_year >= 1990 AND release_year < 2000)
AND (language = 'French' OR language = 'Spanish')
AND (gross >= 2000000);
```

## BETWEEN (2)
```sql
SELECT title, release_year
FROM films
WHERE release_year BETWEEN 1990 AND 2000
AND budget > 100000000
AND (language = 'Spanish' OR language = 'French');
```

## WHERE IN
```sql
##
SELECT title, release_year
FROM films
WHERE release_year IN (1990, 2000)
AND duration > 120;

##
SELECT title, language
FROM films
WHERE language IN ('English', 'Spanish', 'French');

##
SELECT title, certification
FROM films
WHERE certification IN ('NC-17', 'R');
```

## NULL and IS NULL
```sql
##
SELECT name
FROM people
WHERE deathdate IS NULL;

##
SELECT title
FROM films
WHERE budget IS NULL;

##
SELECT COUNT(*)
FROM films
WHERE language IS NULL;
```

## LIKE and NOT LIKE
```sql
##
SELECT name
FROM people
WHERE name LIKE 'B%';

##
SELECT name
FROM people
WHERE name LIKE '_r%';

##
SELECT name
FROM people
WHERE name NOT LIKE 'A%';
```




# 3. Aggregate Functions
## Aggregate functions
```sql
##
SELECT SUM(duration)
FROM films;

##
SELECT AVG(duration)
FROM films;

##
SELECT MIN(duration)
FROM films;

##
SELECT MAX(duration)
FROM films;
```

## Aggregate functions practice
```sql
##
SELECT SUM(gross)
FROM films;

##
SELECT AVG(gross)
FROM films;

##
SELECT MIN(gross)
FROM films;

##
SELECT MAX(gross)
FROM films;
```

## Combining aggregate functions with WHERE
```sql
##
SELECT SUM(gross)
FROM films
WHERE release_year >= 2000;

##
SELECT AVG(gross)
FROM films
WHERE title LIKE 'A%';

##
SELECT MIN(gross)
FROM films
WHERE release_year = 1994;

##
SELECT MAX(gross)
FROM films
WHERE release_year BETWEEN 2000 AND 2012;
```

## A note on arithmetic
```sql
SELECT (10/3);
-- 3
```

## It's AS simple AS aliasing
```sql
##
SELECT title, gross - budget AS net_profit
FROM films;

##
SELECT title, duration/60.0 AS duration_hours
FROM films;

##
SELECT AVG(duration)/60.0 AS avg_duration_hours
FROM films;
```

## Even more aliasing
```sql
##
-- get the count(deathdate) and multiply by 100.0
-- then divide by count(*)
SELECT COUNT(deathdate)*100.0/COUNT(*) AS percentage_dead
FROM people;

##
SELECT MAX(release_year) - MIN(release_year) AS difference
FROM films;

##
SELECT (MAX(release_year) - MIN(release_year)) / 10.0 AS number_of_decades
FROM films;
```




# 4. Sorting and grouping
## ORDER BY
```sql
##
SELECT name
FROM people
ORDER BY name ASC;

##
SELECT name
FROM people
ORDER BY birthdate ASC;

##
SELECT birthdate, name
FROM people
ORDER BY birthdate ASC;
```

## Sorting single columns (2)
```sql
##
SELECT title
FROM films
WHERE release_year = 2000 OR release_year = 2012;

##
SELECT *
FROM films
WHERE release_year <> 2015
ORDER BY duration ASC;

##
SELECT title, gross
FROM films
WHERE title LIKE 'M%'
ORDER BY title ASC;
```

## Sorting single columns (DESC)
```sql
##
SELECT imdb_score, film_id
FROM reviews
ORDER BY imdb_score DESC;

##
SELECT title
FROM films
ORDER BY title DESC;

##
SELECT title, duration
FROM films
ORDER BY duration DESC;
```

## Sorting multiple columns
```sql
##
SELECT birthdate, name
FROM people
ORDER BY birthdate ASC, name ASC;

##
SELECT release_year, duration, title
FROM films
ORDER BY release_year ASC, duration ASC;

##
SELECT certification, release_year, title
FROM films
ORDER BY certification ASC, release_year ASC;

##
SELECT name, birthdate
FROM people
ORDER BY name ASC, birthdate ASC;
```

## GROUP BY practice
```sql
##
SELECT release_year, COUNT(*)
FROM films
GROUP BY release_year;

##
SELECT release_year, AVG(duration)
FROM films
GROUP BY release_year;

##
SELECT release_year, MAX(budget)
FROM films
GROUP BY release_year;

##
SELECT imdb_score, COUNT(*)
FROM reviews
GROUP BY imdb_score;
```

## GROUP BY practice (2)
```sql
##
SELECT release_year, MIN(gross)
FROM films
GROUP BY release_year;

##
SELECT language, SUM(gross)
FROM films
GROUP BY language;

##
SELECT country, SUM(budget)
FROM films
GROUP BY country;

##
SELECT release_year, country, MAX(budget)
FROM films
GROUP BY release_year, country
ORDER BY release_year, country;

##
SELECT country, release_year, MIN(gross)
FROM films
GROUP BY release_year, country
ORDER BY country, release_year
```

## HAVING a great time
```sql
SELECT COUNT(t.c1) FROM (
  SELECT release_year AS c1
  FROM films
  GROUP BY release_year
  HAVING COUNT(title) > 200
) AS t;
```

## All together now
```sql
##
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year;

##
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
GROUP BY release_year
HAVING AVG(budget) >= 60000000;

##
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
FROM films
WHERE release_year > 1990
GROUP BY release_year
HAVING AVG(budget) > 60000000
ORDER BY AVG(gross) DESC;
```

## All together now (2)
```sql
-- select country, average budget, 
--     and average gross
SELECT country, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross
-- from the films table
FROM films
-- group by country 
GROUP BY country
-- where the country has more than 10 titles
HAVING COUNT(title) > 10
-- order by country
ORDER BY country
-- limit to only show 5 results
LIMIT 5;
```

## A taste of things to come
```sql
##
SELECT title, imdb_score
FROM films
JOIN reviews
ON films.id = reviews.film_id
WHERE title = 'To Kill a Mockingbird';
```
