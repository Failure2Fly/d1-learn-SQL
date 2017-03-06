Questions:

How many users are there?
Termianl - sqlite> select count (id) from users;
Answer - count (id) 50

What are the 5 most expensive items?

Terminal - select title, price from items order by price desc limit 5;
Answer -    Small Cotton Gloves|9984
            Small Wooden Computer|9859
            Awesome Granite Pants|9790
            Sleek Wooden Hat|9390
            Ergonomic Steel Car|9341

What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

Terminal - select title, category, price from items where category like '%books%' order by price asc limit 1;
Answer - Ergonomic Granite Chair|Books|1496


Who lives at "6439 Zetta Hills, Willmouth, WY"? 

Terminal - select * from addresses where street like '%6439 Zetta Hills%';
Answer - 43|40|6439 Zetta Hills|Willmouth|WY|15029

Do they have another address?

Terminal - select * from addresses join users on user_id = users.id where user_id='40';
Answer - 43|40|6439 Zetta Hills|Willmouth|WY|15029|40|Corrine|Little|              rubie_kovacek@grimes.net
         44|40|54369 Wolff Forges|Lake Bryon|CA|31587|40|Corrine|Little|rubie_kovacek@grimes.net


Correct Virginie Mitchell's address to "New York, NY, 10108".
Terminal - Step1 - select * from users where first_name='Virginie' AND last_name='Mitchell';
Answer1 - 39|Virginie|Mitchell|daisy.crist@altenwerthmonahan.biz

Step2 - select * from addresses where user_id='39';
Answer2 - 41|39|12263 Jake Crossing|Roxanehaven|NY|34705
          42|39|83221 Mafalda Canyon|Bahringerland|WY|24028

Step3 - pdate addresses set city='New York', state='NY', zip='10108' where user_id=39;
Answer3 - 41|39|12263 Jake Crossing|New York|NY|10108
42|39|83221 Mafalda Canyon|New York|NY|10108


How much would it cost to buy one of each tool?
Terminal - select sum(price) from items where category like '%tool%';
Answer - sum(price) 46477

How many total items did we sell?
Terminal - select sum(quantity) from orders;
Answer - sum(quantity)
         2125


How much was spent on books?
Terminal - SELECT SUM(orders.quantity*items.price) as                                total_spent_on_books FROM orders JOIN items on orders.item_id             = items.id WHERE items.category LIKE '%book%';
Answer -  total_spent_on_books
          1081352


Simulate buying an item by inserting a User for yourself and an Order for that User.
Step1 - insert into users (first_name, last_name, email) values ('Devin',          'Blankenship', 'DB@gmail.com'); 
Answer1 - 
        id|first_name|last_name|email
        51|Devin|Blankenship|DB@gmail.com
step2 - insert into orders (user_id, item_id, quantity, created_at)               values (51, 84, 05, datetime());
answer2 - 378|51|84|5|2017-03-06 22:10:27