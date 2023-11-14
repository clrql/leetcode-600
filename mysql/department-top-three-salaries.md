
  # department-top-three-salaries

  ```mysql
  # Write your MySQL query statement below

select d.name as Department, e.name as Employee, e.salary as Salary
from Employee e
join Department d on e.departmentId = d.id
where (
    select count(distinct salary)
    from Employee
    where departmentId = e.departmentId and salary > e.salary
) < 3
order by d.name, e.salary desc

  ```
  