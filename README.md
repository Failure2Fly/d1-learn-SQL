
1. **Question** How many users are there?
   1. **Terminal** - sqlite> select count (id) from users;
   1. **Answer** - count (id) 50

2. **Question** - What are the 5 most expensive items?
   2. **Terminal** - select title, price from items order by price desc limit 5;
   2. **Answer** - Small Cotton Gloves|9984
                   Small Wooden Computer|9859
                   Awesome Granite Pants|9790
                   Sleek Wooden Hat|9390
                   Ergonomic Steel Car|9341

3. **Question** - What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
   3. **Terminal** - select title, category, price from items where category like '%books%' order by price asc limit 1;
   3. **Answer** - Ergonomic Granite Chair|Books|1496

4. **Question** - Who lives at "6439 Zetta Hills, Willmouth, WY"?
   4. **Terminal** - select * from addresses where street like '%6439 Zetta Hills%';
   4. **Answer** - 43|40|6439 Zetta Hills|Willmouth|WY|15029

4. **Question** - Do they have another address?
   4. **Terminal** - select * from addresses join users on user_id = users.id where user_id='40';
   4. **Answer** - 43|40|6439 Zetta Hills|Willmouth|WY|15029|40|Corrine|Little rubie_kovacek@grimes.net
                   44|40|54369 Wolff Forges|Lake Bryon|CA|31587|40|Corrine|Little|rubie_kovacek@grimes.net

5. **Question** - Correct Virginie Mitchell's address to "New York, NY, 10108".?
   5. **Terminal** - *Step1* - select * from users where first_name='Virginie' AND last_name='Mitchell';
   5. **Answer** - *Answer1* - 39|Virginie|Mitchell|daisy.crist@altenwerthmonahan.biz
   5. **Terminal** - *Step2* - select * from addresses where user_id='39';
   5. **Answer** - *Answer2* - 41|39|12263 Jake Crossing|Roxanehaven|NY|                              34705
                               42|39|83221 Mafalda Canyon|Bahringerland|WY|24028
   5. **Terminal** - *Step3* - pdate addresses set city='New York', state='NY', zip='10108' where user_id=39;
   5. **Answer** - *Answer3* - 41|39|12263 Jake Crossing|New York|NY|10108
42|39|83221 Mafalda Canyon|New York|NY|10108

6. **Question** - How much would it cost to buy one of each tool?
   6. **Terminal** - select sum(price) from items where category like '%tool%';
   6. **Answer** - sum(price) 46477

7. **Question** - How many total items did we sell?
   7. **Terminal** - select sum(quantity) from orders;
   7. **Answer** - sum(quantity) 2125

8. **Question** - How much was spent on books?
   8. **Terminal** - SELECT SUM(orders.quantity*items.price) as                                total_spent_on_books FROM orders JOIN items on orders.item_id             = items.id WHERE items.category LIKE '%book%';
   8. **Answer** - total_spent_on_books 1081352     

9. **Question** - Simulate buying an item by inserting a User for yourself and an Order for that User.
   9. **Terminal** - *Step1* - insert into users (first_name, last_name, email) values ('Devin', 'Blankenship', 'DB@gmail.com'); 
   9. **Answer** - *Answer1* - id|first_name|last_name|email
                               51|Devin|Blankenship|DB@gmail.com
   9. **Terminal** - *step2* - insert into orders (user_id, item_id, quantity, created_at) values (51, 84, 05, datetime());
   9. **Answer** - *Answer2* - 378|51|84|5|2017-03-06 22:10:27