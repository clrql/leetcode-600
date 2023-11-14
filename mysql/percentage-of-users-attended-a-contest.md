
  # percentage-of-users-attended-a-contest

  ```mysql
  # Write your MySQL query statement below

select r.contest_id, round(count(r.user_id)*100.0 / u.total_users, 2) as percentage
from Register r
inner join Users u on r.user_id = u.user_id
cross join (
    select count(*) as total_users from Users
) u
group by r.contest_id
order by percentage desc, r.contest_id asc;
  ```
  