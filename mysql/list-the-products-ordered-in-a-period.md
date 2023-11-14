
  # list-the-products-ordered-in-a-period

  ```mysql
  # Write your MySQL query statement below

select p.product_name, SUM(o.unit) as unit
from Products p
join Orders o on p.product_id = o.product_id
where o.order_date >= '2020-02-01' and o.order_date < '2020-03-01'
group by p.product_name
having unit >= 100;

  ```
  