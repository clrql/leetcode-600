
  # the-number-of-employees-which-report-to-each-employee

  ```mysql
  # Write your MySQL query statement below

select e.employee_id, e.name, count(r.employee_id) as reports_count, round(avg(r.age)) as average_age from Employees e left join Employees r on e.employee_id = r.reports_to
where e.employee_id in (
    select distinct reports_to from Employees
)
group by e.employee_id, e.name
order by e.employee_id
  ```
  