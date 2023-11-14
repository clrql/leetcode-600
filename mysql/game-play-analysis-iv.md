
  # game-play-analysis-iv

  ```mysql
  # Write your MySQL query statement below

with cte as
(
select *,
  lag(event_date) over(partition by player_id order by event_date) as lag_event_date, 
  min(event_date) over(partition by player_id order by event_date) as min_event_date
from activity
),
cte2 as 
(
  select *, 
  datediff(event_date, min_event_date) as date_difference,
  datediff(event_date, lag_event_date) as date_difference_2
  from cte
),
  total_number_of_players as
(
select count(distinct player_id)
  from cte2
)
select round(count(distinct player_id) / (select * from total_number_of_players),2) as fraction
from cte2
where date_difference  = 1
  ```
  