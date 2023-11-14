
  # movie-rating

  ```oraclesql
  /* Write your PL/SQL query statement below */

select name results
from (
select u.user_id, u.name, count(distinct movie_id) mv_cnt
from MovieRating m
inner join Users u
on u.user_id = m.user_id
group by u.user_id, u.name
order by mv_cnt desc, u.name
    )
where rowNum = 1

union all

select title results
from(
    select m2.movie_id, m2.title, avg(m1.rating) avg_rt
    from MovieRating m1
    inner join Movies m2
    on m1.movie_id = m2.movie_id
    where to_char(m1.created_at, 'YYYY-MM') = '2020-02'
    group by m2.movie_id, m2.title
    order by avg_rt desc, m2.title
    )
where rowNum = 1
  ```
  