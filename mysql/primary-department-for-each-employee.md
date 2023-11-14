
  # primary-department-for-each-employee

  ```mysql
  # Write your MySQL query statement below

select employee_id, department_id
from Employee
where primary_flag = 'Y'
union
select employee_id, department_id
from Employee
where employee_id NOT IN (
    select employee_id
    from Employee
    where primary_flag = 'Y'
)

  ```
  