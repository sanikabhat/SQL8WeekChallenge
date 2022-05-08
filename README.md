# SQL8WeekChallenge

#week1
Danny's Diner

1. What is the total amount each customer spent at the restaurant?
select s.customer_id as Customer, 
sum(m.price) as Total_Amount_Spent
from dannys_diner.sales as s join dannys_diner.menu as m
on s.product_id = m.product_id 
group by s.customer_id
order by s.customer_id;

2. How many days has each customer visited the restaurant?
select c.customer, count(c.customer) from
(
  select s.customer_id as Customer,
  count(s.customer_id) as days
  from dannys_diner.sales as s
  group by s.customer_id,s.order_date
 ) as c
 group by c.customer
 order by c.customer;

3. What was the first item from the menu purchased by each customer?
select c.customer, c.product from
(select s.customer_id as customer,
 m.product_name as "product",
rank() over(partition by s.customer_id order by s.order_date) as rnk1
from dannys_diner.sales as s join dannys_diner.menu AS m
on s.product_id = m.product_id
group by s.customer_id, s.order_date, m.product_name) as c
where c.rnk1=1;

4. What is the most purchased item on the menu and how many times was it purchased by all customers?
select m.product_name, c.nooftimes as purchased
from
(
  select s.product_id, 
  count(s.product_id) as nooftimes, 
  rank() over(order by count(s.product_id) desc) as rnk1
  from dannys_diner.sales s
  group by s.product_id
  order by count(s.product_id) desc
  ) as c join dannys_diner.menu as m
on c.product_id = m.product_id
where c.rnk1=1;

5. Which item was the most popular for each customer?

select c.customer, m.product_name from 
(
  select s.customer_id as customer, s.product_id as product,
  count(s.product_id),
  rank() over(partition by s.customer_id order by count(s.product_id) desc) as rnk1 
  from dannys_diner.sales as s 
  group by s.customer_id,s.product_id
  ) as c join dannys_diner.menu as m
  on c.product = m.product_id
  where rnk1=1
  order by c.customer;
  
6. Which item was purchased first by the customer after they became a member?
select customer_id, order_date, product_name from(  
select s.customer_id,
s.order_date,
m.product_name,
rank() over(partition by s.customer_id order by s.order_date) as rnk1
from dannys_diner.sales as s
join
dannys_diner.members as mem
on s.customer_id = mem.customer_id
join dannys_diner.menu as m
on s.product_id= m.product_id 
where s.order_date >= mem.join_date ) as c
where rnk1=1;

7. Which item was purchased just before the customer became a member?
select customer_id, order_date, product_name from(
select s.customer_id,
s.order_date,
m.product_name,
rank() over(partition by s.customer_id order by s.order_date desc) as rnk1
from dannys_diner.sales as s
join
dannys_diner.members as mem
on s.customer_id = mem.customer_id
join dannys_diner.menu as m
on s.product_id= m.product_id 
where s.order_date < mem.join_date) as c where rnk1=1;

8. What is the total items and amount spent for each member before they became a member?
select s.customer_id as Customer,
count(distinct s.product_id) as TotalItems, sum(m.price) as AmountSpent
from dannys_diner.sales as s
join dannys_diner.members as mem
on s.customer_id = mem.customer_id
join dannys_diner.menu as m
on s.product_id = m.product_id
where s.order_date < mem.join_date
group by s.customer_id;

9.  If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
select customer_id, sum(points)
from(
  select s.customer_id,m.product_name,
  case 
  when m.product_name = 'sushi' then sum(m.price*20)
  else sum(m.price*10)
  end as points
  from dannys_diner.sales as s
  join dannys_diner.menu as m
  on s.product_id = m.product_id
  group by  s.customer_id,m.product_name
  ) as c
  group by customer_id
  order by customer_id;
  
10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?
select customer_id, sum(points) as total_points
from
(
select s.customer_id, m.product_name, s.order_date, m.join_date,
case
	when m.product_name = 'sushi' and s.order_date < m.join_date then sum(m.price*20)
	when m.product_name = 'ramen' and s.order_date < m.join_date then sum(m.price*10)
	when m.product_name = 'curry' and s.order_date < m.join_date then sum(m.price*10)
	when s.order_date >= m.join_date and s.order_date < '2021-01-31' then sum(m.price*20)
end as points
from dannys_diner.sales as s
join dannys_diner.menu as m
on s.product_id = m.product_id
join dannys_diner.members as m
on s.customer_id = m.customer_id
where s.order_date < '2021-01-31'
group by s.customer_id,m.product_name,s.order_date,m.join_date) as c
GROUP BY customer_id;
