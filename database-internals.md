# Chapter 1

## Difference Between OLTP and OLAP

### OLTP (Online Transaction Processing)

- Handles day-to-day operations of an application
- Works on small numbers of rows at a time
- High concurrency
- Short-lived transactions
- Transactional workloads

Examples:
- think of small transaction
```
 BEGIN
 SELECT account_balance
 FROM USERS 
 where user_id=101
 FOR UPDATE;

 # deduct 20 dollar rupees

 UPDATE Users 
 SET account_balance=account_balance+10
 where user_id=101

 #creating official record
 INSERT INTO ORDERS(user_id, order_date,amount)
 VALUES(9876, 1045, CURRENT_TIMESTAMP, 20.00);

 COMMIT; 

```
actual business logic
```
# This is Python backend code running on your server

def process_purchase(user_id, book_price):
    
    # 1. Start the transaction
    db.execute("BEGIN TRANSACTION")

    # 2. SELECT the current balance and lock the row
    # We MUST lock it now, otherwise someone else could change the balance 
    # while our Python code is doing the math in step 3.
    result = db.execute("SELECT account_balance FROM Users WHERE user_id = ? FOR UPDATE", user_id)
    current_balance = result['account_balance']

    # 3. THIS IS THE BUSINESS LOGIC I LEFT OUT
    if current_balance < book_price:
        # She doesn't have enough money! 
        db.execute("ROLLBACK") # Unlock the row
        return "Error: Insufficient Funds"
        
    # 4. If she has enough money, NOW we issue the UPDATE
    db.execute("UPDATE Users SET account_balance = account_balance - ? WHERE user_id = ?", book_price, user_id)
    
    # 5. Save changes and unlock the row
    db.execute("COMMIT")
    return "Success: Book purchased!"


```

```
# more production way
UPDATE Users 
SET account_balance = account_balance - 20 
WHERE user_id = 9876 
  AND account_balance >= 20;


```
- In this code you can see why are we first selecting the index and then updating it 
- 1st reason-business logic first check whether she have that 20 dollar in her account or not
- if the balance is less than 20 then say insufficient amount
- 2nd reason preventing concurrency control by using locks
-

---

### OLAP (Online Analytical Processing)

- Handles analytical/business intelligence queries
- Read-heavy workloads
- Scans millions of rows
- Performs aggregations and reporting

Examples:
```
SELECT 
    AVG(u.age) AS average_customer_age,
    COUNT(o.order_id) AS total_books_sold
FROM 
    Orders o
JOIN 
    Users u ON o.user_id = u.user_id
JOIN 
    Products p ON o.product_id = p.product_id
WHERE 
    p.category = 'Science Fiction'
    AND o.order_date BETWEEN '2023-11-24' AND '2023-11-27';

```

