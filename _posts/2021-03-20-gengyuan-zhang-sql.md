---
layout: post
title: "Gengyuan's Notes about SQL knowledge"
date: 2021-03-20
---

Some useful notes are as follows:

1) How to "comment in MySQL workbench" can be found [here](https://www.mysqltutorial.org/mysql-comment/)

2）My exercise for today:

<code>
select * 
from thequantedge.users; -- Select all columns from the table named by 'users'

select id 
from users; -- select the 'id' column from the table named by 'users'

select id, first_name, last_name 
from users; -- select multiple columns from the table named by 'users' 

select * 
from memberships; -- select another table 

select initial_payment 
from memberships; -- all the price 

select distinct initial_payment 
from memberships; -- distinct prices from table named by 'memberships'

SELECT first_name 
from users 
LIMIT 5; -- select the top 5 rows of the selected columns

select first_name 
from users 
limit 5 
offset 5; -- select 5 rows right after the first five rows 

select initial_payment 
from memberships 
order by initial_payment; -- price sorted by ascending order, it is default

select initial_payment 
from memberships 
order by -initial_payment; -- price sorted by descending order

select initial_payment 
from memberships 
order by initial_payment desc; -- alternative way for descending order

select initial_payment, billing_amount, cycle_period 
from memberships
order by cycle_period, initial_payment, billing_amount; -- sorted by multiple columns

select initial_payment, billing_amount, cycle_period 
from memberships
order by 3, 2; -- sorted by multiple columns by column indices

select initial_payment, billing_amount, cycle_period 
from memberships
order by cycle_period, initial_payment desc, billing_amount; -- multiple columns combined sorted

select name, billing_amount 
from memberships
where billing_amount = 49.99; -- selection filter when equal to certain values

select name, billing_amount 
from memberships
where billing_amount >= 9.99
order by billing_amount; -- selection filter together with sorting

select name, billing_amount 
from memberships
where billing_amount between 5 and 99.99
order by billing_amount; -- selection filter together with sorting

select name, billing_amount 
from memberships
where expiration_date IS NULL; -- selection filter when null

select name, description 
from memberships
where billing_amount >= 29.99 and cycle_period = 'Month'; -- AND OR operator for multiple filter, AND prior to OR, using () for priorities

select name, initial_payment 
from memberships
where cycle_period in ('Month','Week','Year')
order by initial_payment; -- selection filter IN

select name, initial_payment, billing_amount 
from memberships
where NOT billing_amount = 0
order by initial_payment; -- filter selection NOT

select name, initial_payment 
from memberships
where name like '%betting%'; -- selection filter LIKE and % for multiple (including zero) letters

select id, first_name, last_name, email 
from users
where email LIKE '____@%'; -- selection filter, LIKE and every _ for every single letter

SELECT trim(first_name) + trim(last_name)  
from users; -- SQL concatenate, not for MySQL 

select * from users;
SELECT first_name, last_name  from users;
select Concat(first_name, ' ', last_name) as full_name from users; -- concatenate of MySQL and MariaDB
 
select * from memberships;
select id, name, initial_payment, initial_payment * 12 as annual_payment 
from memberships; -- adding a new column by simple calculation
 
select now(); -- the current time()

select first_name, last_name, upper(last_name) as last_name_upcase, lower(first_name) as first_name_lcase
from users; 

select first_name 
from users
where first_name = 'ddavid';
select first_name 
from users
where soundex(first_name) = soundex('ddavid'); -- similar pronunciation filter

select * 
from membership_orders;
select id, created_at 
from membership_orders
where year(created_at) = 2018;  -- date selection by year

-- some numerical function: abs(), cos(), exp(), pi(), sin(), sqrt(), tan()

-- aggregate function:  avg(), count(), max(), min(), sum()

select avg(initial_payment) as avg_initial 
from memberships
where billing_amount <> 0;  -- function avg() 

select count(*) as num_users
from users;  -- function count() 

select * 
from users;
select count(deleted_at) as num_users_deleted 
from users; -- conditional count()

select * 
from users;
select count(last_name) as num_users_w_ln 
from users
where length(last_name) != 0; -- conditional count() 

select max(initial_payment) as max_price
from memberships; -- function max() 

select min(initial_payment) as min_price
from memberships; -- function min()

select sum(initial_payment*id) as sum_price
from memberships
where expiration_period = 'month'; -- function sum() with inner multiplication

select avg(distinct initial_payment) as avg_initial
from memberships
where billing_amount <> 0 and expiration_period = 'month';  -- function avg() 

select count(*) as num_items,
		min(initial_payment) as price_min,
        max(initial_payment) as price_max,
        avg(initial_payment) as price_avg
from memberships
where expiration_period = 'month';

select count(*) as num_items
from memberships
where expiration_period = 'month';

select * from users;
select * from users
where is_active = 1;
select count(*) as num_active
from users
where is_active = 1;
select is_active, count(*) as num_users
from users
group by is_active; -- an example of GROUP BY 

select * from membership_users;
select initial_payment, count(*) as num_plan
from membership_users
where cycle_period in ('Month', 'Year')
group by initial_payment
order by initial_payment desc; -- a more complicated example of GROUP BY 

select * from membership_orders;
select membership_user_id, count(*) as orders
from membership_orders
where year(created_at) in (2018, 2019)
group by membership_user_id
having count(*) >= 10
order by orders;  -- an example of HAVING and COUNT. Main difference: HAVING is after group, WHERE is before group

select * from membership_orders
where total > 0;

select membership_user_id from membership_orders
where total > 0
limit 5;  -- main query 1 

select * from users;
select username
from users
where id in (5,17,48,49); -- main query 2

select username
from users
where id in (select distinct membership_user_id
			from membership_orders
			where total > 100)
limit 5; -- combined subquery

select email
from users
where username in (select username
					from users
					where id in (select distinct membership_user_id
									from membership_orders
									where total > 100))
limit 5; -- another subquery example

select * from membership_orders;
select count(*) as num_orders
from membership_orders
where membership_user_id = '4'; -- conditional counts

select username, (select count(*) 
					from membership_orders
                    where membership_orders.membership_user_id = users.id) as num_orders
from users
order by num_orders desc
limit 10;  -- conditional counts using subquery 

select * from membership_users;
select distinct first_name, username, email, initial_payment
from users, membership_users
where users.id = membership_users.user_id; -- an example of equi-join

select distinct first_name, username, email, initial_payment
from users inner join membership_users
on users.id = membership_users.user_id; -- an example of innter join 

select distinct username
from users, membership_orders
where users.id = membership_orders.membership_user_id and membership_orders.total > 100
limit 5; --  another example of join to replace the sub-query

select concat(first_name, ' ', last_name) as full_name
from users; -- an example of new naming

select distinct username
from users as U, membership_orders as M
where U.id = M.membership_user_id and M.total > 100
limit 5; --  another example of new naming

select distinct c1.id, c1.username, c1.email
from users as c1, membership_orders as c2
where c1.id = c2.membership_user_id
and c2.total = 29.99
limit 5;

select distinct c1.*, c1.username, c1.email
from users as c1, membership_orders as c2
where c1.id = c2.membership_user_id
and c2.total = 29.99
limit 5; -- another example of inner join

select first_name, username, email, initial_payment
from users left outer join membership_users
on users.id = membership_users.user_id;
select distinct first_name, username, email, initial_payment
from users right outer join membership_users
on users.id = membership_users.user_id
limit 10;-- an example of outer join LEFT OUTER JOIN and RIGHT OUTER JOIN

select * from membership_orders;
select users.id,
		count(membership_orders.total) as num
from users inner join membership_orders
on users.id = membership_orders.membership_user_id
group by users.id
order by num desc;  
select users.id,
		count(membership_orders.total) as num
from users left outer join membership_orders
on users.id = membership_orders.membership_user_id
group by users.id
order by num desc;  -- example of inner and outer join 

-- next we will combine sub1 and sub2 into one union
select * from users;
-- sub1
select first_name, last_name, username
from users
where first_name = 'David' and last_name like 't%';
-- sub2 
select first_name, last_name, username
from users
where is_active = 1 and first_name = 'David' and last_name = 'etkin';
-- combined union
select first_name, last_name, username
from users
where first_name = 'David' and last_name like 't%'
union
select first_name, last_name, username
from users
where is_active = 1 and first_name = 'David' and last_name = 'etkin'
order by username; -- usage of UNION (default deleting the duplicated row), UNION ALL(keep all rows)

</code>










