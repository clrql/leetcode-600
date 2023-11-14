
  # restaurant-growth

  ```mysql
  # Write your MySQL query statement below

with helpDATE as (
    select date_add(visited_on, interval 6 day) as seven_day
    from Customer
), moving_amount as (
    select visited_on, sum(sum(amount)) over window_frame as amount,
    round(avg(sum(amount)) over window_frame, 2) as average_amount
    from Customer
    group by visited_on window window_frame as (
        order by visited_on rows between 6 preceding and current row 
    )
)

select visited_on, amount, average_amount
from moving_amount
where visited_on in (select * from helpDATE)
  ```
  