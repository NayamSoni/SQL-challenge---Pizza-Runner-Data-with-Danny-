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

Solution- A total of 14 pizzas were ordered. 

-- 2. How many unique customer orders were made?

select count(distinct order_id) unique_orders
from pizza_runner.customer_orders ;

Solution- There were a total of 10 unique orders. 

-- 3. How many successful orders were delivered by each runner?

select runner_id,count(order_id) as successful_orders
from pizza_runner.runner_orders 
where distance <> 'null'
       group by runner_id
       order by runner_id;

Solution - ![image](https://github.com/NayamSoni/SQL-challenge---Pizza-Runner-Data-with-Danny-/assets/98815102/e95f4727-bc62-488e-8fd6-fb0d39600b3d)

