
  # friend-requests-ii-who-has-the-most-friends

  ```mysql
  # Write your MySQL query statement below

select id, count(*) as num
from (
  select requester_id as id
  from RequestAccepted
  union all
  select accepter_id as id
  from RequestAccepted
) as t
group by id
having count(*) = (
  select count(*)
  from (
    select requester_id as id
    from RequestAccepted
    union all
    select accepter_id as id
    from RequestAccepted
  ) as u
  group by id
  order by count(*) desc
  limit 1
);

  ```
  