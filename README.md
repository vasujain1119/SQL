**SELECT from Nobel Tutorial**
-- 1. Change the query shown so that it displays Nobel prizes for 1950.
  SELECT yr, subject, winner
  FROM nobel
  WHERE yr = 1950
--2.Show who won the 1962 prize for literature.
   SELECT winner
   FROM nobel
   WHERE yr = 1962
   AND subject = 'literature'
--3.Show the year and subject that won 'Albert Einstein' his prize.
     SELECT yr, subject
     FROM nobel
     WHERE  winner =  'Albert Einstein'
--4.Give the name of the 'peace' winners since the year 2000, including 2000.
      SELECT winner
      FROM nobel
      WHERE yr >= 2000
      AND subject = 'peace'
--5. Show all details (yr, subject, winner) of the literature prize winners for 1980 to 1989 inclusive.
      SELECT yr, subject, winner
      FROM nobel
      WHERE subject = 'Literature' AND yr BETWEEN 1980 AND 1989
--6. Show all details of the presidential winners:
Theodore Roosevelt
Thomas Woodrow Wilson
Jimmy Carter
Barack Obama
       SELECT * FROM nobel
 WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter', 
                   'Barack Obama')

--7. Show the winners with first name John
        SELECT winner
        FROM nobel
        WHERE winner LIKE 'John%'
--8. Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984.
          SELECT* 
         FROM nobel
          WHERE yr = 1980 AND subject = 'physics'
          OR yr = 1984 AND subject ='chemistry'

--9. Show the year, subject, and name of winners for 1980 excluding chemistry and medicine
       SELECT *
       FROM nobel
        WHERE yr = 1980 AND subject NOT IN ('chemistry' , 'medicine')
--10. Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)
           SELECT *
           FROM nobel
           WHERE yr<1910 AND subject ='Medicine'
           OR yr>=2004 AND subject =   'Literature' 


--11. Find all details of the prize won by PETER GRÜNBERG  Non-ASCII characters .The u in his name has an umlaut. You may find this link useful
            SELECT *
            FROM nobel
            WHERE winner = 'PETER GRÜNBERG'

--12. Find all details of the prize won by EUGENE O'NEILL Escaping single quotesYou can't put a single quote in a quote string directly. You can use two single quotes within a quoted string.
            SELECT *
          FROM nobel
          WHERE winner = "EUGENE O''NEILL"
--13.List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.
            SELECT winner,yr,subject FROM nobel
            WHERE winner LIKE 'Sir%'                (SELECT * NOT WORKIN NOR subject,yr,winner)
           ORDER BY yr DESC, winner ASC


--14.The expression subject IN ('chemistry','physics') can be used as a value - it will be 0 or 1.Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last.
                   SELECT winner, subject
                   FROM nobel
                   WHERE yr=1984
                 ORDER BY subject IN ('physics','chemistry'),subject,winner



**SELECT within SELECT Tutorial**

--1. List each country name where the population is larger than that of 'Russia'.


   SELECT name FROM world
   WHERE population >
   (SELECT population FROM world
   WHERE name='Russia')

--2. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

  SELECT name FROM world
  WHERE continent = 'Europe' AND  gdp/population >
  (SELECT gdp/population FROM world
  WHERE name = 'United Kingdom')

--3.List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

     SELECT name, continent 
    FROM world
    WHERE continent IN
    (SELECT continent FROM world 
    WHERE name = 'Argentina' OR name = 'Australia')
    ORDER BY name

--4.Which country has a population that is more than United Kingdom but less than Germany? Show the name and the population.

       SELECT name ,population
       FROM world
      WHERE population > 
    (SELECT population FROM world
      WHERE name='United Kingdom')
      AND population <
     (SELECT population FROM world
      WHERE name='Germany')


--5. Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
          SELECT name, CONCAT(ROUND (100*population/ 
     (SELECT population FROM world
      WHERE name='Germany')), '%')AS 'percentage'
FROM world
  WHERE continent ='Europe'

--6Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)
       SELECT name
        FROM world
         WHERE gdp > (
          SELECT MAX(gdp)
              FROM world
               WHERE continent = 'Europe' AND gdp > 0)


  --7 
                      
