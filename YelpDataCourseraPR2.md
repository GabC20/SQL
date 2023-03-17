# **Part 1: Yelp Dataset Profiling and Understating**

## _**1. Total Number of records for each of the tables below:**_

### i. Attribute Table

```sql
SELECT COUNT(*) AS NumRecords
FROM attribute 
```
> **Number of Records Attribute Table: 10000**

### ii. Business Table

```sql
SELECT COUNT(*) AS NumRecords
FROM business
```
> **Number of Records Business Table: 10000**

### iii. Category Table

```sql
SELECT COUNT(*) AS NumRecords
FROM category
```
> **Number of Records Category
 Table: 10000**

 ### iv. Checkin Table

```sql
SELECT COUNT(*) AS NumRecords
FROM checkin
```
> **Number of Records Checkin
 Table: 10000**

 ### v. Elite_Years Table

```sql
SELECT COUNT(*) AS NumRecords
FROM elite_years
```
> **Number of Records Elite_Years
 Table: 10000**

 ### vi. Friend Table

```sql
SELECT COUNT(*) AS NumRecords
FROM friend
```
> **Number of Records Friend
 Table: 10000**

 ### vii. Hours Table

```sql
SELECT COUNT(*) AS NumRecords
FROM hours
```
> **Number of Records Hours
 Table: 10000**

 ### viii. Photo Table

```sql
SELECT COUNT(*) AS NumRecords
FROM photo
```
> **Number of Records Photo
 Table: 10000**

 ### ix. Review Table

```sql
SELECT COUNT(*) AS NumRecords
FROM review
```
> **Number of Records Review
 Table: 10000**

 ### x. Tip Table

```sql
SELECT COUNT(*) AS NumRecords
FROM tip
```
> **Number of Records Tip
 Table: 10000**

 ### xi. User Table

```sql
SELECT COUNT(*) AS NumRecords
FROM user
```
> **Number of Records User
 Table: 10000**


## _**2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.**_

### i. Business Table

```sql
SELECT COUNT(DISTINCT id) AS DistinctRecords
FROM business
```
> **Number of Distinct Records from Business Table: 10000, PrimaryKey = id**


### ii. Hours Table

```sql
SELECT COUNT(DISTINCT(business_id)) AS DistinctRecords
FROM hours
```
> **Number of Distinct Records from Hours Table: 1562, ForeignKey = business_id**

### iii. Category Table

```sql
SELECT COUNT(DISTINCT(business_id)) AS DistinctRecords
FROM category
```
> **Number of Distinct Records from Category Table: 2643, ForeignKey = business_id**

### iv. Attribute Table

```sql
SELECT COUNT(DISTINCT(business_id)) AS DistinctRecords
FROM attribute
```
> **Number of Distinct Records from Attribute Table: 1115, ForeignKey = business_id**

### v. Review Table

```sql
SELECT COUNT(DISTINCT id), COUNT(DISTINCT business_id), COUNT(DISTINCT user_id) 
FROM review
```
> **Number of Distinct Records from Attribute Table: 10000, PrimaryKey = id**

> **Number of Distinct Records from Attribute Table: 8090, ForeignKey = business_id**

> **Number of Distinct Records from Attribute Table: 9581, ForeignKey = user_id**

### vi. Checkin Table

```sql
SELECT COUNT(DISTINCT(business_id)) AS DistinctRecords
FROM checkin
```
> **Number of Distinct Records from Checkin Table: 493, ForeignKey = id**

### vii. Photo Table

```sql
SELECT COUNT(DISTINCT(id)), COUNT(DISTINCT(business_id)) 
FROM photo
```
> **Number of Distinct Records from Photo Table: 10000, PrimaryKey = id**

> **Number of Distinct Records from Photo Table: 6493, ForeignKey = business_id**

### viii. Tip Table

```sql
SELECT COUNT(DISTINCT(user_id)), COUNT(DISTINCT(business_id)) 
FROM tip
```
> **Number of Distinct Records from Tip Table: 537, ForeignKey = user_id**

