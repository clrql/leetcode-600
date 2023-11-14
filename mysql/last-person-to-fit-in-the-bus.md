
  # last-person-to-fit-in-the-bus

  ```mysql
  # Write your MySQL query statement below

with cte as (
  select 
    person_id, 
    person_name, 
    sum(weight) over(order by turn) as total_weight 
  from queue
)
select person_name 
from cte
where total_weight <= 1000
order by total_weight desc
limit 1;
  ```
  