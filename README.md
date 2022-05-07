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

5. What is the most purchased item on the menu and how many times was it purchased by all customers?
6. Which item was the most popular for each customer?
7. Which item was purchased first by the customer after they became a member?
8. Which item was purchased just before the customer became a member?
9. What is the total items and amount spent for each member before they became a member?
10.  If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
11. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?