> **Number of Distinct Records from Tip Table: 3979, ForeignKey = business_id**

### ix. User Table

```sql
SELECT COUNT(DISTINCT(id))
FROM user
```
> **Number of Distinct Records from User Table: 10000, PrimaryKey = user_id**

### x. Friend Table

```sql
SELECT COUNT(DISTINCT(user_id))
FROM friend
```
> **Number of Distinct Records from Friend Table: 11, ForeignKey = user_id**

### xi. Elite_Years Table

```sql
SELECT COUNT(DISTINCT(user_id))
FROM elite_years
```
> **Number of Distinct Records from Elite_Years Table: 2780, ForeignKey = user_id**



## _**3. Are there any columns with null values in the Users table? Indicate "yes," or "no."**_

> **No**

```sql
SELECT COUNT(*) AS NumNullColumns
FROM user
WHERE 
    id IS NULL OR
    name IS NULL OR
    review_count IS NULL OR
    yelping_since IS NULL OR
    useful IS NULL OR
    funny IS NULL OR
    cool IS NULL OR
    fans IS NULL OR
    average_stars IS NULL OR
    compliment_hot IS NULL OR
    compliment_more IS NULL OR
    compliment_profile IS NULL OR
    compliment_cute IS NULL OR
    compliment_list IS NULL OR
    compliment_note IS NULL OR
    compliment_plain IS NULL OR
    compliment_cool IS NULL OR
    compliment_writer IS NULL OR
    compliment_photos IS NULL 
```

## _**4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:**_

### i. Table: Review, Column: Stars

```sql
SELECT MIN(stars), MAX(stars), AVG(stars)
FROM review
```

> **Min: 1  
Max: 5  
Avg: 3.7082**

### ii. Table: Business, Column: Stars

```sql
SELECT MIN(stars), MAX(stars), AVG(stars)
FROM business
```

> **Min: 1.0  
Max: 5.0  
Avg: 3.6549**

### iii. Table: Tip, Column: Likes

```sql
SELECT MIN(likes), MAX(likes), AVG(likes)
FROM tip
```

> **Min: 0  
Max: 2  
Avg: 0.0144**

### iv. Table: Checkin, Column: Count

```sql
SELECT MIN(count), MAX(count), AVG(count)
FROM checkin
```

> **Min: 1  
Max: 53  
Avg: 1.9414**

### v. Table: User, Column: Review_count

```sql
SELECT MIN(count), MAX(count), AVG(count)
FROM checkin
```

> **Min: 0  
Max: 2000  
Avg: 24.2995**


## _**5. List the cities with the most reviews in descending order:**_

```sql
SELECT city, SUM(review_count) AS ReviewSumByCity
FROM business
GROUP BY city
ORDER BY ReviewSumByCity DESC
```

> **Result:**

| city            | ReviewSumByCity |
|-----------------|-----------------|
| Las Vegas       |           82854 |
| Phoenix         |           34503 |
| Toronto         |           24113 |
| Scottsdale      |           20614 |
| Charlotte       |           12523 |
| Henderson       |           10871 |
| Tempe           |           10504 |
| Pittsburgh      |            9798 |
| Montréal        |            9448 |
| Chandler        |            8112 |
| Mesa            |            6875 |
| Gilbert         |            6380 |
| Cleveland       |            5593 |
| Madison         |            5265 |
| Glendale        |            4406 |
| Mississauga     |            3814 |
| Edinburgh       |            2792 |
| Peoria          |            2624 |
| North Las Vegas |            2438 |
| Markham         |            2352 |
| Champaign       |            2029 |
| Stuttgart       |            1849 |
| Surprise        |            1520 |
| Lakewood        |            1465 |
| Goodyear        |            1155 |

(Output limit exceeded, 25 of 362 total rows shown)

## _**6. Find the distribution of star ratings to the business in the following cities:**_

### i. Avon

