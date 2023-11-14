
  # queries-quality-and-percentage

  ```mysql
  # Write your MySQL query statement below

select
  query_name,
  round(avg(cast(rating as DECIMAL) / position), 2) as quality,
  round((count(case when rating < 3 then 1 end) / count(*) * 100), 2) as poor_query_percentage
from
  Queries
group by
  query_name;

  ```
  