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

6. Which item was the most popular for each customer?

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
  
8. Which item was purchased first by the customer after they became a member?
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

10. Which item was purchased just before the customer became a member?
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

12. What is the total items and amount spent for each member before they became a member?
13.  If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
14. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?