```sql
SELECT SUM(review_count) AS ReviewsPerStars, stars
FROM business
WHERE city='Avon'
GROUP BY stars
```

> **Result:**

| ReviewsPerStars | stars |
|-----------------|-------|
|              10 |   1.5 |
|               6 |   2.5 |
|              88 |   3.5 |
|              21 |   4.0 |
|              31 |   4.5 |
|               3 |   5.0 |

### ii. Beachwood

```sql
SELECT SUM(review_count) AS ReviewsPerStars, stars
FROM business
WHERE city='Beachwood'
GROUP BY stars
```

> **Result:**

| ReviewsPerStars | stars |
|-----------------|-------|
|               8 |   2.0 |
|               3 |   2.5 |
|              11 |   3.0 |
|               6 |   3.5 |
|              69 |   4.0 |
|              17 |   4.5 |
|              23 |   5.0 |

## _**7. Find the top 3 users based on their total number of reviews:**_

```sql
SELECT id, name, SUM(review_count) AS TotalReviewsOfUser
FROM user
GROUP BY id
ORDER BY TotalReviewsOfUser DESC
LIMIT 3
```

> **Result:**

| id                     | name   | TotalReviewsOfUser |
|------------------------|--------|--------------------|
| -G7Zkl1wIWBBmD0KRy_sCw | Gerald |               2000 |
| -3s52C4zL_DHRK0ULG6qtg | Sara   |               1629 |
| -8lbUNlXVSoXqaRRiHiSNg | Yuri   |               1339 |


## _**8. Does posing more reviews correlate with more fans?**_

```sql
SELECT FansBins,
       COUNT(*) AS NumUsers,
       AVG(review_count) AS AvgNumOfReviews,
       AVG(fans) AS AvgNumOfFans
FROM (SELECT CASE WHEN fans BETWEEN 0 AND 9 THEN '0 to 9 fans'
                  WHEN fans BETWEEN 10 AND 99 THEN '10 to 99 fans'
                  ELSE '100 to 503 fans' END AS FansBins,
                  review_count,
                  fans
      FROM user) AS aux_table
GROUP BY aux_table.FansBins
```

> First I ran a simple query to discover the person with the most fans (see below):
```sql
SELECT review_count, fans
FROM user
ORDER BY fans DESC
```
> Doing this, we find out that the person with most fans is Amy, with 503 fans. After doing this, the ideia was to create a new table describing ranges of number of fans to see if the number of fans increases with the increase in number of fans. For this I separated the table in three bins describing from 0 to 9 fans, from 10 to 99 and from 100 to 503 fans (the maximum number of fans we discovered earlier). After this we get the average number of reviews for each of the bins and see if the the average number of reviews increases as the number of fans inceases. After querying the database as described in the first SQL query, we get this table:

| FansBins        | NumUsers | AvgNumOfReviews |   AvgNumOfFans |
|-----------------|----------|-----------------|----------------|
| 0 to 9 fans     |     9690 |   15.0085655315 | 0.447265221878 |
| 10 to 99 fans   |      294 |   283.326530612 |  25.5986394558 |
| 100 to 503 fans |       16 |           891.5 |         189.75 |

> Now, it becomes clear that the number of fans is positively correlated with the number of reviews, as both increase together. However, to get a more precise estimation of the magnitude of this correlation it is necessary to apply a more formal approch and mathematically calculate the correlation between the variables.

## _**9. Are there more reviews with the word "love" or with the word "hate" in them?**_

```sql
SELECT sentiment, COUNT(*) AS SentimentCount
FROM (SELECT CASE WHEN text LIKE '%love%' THEN 'love'
                  WHEN text LIKE '%hate%' THEN 'hate'
                  END AS sentiment
      FROM review) AS aux_table
GROUP BY sentiment
```

> **Result:**

| sentiment | SentimentCount |
|-----------|----------------|
|      None |           8042 |
|      hate |            178 |
|      love |           1780 |

