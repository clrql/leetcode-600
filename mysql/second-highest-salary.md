
  # second-highest-salary

  ```mysql
  # Write your MySQL query statement below

SELECT
    MAX(salary) AS SecondHighestSalary
FROM
    Employee
WHERE
    salary < (SELECT MAX(salary) FROM Employee)
  ```
  