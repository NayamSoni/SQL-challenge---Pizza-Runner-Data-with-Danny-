# SQL-challenge---Pizza-Runner-Data-with-Danny-
As we know, Pizza is the Future! 🍕 So let's work on this case study. 

-- Part A of Pizza Runner i.e. Pizza Metrics --

👉 Introduction:

Certainly! Danny, the founder of Pizza Runner, has launched a new venture combining "80s Retro Styling and Pizza."
To expand his Pizza Empire, he came up with the idea of Uberizing it, and thus Pizza Runner was born.

He recruited "runners" to deliver fresh pizza from his headquarters (his house) and developed a mobile app to accept orders from customers.

To optimize Pizza Runner's operations, Danny understands the importance of data collection. I will help clean the data and perform necessary calculations for better 
directing the runners and improving the business's efficiency. All datasets are within the pizza_runner database schema. Let's get started! 🍕

Dataset Link - https://8weeksqlchallenge.com/case-study-2/

Online Platform - https://www.db-fiddle.com/f/7VcQKQwsS3CTkGRFG7vu98/65

Case Study Questions: 

-- 1. How many pizzas were ordered?

select count(order_id) pizzas_ordered
from pizza_runner.customer_orders ;

Output - A total of 14 pizzas were ordered. 

![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/85ba11c2-b3b4-4d6e-86f7-7312783dcd8b)


-- 2. How many unique customer orders were made?

select count(distinct order_id) unique_orders
from pizza_runner.customer_orders ;

Output - There were a total of 10 unique orders. 

![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/79163fa9-940c-4970-8dcc-b33491a89474)


-- 3. How many successful orders were delivered by each runner?

select runner_id,count(order_id) as successful_orders
from pizza_runner.runner_orders 
where distance <> 'null'
       group by runner_id
       order by runner_id;

Output  - ![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/e95f4727-bc62-488e-8fd6-fb0d39600b3d)

-- 4. How many of each type of pizza was delivered?   

select pizza_name, count(customer_orders.order_id) as pizza_dilvered
from pizza_runner.customer_orders join pizza_runner.runner_orders 
ON customer_orders.order_id = runner_orders.order_id
join pizza_runner.pizza_names
on customer_orders.pizza_id = pizza_names.pizza_id
where distance <> 'null'
group by pizza_name
order by pizza_dilvered desc;


Output - ![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/17a08ef7-eba6-46ac-9469-5b53fd046e23)

-- 5. How many Vegetarian and Meatlovers were ordered by each customer?

select customer_id, pizza_name,count(customer_orders.order_id) as pizza_dilvered
from pizza_runner.customer_orders join pizza_runner.runner_orders 
ON customer_orders.order_id = runner_orders.order_id
join pizza_runner.pizza_names
on customer_orders.pizza_id = pizza_names.pizza_id
group by customer_id, pizza_name
order by customer_id;

Output - ![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/66efd9ad-b727-48a8-b449-123b967c802f)

-- 6. What was the maximum number of pizzas delivered in a single order?

 WITH count_of_the_customers AS
 (
 SELECT customer_orders.order_id,
 COUNT(customer_orders.order_id) as count_id
 from pizza_runner.customer_orders JOIN pizza_runner.runner_orders
 ON customer_orders.order_id = runner_orders.order_id
 WHERE distance <> 'null'
 GROUP BY 1)
    
 Select max(count_id) as maximum_single_orders
 from count_of_the_customers;

Output - ![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/8518c3ed-4866-407a-86c9-40854e37ad03)

-- 7. For each customer, how many delivered pizzas had at least 1 change and how many had no changes?

select customer_id,
        sum(case when exclusions = '' or extras = '' or exclusions = 'null' or extras = 'null' then 0 else 1 end) as atleast_1_change, 
         sum(case when exclusions <> '' or extras <> '' or exclusions <> 'null' or extras <> 'null' then 1 else 0    end) as no_change
 from pizza_runner.customer_orders join pizza_runner.runner_orders
 on customer_orders.order_id = runner_orders.order_id
 where distance <> 'null'
 group by customer_id
 order by customer_id;

Output - ![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/7918e944-781c-4f21-9501-127ccbcc2a2f)

 -- 8. How many pizzas were delivered that had both exclusions and extras?
 
 select 
            sum(case when exclusions <> '' and extras <> '' and exclusions <> 'null' and extras <> 'null'
            then 1
            else 0 
            end) as Pizzas_delivered
 from pizza_runner.customer_orders join pizza_runner.runner_orders
 on customer_orders.order_id = runner_orders.order_id
 where distance <> 'null' ;

 Output- ![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/34a2f5f1-ee33-41fa-af3d-60f6104aa336)

 
 -- 9. What was the total volume of pizzas ordered for each hour of the day?
select date_part('hour',order_time) as each_hour , count(order_id) as toal_pizzas_ordered 
from pizza_runner.customer_orders
group by 1 
order by 1;

 Output- ![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/cef61c6f-2423-4f41-960a-4f3cb2ffde81)

 
-- 10. What was the volume of orders for each day of the week?

select to_char(order_time,'day') as day_of_the_week,
count(order_id) as volume_of_orders
from pizza_runner.customer_orders
group by 1
order by 1;

 Output- ![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/0323134d-ffb3-4426-8a48-449a8884c526)

