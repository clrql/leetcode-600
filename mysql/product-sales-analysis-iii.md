
  # product-sales-analysis-iii

  ```mysql
  # Write your MySQL query statement below

select s.product_id, s.year as first_year, s.quantity, s.price
from Sales s
inner join (
    select product_id, min(year) as min_year
    from Sales
    group by product_id
) t on s.product_id = t.product_id and s.year = t.min_year

  ```
  