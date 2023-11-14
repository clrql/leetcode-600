
  # exchange-seats

  ```mysql
  SELECT  
  IF(id % 2 = 0 , id-1 ,IF(id != ( SELECT MAX(id) FROM SEAT ),id+1,id)) AS id,
  student
FROM SEAT
ORDER BY id;
  ```
  