# SQL_Exe
https://www.edx.org/course/databases-5-sql \
<br/>
Q1:\
<br/>
SELECT title FROM Movie WHERE director = "Steven Spielberg"\
<br/>
Q2:\
<br/>
SELECT distinct Movie.year FROM Movie, Rating \
WHERE Movie.mID = rating.mID AND Rating.stars >=4 \
ORDER BY Movie.year ASC\
<br/>
Q3:\
<br/>
SELECT distinct Movie.title \
FROM Movie left join Rating on Movie.mID = Rating.mID \
WHERE Rating.stars is null\
<br/>
Q4:\
<br/>
SELECT Reviewer.name \
FROM Reviewer, Rating \
WHERE Rating.rId = Reviewer.rID AND Rating.ratingDate is null\
<br/>
Q5:\
<br/>
SELECT Reviewer.name, Movie.title, Rating.stars, Rating.ratingDate \
FROM Movie, Reviewer, Rating \
WHERE Movie.mID = Rating.mID AND Reviewer.rID = Rating.rID ORDER BY Reviewer.name,Movie.title,Rating.stars\
<br/>
Q6:\
<br/>
SELECT name, title\
FROM Movie\
INNER JOIN Rating R1 USING(mId)\
INNER JOIN Rating R2 USING(rId)\
INNER JOIN Reviewer USING(rId)\
WHERE R1.mId = R2.mId AND R1.ratingDate < R2.ratingDate AND R1.stars < R2.stars;\
<br/>
Q7:\
<br/>
SELECT title, MAX(stars)\
FROM Movie\
INNER JOIN Rating USING(mId)\
GROUP BY title\
ORDER BY title;\
<br/>
Q8:\
<br/>
SELECT title, (MAX(stars) - MIN(stars)) AS r\
FROM Movie\
INNER JOIN Rating USING(mId)\
GROUP BY mId\
ORDER BY r DESC, title;\
<br/>
Q9:\
<br/>
SELECT AVG(Before.avg) - AVG(After.avg) \
FROM \
&nbsp;( \
    &nbsp;&nbsp;SELECT AVG(stars) AS avg \
    &nbsp;&nbsp;FROM Movie, Rating  \
    &nbsp;&nbsp;WHERE Movie.mId = Rating.mId and Movie.year < 1980 GROUP BY Movie.mId\
  &nbsp;) AS Before,\
  &nbsp;(\
    &nbsp;&nbsp;SELECT AVG(stars) AS avg \
    &nbsp;&nbsp;FROM Movie, Rating  \
    &nbsp;&nbsp;WHERE Movie.mId = Rating.mId and Movie.year > 1980 GROUP BY Movie.mId\
  &nbsp;&nbsp;) AS After;\
