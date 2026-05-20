# HOW TO DO LEFT JOIN
- Ques
![alt text](sql-images/image.png)
- SOl
![alt text](sql-images/image-1.png)
Here if your field name is different then write as a.address as add like this
# alter changes column strctre and can add column in table

# you can add list by using IN OR NOT IN
# HOW TO DO RECURSION
![alt text](sql-images/image-2.png)
QUESTIONS-
![alt text](sql-images/image-3.png)
# ANS-
![alt text](sql-images/image-4.png)
![alt text](sql-images/image-5.png)

# FILTER
- like '_%a' have minimum 1 character ..then ending with a
- regex WHERE first_name REGEXP '^[ABCD]'-starts with ABCD
-regex ending with '[ABCD]$' here ending with A OR B OR C OR D
-2nd charater(a,e,i,o,u)-> '^.[aeiou]'
- [abcd]* - 0 or more times
-[abcd]+ - 1 or more times
-[abcd]? - 0 or 1 time
-email '^[a-z0-9._]+@[a-z0-9_]+\.[a-z]{2,}$'minimum 2 
- inside []you have to use hyphen you have to use [\\-]
-

# HOW TO USE WITH CLAUSE
![alt text](sql-images/image-6.png)
We can use multiple references to cte  with the use of WITH clause
# when you write with average_salary   

![alt text](sql-images/image-7.png)

# WINDOW FUNCTION

<WINDOW FUNCTION>OVER (PARTITION BY department ORDER BY Salary Desc)
![alt text](sql-images/image-8.png)
![alt text](sql-images/image-9.png)
![alt text](sql-images/image-10.png)

-ROW NO,RANK,DENSE
- let say there are ties then row no will give diff to each
- rank will give same to ties then continue with not continuation
- dense will give same to ties but start with continuation

-LEAD AND LAG
-SELECT *,LAG(Salary,3) OVER (ORDER BY SALARY DESC)as next_sal
FROM EMPLOYESS(3- the lead you want to take)


# SUBQUERIES
 1) SCALAR SUBQUERIES
    used for 1 row and 1 column
    ![alt text](sql-images/image-11.png) always return 1 column with 1 row
      
 2) MULTIPLE ROW SUBQUEY
  return both multiple rows and multiple column
  or 1 multiple row and one column
  ![alt text](sql-images/image-13.png)

  # when you have to find a department where atleast there is one employee
  ![alt text](sql-images/image-14.png)

   
 ![alt text](sql-images/image-12.png)
 3) CORRELATED SUBQUERY
![alt text](sql-images/image-15.png)
![alt text](sql-images/image-16.png)

# VIEW
when you want to give access (restricted access)to customers
![ ](sql-images/image-17.png)c
![alt text](sql-images/image-18.png)

```
create view customers_v as
select customer_id,customer_fname,,customer_fname,customver_city;

select * from customers_v limit 10;  


```
- now you wanted to give permission to the user
- CREATE USER 'analyticsx'@'localhost  identified by 'analytics123'
-GRANT SELECT ON retail_db.customer_v TO 'analyticsx'@'localhost';
![alt text](image-39.png)
if you want to revoke
- REVOKE SELECT ON retail-db.customers_v fromr 'analuticss'@'localhost'
- similarily we can give SELECT,DROP whatever they want
  
 # constraint
 for accuracy
  -ALTER TABLE ORDERS 
  ADD CHECK (order_status in ('CLOSED',"PENDING','COMPLETE'))
 - for dropping constraint
  -ALTER TABLE orders DROP CHECK orders_chk_1
  -?? from where orders_chk_1 will come see in show create table orders
  - can directly use when creating table
  - order_status varchar(20) CHECK (order_status in());

# FOREIGN KEY
-when adding foreign key add also ON DELTE CASCADE
-ON UPDATE CASCADE_ AUTOMATICaLLy changes id of children if id of parent id changed
- we can also use self referencing
-
