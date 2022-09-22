# SQLBOLT-Queris-Solutions

## Visit [Sql Bolt](https://sqlbolt.com/lesson/select_queries_introduction)

## Exercise 1 — Tasks

### 1.Find the title of each film

SELECT title FROM movies;

## 2.Find the director of each film

SELECT director FROM movies;

## 3.Find the title and director of each film

SELECT title,director FROM movies;

## 4.Find the title and year of each film

SELECT title,year FROM movies;

## 5.Find all the information about each film

SELECT * FROM movies;

# Exercise 2 — Tasks

## 1.Find the movie with a row id of 6

SELECT title FROM movies
where id=6;

## 2.Find the movies released in the years between 2000 and 2010

SELECT * FROM movies WHERE year BETWEEN 2000 AND 2010;

## 3.Find the movies not released in the years between 2000 and 2010

SELECT * FROM movies WHERE year NOT BETWEEN 2000 AND 2010;

## 4.Find the first 5 Pixar movies and their release year

SELECT title, year FROM movies
ORDER BY year
LIMIT 5;

# Exercise 3 — Tasks

## 1.Find all the Toy Story movies

SELECT title FROM movies
WHERE title LIKE '%Toy Story%';

## 2.Find all the movies directed by John Lasseter

SELECT * FROM movies
WHERE director = "John Lasseter";

## 3.Find all the movies (and director) not directed by John Lasseter

SELECT * FROM movies
WHERE NOT director = "John Lasseter";

## 4.Find all the WALL-* movies

SELECT * FROM movies
WHERE title LIKE 'WALL-%';

# Exercise 4 — Tasks

## 1.List all directors of Pixar movies (alphabetically), without duplicates

SELECT distinct(director) FROM movies
order by director asc;

## 2.List the last four Pixar movies released (ordered from most recent to least)

SELECT title FROM movies
order by Year desc
limit 4;

## 3.List the first five Pixar movies sorted alphabetically

SELECT title FROM movies
order by title asc
limit 5;

## 4.List the next five Pixar movies sorted alphabetically 

SELECT title FROM movies
ORDER BY title ASC
LIMIT 5 OFFSET 5;

# Exercise 5 — Tasks

## 1.List all the Canadian cities and their populations

SELECT city, population 
FROM north_american_cities
where country = 'Canada';

## 2.Order all the cities in the United States by their latitude from north to south

SELECT city FROM north_american_cities
where country= 'United States'
order by latitude desc;

## 3.List all the cities west of Chicago, ordered from west to east

SELECT city
FROM north_american_cities
WHERE longitude < -87.629798
ORDER BY longitude;

## 4.List the two largest cities in Mexico (by population)

SELECT city
FROM north_american_cities
where country = 'Mexico'
order by population desc
limit 2;

## 5.List the third and fourth largest cities (by population) in the United States and their population

SELECT city
FROM north_american_cities
where country = 'United States'
order by population desc
limit 2 offset 2;

# Exercise 6 — Tasks

## 1.Find the domestic and international sales for each movie 

select  Domestic_sales, International_sales, title from Boxoffice b
join Movies m 
on b.movie_id = m.id;

## 2.Show the sales numbers for each movie that did better internationally rather than domestically

select   domestic_sales, international_sales, title from Boxoffice b
join Movies m 
on b.movie_id = m.id
where international_sales > domestic_sales;

## 3.List all the movies by their ratings in descending order
select title from Boxoffice b
join Movies m 
on b.movie_id = m.id
order by rating desc;

# Exercise 7 — Tasks

## 1.Find the list of all buildings that have employees

select distinct building from employees;

## 2.Find the list of all buildings and their capacity

select * from buildings;

## 3. List all buildings and the distinct employee roles in each building (including empty buildings)

SELECT DISTINCT building_name, role
FROM buildings
LEFT JOIN employees
ON building_name = employees.building;

