
  # delete-duplicate-emails

  ```mysql
  # Please write a DELETE statement and DO NOT write a SELECT statement.
# Write your MySQL query statement below

delete from Person
where id NOT IN (
    select id
    from (
        select min(id) AS id
        from Person
        group by email
    ) as t
);
  ```
  