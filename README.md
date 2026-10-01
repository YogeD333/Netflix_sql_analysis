<img width="672" height="311" alt="image" src="https://github.com/user-attachments/assets/3124c2f2-058b-49dd-babb-4d198814f79a" />

# 🍿 Netflix Content Strategy SQL Analysis

## 🚀 Objective
Executed complex SQL queries on Netflix's catalog database to extract business insights regarding content trends, regional production, and genre popularity.

## 🛠 Technical Execution
* **Database:** PostgreSQL
* **Techniques Used:** Window Functions, Subqueries, Array Unnesting, Date/Time Functions, Conditional Logic (CASE WHEN).

## 💻 Sample Query: Most Common Rating by Content Type
*The following query determines the most frequent content rating for both Movies and TV Shows using a Window Function.*

```sql
SELECT type, rating
FROM (
    SELECT type, rating, COUNT(*),
           RANK() OVER(PARTITION BY type ORDER BY COUNT(*) DESC) as rank
    FROM netflix
    GROUP BY type, rating
) AS ranked_ratings
WHERE rank = 1;
