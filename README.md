# Movie_Data_Analysis



<img width="298" alt="front page" src="https://github.com/user-attachments/assets/36424cbe-ee34-4339-95cd-a56e4643eb57" />


## Table of Content

- [Project Overview](#project-overview)
- [Tools used](#tools-used)
- [Dataset](#dataset)
- [Objectives](#objectives)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Visualization](#visualization)
- [Key Findings](#key-findings) 


# Project Overview

This analysis aims to provide insights into major trends and patterns in the films dataset to guide decision making for a new movie producer. The dataset contains information such as title, release year, genres, gross, budget, and other features relevant to understanding the film industry. The dataset was explored using SQL for detailed analysis, and Tableau to present key findings using an interactive dashboard. 

## Tools used: 

**PostgreSql:** Querying, Cleaning, and analyzing the data

**Tableau:** For data visualization via an interactive dashboard

**Github:** Hosting the project documentation 


## Dataset
**Source:** The dataset used was provided by Techway Consult for the sole purpose of learning. The dataset is not of a real company. 

**Size:** The dataset contains 4000+ records. 

## Objectives
A new movie producer wants to understand the trends and patterns of the movie industry to gain insights into countries where films perform exceptionally well based on box office revenues, and average profit with the corresponding language.

## Exploratory Data Analysis
To provide answers to the following questions and summarize key findings using a tableau dashboard. 
- What are the top 10 highest-grossing films in the database, and when were they released? 
- How many films in the database were released in each country, and what are the top five countries?
- How many films are available in each language, and what are the top three languages represented?
- What is the average IMDb score for films in the database? 
- Which country has made the highest profit from movies? 
- Which movie made the highest profit in the 21st century? 
- How many people in the database are still alive?
- Which year has the highest number of movie releases? 
- Determine the top 10 people with the most roles in the database. 
- Who are the top 10 actors or directors with the most roles in the database? 
- Identify how many people in the database are still alive. 
- Calculate the average number of users and critic reviews for films. 
- Identify films with the highest number of users and critic reviews. 
- Which films have the most Facebook likes, and is there a correlation with their IMDb scores

  ## Data Analysis 

```Sql Query
Sql Query
--  1. What are the top 10 highest-grossing films in the database and when were they released?

SELECT title, gross,  release_year
FROM films
WHERE gross IS NOT NULL
ORDER BY gross DESC
LIMIT 10;

--2 How many films in the database were released in each country, and what are the top five countries?
SELECT country, COUNT(title) AS number_of_movies 
FROM films
GROUP BY country
ORDER BY number_of_movies DESC
LIMIT 5;

--3 How many films are available in each language, and what are the top three languages represented?

SELECT language, count (title) AS movie_lang
FROM films
GROUP BY language
ORDER BY movie_lang DESC
LIMIT 3;

-- 4 What is the average IMDb score for films in the database?

SELECT AVG(imdb_score) AS imdb_ave
FROM reviews;

--5 Which country has made the highest profit from movies?

SELECT country, AVG(gross-budget) AS Profit
FROM films
WHERE gross IS NOT NULL AND budget IS NOT NULL
GROUP BY country
ORDER BY Profit DESC
LIMIT 1;

--6 Which movie made the highest profit in the 21st century?

SELECT title, release_year, AVG(gross-budget) AS Profit
FROM films
WHERE release_year >=2001 
	AND gross IS NOT NULL AND budget IS NOT NULL
GROUP BY title, release_year
ORDER BY Profit DESC
LIMIT 1;


--7 How many people in the database are still alive?

SELECT COUNT(*) AS alive
FROM people
WHERE deathdate IS NULL;


--8 Which year has the highest number of movie releases?

SELECT release_year, COUNT(title) AS highest_movie_year
FROM films
GROUP BY release_year
ORDER BY highest_movie_year DESC
LIMIT 1;

--9 Determine the top 10 people with the most roles in the database.

SELECT name, COUNT(role) AS num_of_roles
FROM people
JOIN roles 
ON people.id=roles.id
GROUP BY name
ORDER BY num_of_roles DESC
LIMIT 10;

--10 Who are the top 10 actors or directors with the most roles in the database?

SELECT name, COUNT(role) AS num_of_roles
FROM people
RIGHT JOIN roles ON people.id=roles.id
WHERE role IN ('actor', 'director') 
	AND name IS NOT NULL
	AND role IS NOT NULL
GROUP BY name
ORDER BY num_of_roles DESC
LIMIT 10;

--11 Identify how many people in the database are still alive

SELECT COUNT(*) AS not_dead
FROM people
WHERE deathdate IS NULL;

--12 Calculate the average number of users and critic reviews for films.

SELECT
	AVG (num_user) AS avg_user,
	AVG(num_critic) AS avg_critic
FROM reviews;

--13 Identify films with the highest number of user and critic reviews.

(SELECT title, num_user AS highest_user
FROM films
JOIN reviews ON films.id=reviews.id
WHERE num_user IS NOT NULL
ORDER BY num_user DESC
LIMIT 1)
UNION
(SELECT title, num_critic 
FROM films
JOIN reviews ON films.id=reviews.id
WHERE num_critic IS NOT NULL
ORDER BY num_critic DESC
LIMIT 1);

--14 Which films have the most Facebook likes, and is there a correlation with their IMDb scores?

SELECT title, facebook_likes, imdb_score
FROM films
JOIN reviews ON films.id=reviews.id 
LIMIT 10;
```
## Results 
### Top 10 higest grossing movies

  
<img width="215" alt="top 10 highest grossing movies" src="https://github.com/user-attachments/assets/9349ff73-a23c-4479-843a-ab46a8bb8e34" />


### Top 5 countries with the highest movie releases

<img width="222" alt="Top 5 countries with the highest releases  " src="https://github.com/user-attachments/assets/b33b6bea-0bee-4f92-94c6-6460a6ab6b9d" />



### Top 3 languages represented

<img width="205" alt="Top 3 languages represented" src="https://github.com/user-attachments/assets/dbb7df0b-a4e4-4f5b-b171-ddd2d1b5546e" />



### 21st Century highest profiting movie


<img width="257" alt="21st century highest profiting  " src="https://github.com/user-attachments/assets/2dd09a89-f016-41a8-89c8-c716f6a61120" />




### Top profiting country


<img width="236" alt="Top profiting country" src="https://github.com/user-attachments/assets/908392d7-b2e9-4739-9f52-bfa10af05d43" />


## Visualization 



<img width="590" alt="Tableau dashboard for the films dataset  " src="https://github.com/user-attachments/assets/349fa0e8-2548-488c-b3f0-363b3ab53424" />


## Key Findings

- A total of 4635 movies were released in English Language followed by French (72) and Spanish (40) showing a global reach of these languages. making English the top language in the films industry. 

- USA released the highest number of films totaling up to 3750 followed by UK and France showing a global acceptance of Hollywood movies, and UK and France cinema movies. 

- Taiwan made a total profit of $46,340,682 making it the highest profit country 

- The movie, Star wars: Episode VII: The force awakens released in 2015 made a total $691,627,416 as profit making it the most profitable movie in the 21st century. 

- The Avengers however, tops the highest grossing movie with a sum of $1,246,559,094.