> **From the table above we see that 'love' is mentioned more than hate. There are more reviews with the word 'love'**


## _**10. Find the top 10 users with the most fans:**_

```sql
SELECT id, name, review_count, fans
FROM user
ORDER BY fans DESC
LIMIT 10
```

> **Result:**

| id                     | name      | review_count | fans |
|------------------------|-----------|--------------|------|
| -9I98YbNQnLdAmcYfb324Q | Amy       |          609 |  503 |
| -8EnCioUmDygAbsYZmTeRQ | Mimi      |          968 |  497 |
| --2vR0DIsmQ6WfcSzKWigw | Harald    |         1153 |  311 |
| -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |         2000 |  253 |
| -0IiMAZI2SsQ7VmyzJjokQ | Christine |          930 |  173 |
| -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |          813 |  159 |
| -9bbDysuiWeo2VShFJJtcw | Cat       |          377 |  133 |
| -FZBTkAZEXoP7CYvRV2ZwQ | William   |         1215 |  126 |
| -9da1xk7zgnnfO1uTVYGkA | Fran      |          862 |  124 |
| -lh59ko3dxChBSZ9U7LfUw | Lissa     |          834 |  120 |


# **Part 2: Inferences And Analysis**

## _**1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.**_

After playing a little with the database, I chose the city of "Toronto" and category  "Restaurants" as to obtain the maximum number of ratings for a more significative statistical analysis.

### i. Do the two groups you chose to analyze have a different distribution of hours?

```sql
SELECT CASE WHEN stars >= 2.0 AND stars < 4.0 THEN '2-3 stars'
            WHEN stars >= 4.0 THEN '4-5 stars'
            ELSE 'less than 2 stars' END AS Rating, 
            SUM(DaysOpen)*1.0/COUNT(name) AS DaysOpenPerWeek
FROM(
    -- This level gives a table of restaurants and their number of days open
    SELECT *, COUNT(hours) AS DaysOpen
    FROM(
        -- This level gives a table with all necessary rows and specific city and category
        SELECT name, stars, city, category.category, hours.hours
        FROM (business JOIN category ON business.id=category.business_id 
            JOIN hours ON business.id=hours.business_id)
        WHERE city='Toronto' AND category.category='Restaurants')
    GROUP BY name)
GROUP BY Rating
```


> **This query aims to first join all the data necessary by joining three tables: business, category and hours for the specified city and category. After this, we create another table where the main information is the number of days open for each restaurant. Lastly, we get the rating of each restaurants into bins of 2-3 stars or 4-5 stars and average the number of days open for each bin. This way, we can see the both ratings have a similar average of days open per week, which indicates that the hours distribution between different raitngs is not much different.**

> **Result: The hours distribution is not very different**


| Rating    | DaysOpenPerWeek |
|-----------|-----------------|
| 2-3 stars |             7.0 |
| 4-5 stars |   6.33333333333 |

### ii. Do the two groups you chose to analyze have a different number of reviews?

>
```sql
SELECT CASE WHEN stars >= 2.0 AND stars < 4.0 THEN '2-3 stars'
            WHEN stars >= 4.0 THEN '4-5 stars'
            ELSE 'less than 2 stars' END AS Rating,
            SUM(review_count) AS TotalReviewsByRating
FROM(SELECT name, stars, city, review_count, category.category
     FROM business JOIN category ON business.id=category.business_id
     WHERE city='Toronto' AND category.category='Restaurants')
GROUP BY Rating
```

> **Result: Yes, the 4-5 stars bin has more than double the reviews compared to the 2-3 stars bin**

| Rating            | TotalReviewsByRating |
|-------------------|----------------------|
| 2-3 stars         |                   89 |
| 4-5 stars         |                  206 |
| less than 2 stars |                    4 |


### iii. Are you able to infer anything from the location data provided between these two groups? Explain.

