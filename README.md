# SQL8WeekChallenge

(I will upload all the sql files for every week)

## **Danny Ma's Week 1 (Danny's Diner) Challenge**

![image](https://user-images.githubusercontent.com/26146479/167309111-50470b0d-b43a-4b53-aece-096608950e8b.png)

1. What is the total amount each customer spent at the restaurant?
2. How many days has each customer visited the restaurant?
3. What was the first item from the menu purchased by each customer?
4. What is the most purchased item on the menu and how many times was it purchased by all customers?
5. Which item was the most popular for each customer?
6. Which item was purchased first by the customer after they became a member?  
7. Which item was purchased just before the customer became a member?
8. What is the total items and amount spent for each member before they became a member?
9.  If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?

## ** Week 2 (Pizza Runner) Challenge**

![image](https://user-images.githubusercontent.com/26146479/167879674-116e3a28-44cb-4c5a-aedc-f6e4fba0d09f.png)


Areas of Focus:
Danny decided to Uberize his Pizza business. So, he launches "Pizza Runner" (runners recruited to deliver pizza from his home) and is developping an app

Questions to be answered are categorised into different topic:

Pizza Metrics
Runner and Customer Experience
Ingredient Optimisation
Pricing and Ratings
Bonus Challenge

ER Diagram below

![image](https://user-images.githubusercontent.com/26146479/167879862-a5234d3d-a28e-4ef8-a2bb-7220d87e8298.png)

A. Pizza Metrics
    1. How many pizzas were ordered?
    2. How many unique customer orders were made?
    3. How many successful orders were delivered by each runner?
    4. How many of each type of pizza was delivered?
    5. How many Vegetarian and Meatlovers were ordered by each customer?
    6. What was the maximum number of pizzas delivered in a single order?
    7. For each customer, how many delivered pizzas had at least 1 change and how many had no changes?
    8. How many pizzas were delivered that had both exclusions and extras?
    9. What was the total volume of pizzas ordered for each hour of the day?
    10. What was the volume of orders for each day of the week?

B. Runner and Customer Experience
    1. How many runners signed up for each 1 week period? (i.e. week starts 2021-01-01)
    2. What was the average time in minutes it took for each runner to arrive at the Pizza Runner HQ to pickup the order?
    3. Is there any relationship between the number of pizzas and how long the order takes to prepare?
    4. What was the average distance travelled for each customer?
    5. What was the difference between the longest and shortest delivery times for all orders?
    6. What was the average speed for each runner for each delivery and do you notice any trend for these values?
    7. What is the successful delivery percentage for each runner?
    
C. Ingredient Optimisation
    1. What are the standard ingredients for each pizza?
    2. What was the most commonly added extra?
    3. What was the most common exclusion?
    4. Generate an order item for each record in the customers_orders table in the format of one of the following:
        a. Meat Lovers
        b. Meat Lovers - Exclude Beef
        c. Meat Lovers - Extra Bacon
        d. Meat Lovers - Exclude Cheese, Bacon - Extra Mushroom, Peppers
    5. Generate an alphabetically ordered comma separated ingredient list for each pizza order from the customer_orders table and add a 2x in front of any relevant ingredients
    For example: "Meat Lovers: 2xBacon, Beef, ... , Salami"
    6. What is the total quantity of each ingredient used in all delivered pizzas sorted by most frequent first?
    
D. Pricing and Ratings
    1. If a Meat Lovers pizza costs $12 and Vegetarian costs $10 and there were no charges for changes -
        how much money has Pizza Runner made so far if there are no delivery fees?
    2. What if there was an additional $1 charge for any pizza extras?
        Add cheese is $1 extra
    3. The Pizza Runner team now wants to add an additional ratings system that allows customers to rate their runner, how would you design an additional table for this new dataset - generate a schema for this new table and insert your own data for ratings for each successful customer order between 1 to 5.
    4. Using your newly generated table - can you join all of the information together to form a table which has the following information for successful deliveries?
        a. customer_id
        b. order_id
        c. runner_id
        d. rating
        e. order_time
        f. pickup_time
        g. Time between order and pickup
        h. Delivery duration
        i. Average speed
        j. Total number of pizzas
    5. If a Meat Lovers pizza was $12 and Vegetarian $10 fixed prices with no cost for extras and each runner is paid $0.30 per kilometre traveled - how much money does Pizza Runner have left over after these deliveries?

E. Bonus Questions
1. If Danny wants to expand his range of pizzas - how would this impact the existing data design? Write an INSERT statement to demonstrate what would happen if a new Supreme pizza with all the toppings was added to the Pizza Runner menu?
