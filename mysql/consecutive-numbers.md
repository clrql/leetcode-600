
  # consecutive-numbers

  ```mysql
  # Write your MySQL query statement below
select distinct num as ConsecutiveNums
from (
  select num,  row_number() over (order by id) - row_number() over (partition by num order by id) as consecutive_group
  from Logs
) as subquery
group by num, consecutive_group
having count(*) >= 3;
  ```
  