```sql
SELECT
CASE WHEN stars >= 2.0 AND stars < 4.0 THEN '2-3 stars'
WHEN stars >= 4.0 THEN '4-5 stars'
ELSE 'less than 2 stars' END AS Rating, 
name, 
stars, 
city, 
neighborhood, 
state,
postal_code,
latitude,
longitude,
category.category
FROM business JOIN category ON business.id=category.business_id
WHERE city='Toronto' AND category.category='Restaurants'
```
> Plotting a general table with all location attributes, we see that latitude and longitude are of little value because all those numbers are very close to each other and we don't have sense of scale so accurate enough about those attribute as to hypothesize about them. Other location attribute that has little value is the Postal Code sinze we can't identify the actual proximity of the restaurants based on it. 

> **Result: Every restaurant seems to be in a differente location so that makes it hard to make a correlation between location and Rating with this little data.However, wee see that both places on Downtown Core are 2-3 stars rated.**


## _**2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.**_

### i. Difference 1: Closed places have much less reviews than the ones open.

### ii. There's much more places open than closed.

```sql
SELECT is_open, SUM(review_count) AS NumReview, AVG(stars) AS AvgRating, COUNT(is_open) AS Count
FROM business
GROUP BY is_open
```

## _**3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.**_

### i. Indicate the type of analysis you chose to do:

> The analysis I chose to do was to find out if there was a relationship between restaurants rating (mainly), review count and number of open places with the presence of positive or negative words in the tips table, where users write their opinions on the restaurants. For this I defined some words that summarize a tip as positive ("good", "great", "excellent" and "best") or negative ("bad", "worst", "terrible" and "horrible"). 

### ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:

> To make this analysis happen, I need to get data from the tip table and the business table. From the first, I get the tip provided by the users about the business. From the second, I get the number of stars for each restaurant, the number of review and if it is open or not. 

> The process of this analysis can be summarized in some simple steps:
1. Join the tip and bussiness table on the business_id. 
2. Using the join as the referenced table, I aggregate the tips into "positive", "negative" or "None" bins where a restaurant gets put into a bin according to the words found on the tip for that restaurant. For example, if the 'LIKE' operator finds any of the words defined as positive in the list of positive words in the tip, it classifies that review as positive and vice versa for the negative case. However, this is a simple analysis of just a few key words, so naturally a great number of tips will not contain either words from the positive or negative lists. 
3. Lastly, I generate a table with a Classification column (with values 'positive', 'negative' or 'None'), an average rating column, a total number of reviews column and the number of open places.

### iii. Output of your finished dataset:

> The finished table ready for analysis is this:

| Classification |      AvgStars | TotalNumReviews | OpenPlaces |
|----------------|---------------|-----------------|------------|
|           None | 3.74029574861 |           53331 |        470 |
|       negative | 3.27777777778 |             430 |          8 |
|       positive | 3.71653543307 |           13609 |        102 |

> From this table we can see that the presence of those specific positive words we are watching for is a very good indicator of the success of the restaurant as the average rating of restaurants that have one or more of those words in the tips wrote by users, have an average of 0.5 stars more than the negative words case. So we can see that there is a strong correlation between the rating of a restaurant and what people write about it. We also see that better rated restaurants have so much more reviews than lower rated ones and are open much more often as well.
 

 ### iv. Provide the SQL code you used to create your final dataset:

 ```sql
SELECT CASE WHEN text LIKE '%good%'
              OR text LIKE '%great%'
              OR text LIKE '%excellent%'
              OR text LIKE '%best%' THEN 'positive'
            WHEN text LIKE '%bad%' 
              OR text LIKE '%worst%' 
              OR text LIKE '%terrible%'
              OR text LIKE '%horrible' THEN 'negative'
            END AS 'Classification',
            AVG(stars) AS AvgStars, 
            SUM(review_count) AS TotalNumReviews, 
            SUM(is_open) AS OpenPlaces
FROM(
     SELECT stars, review_count, is_open, tip.text
     FROM business JOIN tip ON business.id=tip.business_id
     )
GROUP BY Classification
```