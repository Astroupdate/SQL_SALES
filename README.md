select * from sales;

create table sales_1
like sales;

select * from sales_1;

insert sales_1
select * 
from sales;

select * from sales_1;

select *,
row_number () 
over 
(partition by `date`, `day`, `month`, `year`, customer_age, age_group, customer_gender, country, state, product_category, sub_category, product, order_quantity, unit_cost, unit_price,profit, cost, revenue )
as row_num
from sales_1;


with duplicate_cte as 
(select *,
row_number () 
over 
(partition by `date`, `day`, `month`, `year`, customer_age, age_group, customer_gender, country, state, product_category, sub_category, product, order_quantity, unit_cost, unit_price,profit, cost, revenue )
as row_num
from sales_1
)
select * from duplicate_cte
where row_num > 1;


select *
from sales_1
where `day` = 2;


CREATE TABLE `sales_2` (
  `Date` text,
  `Day` int DEFAULT NULL,
  `Month` text,
  `Year` int DEFAULT NULL,
  `Customer_Age` int DEFAULT NULL,
  `Age_Group` text,
  `Customer_Gender` text,
  `Country` text,
  `State` text,
  `Product_Category` text,
  `Sub_Category` text,
  `Product` text,
  `Order_Quantity` int DEFAULT NULL,
  `Unit_Cost` int DEFAULT NULL,
  `Unit_Price` int DEFAULT NULL,
  `Profit` int DEFAULT NULL,
  `Cost` int DEFAULT NULL,
  `Revenue` int DEFAULT NULL,
  `row_num` int 
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


select *
from sales_2;

insert into sales_2
select *,
row_number () 
over 
(partition by `date`, `day`, `month`, `year`, customer_age, age_group, customer_gender, country, state, product_category, sub_category, product, order_quantity, unit_cost, unit_price,profit, cost, revenue )
as row_num
from sales_1;

select *
from sales_2
where row_num > 1;

delete 
from sales_2
where row_num > 1;

select *
from sales_2;


select distinct(country)
from sales_2;

select country, trim(country)
from sales_2;

update sales_2
set country = trim(country);

select * 
from sales_2;

select distinct(sub_category)
from sales_2
order by 1;

select distinct(product)
from sales_2
where product like 'Road-650 %'
order by 1;

select distinct country, trim(trailing '.' from country)
from sales_2
order by 1;

select *
from sales_2
where country = 'Germany'
order by 1;

select `date`
from sales_2;


alter table sales_2		
modify column `date` date;

select *
from sales_2;

select *
from sales_2
where order_quantity is null
or Order_Quantity = '';

-- the dateset does not have any null or blanks ....
select distinct age_group
from sales_2
order by 1;

select *
from sales_2
where age_group like 'Adults%';
update sales_2
set age_group = 'Adults'
where age_group like 'Adults%'; 

select *
from sales_2
where age_group like 'Seniors%';
update sales_2
set age_group = 'Seniors'
where age_group like 'Seniors%';

select *
from sales_2
where age_group like 'Young Adults%';
update sales_2
set age_group = 'Young Adults'
where age_group like 'Young Adults%';

select *
from sales_2
where age_group like 'Youth%';
update sales_2
set age_group = 'Youth'
where age_group like 'Youth%';

select distinct age_group
from sales_2
order by 1;

select *
from sales_2;

alter table sales_2
drop column row_num;

select *
from sales_2;