# Exercise 8 — Tasks

## 1.Find the name and role of all employees who have not been assigned to a building

SELECT name, role FROM employees
where building is null;

## 2.Find the names of the buildings that hold no employees

SELECT distinct building_name
from buildings b
left join employees e
on b.building_name = e.building
where e.name is null;

# Exercise 9 — Tasks

## 1.List all movies and their combined sales in millions of dollars

SELECT DISTINCT title, (domestic_sales + international_sales) / 1000000 AS sales
FROM movies
INNER JOIN boxoffice
ON movies.id = boxoffice.movie_id;

## 2.List all movies and their ratings in percent

SELECT DISTINCT title, rating*10 as rating_percent
FROM movies
INNER JOIN boxoffice
ON movies.id = boxoffice.movie_id;

## 2.List all movies that were released on even number years

select title from movies
where year%2=0;

# Exercise 10 — Tasks

## 1.Find the longest time that an employee has been at the studio 

SELECT max(years_employed) FROM employees;

## 2.For each role, find the average number of years employed by employees in that role

SELECT role, avg(years_employed) FROM employees
group by role;

## 3.Find the total number of employee years worked in each building

SELECT building, SUM(years_employed) FROM employees GROUP BY building;

# Exercise 11 — Tasks

## 1.Find the number of Artists in the studio (without a HAVING clause) 

SELECT role, count(*) FROM employees
where role  = 'Artist';

## 2.Find the number of Employees of each role in the studio

select role, count(*) as Number_of_Employee from employees
group by role;

## 3.Find the total number of years employed by all Engineers

select role, sum(years_employed) from employees
where role= 'Engineer';

# Exercise 12 — Tasks

## 1.Find the number of movies each director has directed 

SELECT director, count(title) FROM movies
group by director;

## 2.Find the total domestic and international sales that can be attributed to each director

SELECT *, sum(Domestic_sales+international_sales) as total_sales FROM movies m
inner join Boxoffice b
on m.id = b.movie_id
group by director;

# Exercise 13 — Tasks

## 1.Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)

INSERT INTO  movies VALUES (15, 'Toy Story 4', 'Brad Bird', 2021, 100);

## 2.Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table 

INSERT INTO Boxoffice VALUES(15,8.7,340000000,270000000);

# Exercise 14 — Tasks

## 1.The director for A Bug's Life is incorrect, it was actually directed by John Lasseter

UPDATE Movies
SET Director = 'John Lasseter'
WHERE title = "A Bug's Life";

## 2.The year that Toy Story 2 was released is incorrect, it was actually released in 1999 

UPDATE Movies
SET Year = 1999
WHERE Title = "Toy Story 2";

## 3.Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich

UPDATE Movies 
SET Title = 'Toy Story 3' , Director = "Lee Unkrich"
WHERE Title = 'Toy Story 8';

# Exercise 15 — Tasks

## 1.This database is getting too big, lets remove all movies that were released before 2005.

DELETE FROM Movies
WHERE year<2005;

## 2.Andrew Stanton has also left the studio, so please remove all movies directed by him.

DELETE FROM movies WHERE director = "Andrew Stanton";

# Exercise 16 — Tasks

##Create a new table named Database with the following columns:
– Name A string (text) describing the name of the database
– Version A number (floating point) of the latest version of this database
– Download_count An integer count of the number of times this database was downloaded
##This table has no constraints.

CREATE TABLE Database(
Name varchar(50),
Version float,
Download_count int);

# Exercise 17 — Tasks

## 1.Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in

Alter table Movies
ADD  Aspect_ratio float;

## 2.Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.

Alter table Movies
ADD  Language varchar(50) DEFAULT 'English';

# Exercise 18 — Tasks

## 1.We've sadly reached the end of our lessons, lets clean up by removing the Movies table 

DROP Table Movies;

## 2.And drop the BoxOffice table as well

DROP Table BoxOffice;
 











