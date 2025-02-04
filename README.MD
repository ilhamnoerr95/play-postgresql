### REQUIREMENTS PLAY WITH POSTGRES

1. Install postgresql that you could using homebrew brew install postgresql@15 (for mac),or more information based on OS you could jump to the documentation postgresql
2. GUI for easy you for manage your database. examples gui: dbeaver, etc
3.

### tipe data:

1. Type Number:
   a. SmallInt
   b. Integer: bilangan bulat
   c. BigInt
   d. Decimal/floatin point
   e. Numberic
   f. Real
   g. double precision
   h. small serial
   i. serial
   j. bigserial

2. Type String: decide min lenght of characters char and varchar
   a. Char & varchar = max 65535
   b. Text = not have max characters
3. Type Data & Time
   a. timestamp: YYYY MM DD HH:mm:ss
   b. date: YYYY MM DD
   c. Time: HH:mm:ss
4. TYPE data boolean (true or false only 2 data)
5. TYPE data ENUM: data of type that have default/fix value
6. link data Type: [LINK](https://www.postgresql.org/docs/current/datatype.html)

### TABLE

how to create table:

````postgresql
CREATE TABLE name_tables (
   name TEXT.
   kode VARCHAR(20) not null,
   price INT,
   <!-- current timestamp akan mengisi value waktu saat ini -->
   created_at TIMESTAMP not null default current_timestamp
   ); => adjust as you want
``

## HOW TO INSERT TABLE

```postgresql
INSERT INTO products(id, name, price, qty)
VALUES ('POOO1', null, 15000, 11);

<!-- insert multiple values -->
INSERT INTO products (id, name,price, qty)
VALUES ('POOO2', 'test', 20000, 12),
         ('POOO3', 'test3', 40000, 1),
          ('POOO4', 'test4', 30000, 10);


````

## HOW TO DISPLAY DATA TABLE

```postgresql
<!-- for all column -->
SELECT * FROM nama_tables;

<!-- could pick specific name columnt -->
SELECT name, id from table_name;

```

## PRIMARY KEY

every single data have a primary key, primary key as id for the column table. primary key have to be unique, primary key indetity for the column table.

> [!NOTE]
> Composite primary key is a primary key that could set up in multiple column. Comnbintation primary key in multiple column it will be good when used on relation many to many.

```postgresql
<!-- add primary key FOR first time -->
CREATE TABLE nama_tables (
    id VARCHAR(10) NOT NULL,
    PRIMARY KEY (id)
)
```

## WHERE CLAUSE

this how we could find/search data with the condition what we want. Condition could using for update,delete data, carefully when we want to update/delete the data, if we wrong input update the data without using 'where clause', all data we'll be update.

```postgresql
<!-- pick all column in name_table where condition is qty === 0 -->
SELECT * FROM name_tables
WHERE qty = 0;

<!-- how to update with alter -->
UPDATE name_tables
SET name_column = 'food'
WHERE id = 'P0001';

<!-- when update multiple value -->
UPDATE name_tables
SET name_column = 'food'
    name_column2 = 'beraq'
WHERE id = 'P0002';

<!-- delete data -->
DELETE FROM name_table
WHERE id = 'PO001'
```

> [!TIP]
> Postgres have "ALIAS" benfical feature. this feature is good when using in case JOIN feature. change real name column to become alias name.

```postgresql
SELECT
    id as 'kode id',
    name as nama
from name_table as p;

```

## WHERE OPERATOR

WHERE operator same as operators in js or another language tho.

```postgresql
SELECT * FROM name_table
WHERE price > 15000

SELECT * FROM name_table
WHERE price = 15000

SELECT * FROM name_table
WHERE price <= 15000

```

## CONDITION OR, AND

> [!NOTE]
>
> 1. explanation OPERATOR AND have 2 conditions: when 2 conditions are true the result will be true (DISPLAY THE DATA) and the rest of it will be false.
> 2. EXPLAINS operator OR condition: when 2 condition are false the result will be false and the rest of it will true. OR condition will display data one of true condition.

```postgresql
SELECT * FROM name_table
    WHERE price > 15000
    AND ID = 'POOO2';

<!-- OR CONDITIONS -->
SELECT * FROM name_table
    WHERE price > 15000
    OR ID = 'POOO2';

<!-- multiple conditions, double brackets will be prioritize. -->
SELECT * FROM name_table
    WHERE (qty > 2 OR category = 'food')
    AND price < 200000;

```

## CONDITION LIKE OPERATOR

OPERATOR LIKE used to search for part of the data in a string,

> [!WARNING]
> Operator LIKE NOT RECOMENDED to search large of data because it'll make slow searching. Case sensitive has an effect with this Operator. when wanna not affected by case sensitive please using ILIKE operator.

```postgresql
SELECT * FROM name_table
WHERE name ILIKE '%mie%' => string have mie

SELECT * FROM name_table
WHERE name ILIKE 'b%' => prefix have b

SELECT * FROM name_table
WHERE name ILIKE '%c' => suffix have c

SELECT * FROM name_table
WHERE name NOT LIKE '%mie%' => not like mie

```

## NULL OPERATOR

find null data, cannot using basic operator to search null condition, IS NULL search NULL, IS NOT NULL search not null

## BETWEEN OPERATOR

simplify condition of WHERE ex: where price >= 1000 and price <= 2000

```postgresql
select * from name_table
WHERE price BETWEEN 1000 and 2000;

```

## IN OPERATOR

OPERATOR that search several value in 1 column

```postgresql
SELECT * FROM name_table
where category IN ('food', 'water')

```

## ORDER CLAUSE

ordering column by ASC and DESC

```postgresql
SELECT * FROM name_table
ORDER BY price ASC, id DESC;

```

## LIMIT CLAUSE

display all data in db is not wise when the data already large, with LIMIT CLAUSE will limit data to display and used to pagination in app with combination OFFSET.

```postgresql
SELECT * FROM name_table
WHERE price > 0
ORDER BY id ASC
LIMIT 3;

<!-- USING OFFSET, ex length of data are 10 -->
SELECT * FROM name_table
WHERE price > 0
ORDER BY id ASC
<!-- OFFSET MEANs, take data from index/offset 3 to LIMIT -->
LIMIT 2 OFFSET 2;

```

## SELECT DISTINC DATA

When we query select, sometime we got duplicates data. there is many duplicates of data, so when you want to avoid duplicate you can using DISTINC. add before column.

```postgresql
SELECT DISTINCT name_column
FROM products;

```

## AUTO INCREMENT

We will use SERIAL TYPE for increment

```postgresql
 CREATE TABLE name_table (
    id SERIAL not null,
    first_name VARCHAR(100),
    last_name VARCHAR(100),

    PRIMARY KEY (id)
 )

 <!-- see last increment -->
 select currval('admin_id_seq');
```

## SEQUENCE

In background actually Serial type using sequence. Sequance is a function created increment. when you using serial, posgresql as default will running sequence function to primary key.

### how to Create Sequence?

```postgresql
<!-- CREATE SEQUENCE -->
create sequence name_sequence;

<!-- call sequence, automatically will increment -->
SELECT nextval('name_sequence')

<!-- take last sequence value -->
SELECT currval('name_sequence')

```

## FLOW CONTROL

flow control same as IF ELSE BUT NOT COMPLICATED THAN another language.

```postgresql
SELECT id,
    CASE category
        WHEN 'food' THEN 'enak'
        WHEN 'DRINK' Then 'seger'
        ELSE 'APAAN TUH?'
        END AS category
FROM products;

<!-- with operator-->
select id ,
	price,
	case
	when price < 10000 then 'murah'
	when price <= 20000 then 'mahal'
	else 'sangat mahal'
    <!-- end as new column -->
	end as murah
from products;
```

## AGGREGATE FUNCTION

functino that find out max/min/average etc from value

```postgresql
    select COUNT(id) AS "total Id" from products;

```

## GROUPING

sometime we doing aggregate data want to grouping per category or anything.

```postgresql
SELECT category,
COUNT(id) AS "Total products" from products
group by category;

```

## HAVING CLAUSE

Filtering after grouping. this just applies for grouping, as well having clause always continued by aggregate function.

```postgresql

SELECT category,
COUNT(id) AS "Total products" from products
group by category
<!-- display total product bigger than 3 -->
HAVING COUNT(id) > 3;

SELECT category,
MAX(price) AS "Max Price", min(price) as "Min Price", avg(price) as "Average Price" from products
group by category
having AVG(price) > 20000

```

## CONSTRAINT

Rules of table, make table clear as well keep it good for the data. Constrain like validation for data.
a. uniques constrain rule makesure the data always be uniques

### check constraint

check constraint could add condition for checking/validation data before data save to the database.

```postgresql
CREATE TABLE customer (
    id SERIAL not null,
    email VARCHAR(255) NOT NULL,
    username VARCHAR(255) NOT NULL,
    fullname VARCHAR(255),
    PRIMARY KEY (id),
    CONSTRAINT name_constrain UNIQUE (email)

);

<!-- delete constrain -->
ALTER TABLE customer
    DROP CONSTRAINT name_constrain;

<!-- add constraint -->
ALTER TABLE customer
    ADD CONSTRAINT name_constrain UNIQUE (email)

<!-- CHECK CONSTRAINT -->
<!-- this add constrain for existing table -->
ALTER TABLE products
    ADD CONSTRAINT price_check CHECK (price < 10000)
```

## INDEX

As default postgresql will save the data to disk like general table. Thats means postgresql will find a data from first to end of the row, so more and more data proccessing of find data will be slow. How to find data will be easier that using Index, when we created Index, posgres will save the data as Balance-tree.
primary key and unique constrain as default have a index.

### Side Effect index

index cannot effect to manipulate data process like (UPDATE,DELETE, AND INSERT). when we create index, postgres will do processing update, delete and insert every adding some data in table.

> [!NOTE]
> When the some column no have index, the data will be searched from first to end of data. \
> for Ex: when id (have index ,col1), name(no index, col2) it will search by default without using index in other side when both of id(col1) and name(col2) have index, searching data will be faster because combination 2 of column index. \
> Another example(col1, col2,col3), when we find data with combination (col1), or (col1,col2) or (col1,col2,col3) index will be working but when we want combination find data with (col1, col3) it'll not work because we no create for that combination.

> [!WARNING]
> when the data bigger and table have many index manipulate proccessing update, delete, insert will be slow. Please to make wise decision for create INDEX.

```postgresql
<!-- adding index -->
CREATE INDEX name_index ON name_table (column);

<!-- delete index -->
DROP INDEX name_index;

<!-- example adjust condition for add index in column -->
CREATE INDEX name_index ON name_table (column1, column3);


```

## FULL TEXT SEARCH

somethimes we find a data with LIKE OPERATOR. LIKE OPERATOR will searching the data from first line to last lines, that make LIKE OPERATOR will be slower.
Adding index in table will not work for LIKE OPERATOR.

Full text search could find part of word in column with type string data. This same LIKE OPERATOR, but we could find the data no only equal operator.

FULL TEXT operator not flexible LIKE OPERATOR;

> [!NOTE]
> query operator, to_tsquery support many operator
> & for AND , | for OR , ! for NOT, "" for all data. Find data per word.
> easy way to create index in full text search to automatically is when create a new table just put on type TSVECTOR for column, so that column will be automatically created index for FULL TEXT SEARCH.

```postgresql
SELECT * FROM table
WHERE to_tsvector(column_name) @@ to_tsquery("nae")

<!-- how to create index with full text search -->
<!-- first thing first u must know about cfgname or based language that u want to used -->
<!-- first check -->
select cfgname from pg_ts_config;

<!-- create index -->
CREATE INDEX product_name_search ON table_name using gin (to_tsvector('indonesian', name_column));

<!-- how to using full text search that registered by index -->
SELECT * from products WHERE name_column @@ to_tsquery('blabla')

<!-- example for query operator -->
SELECT * from products WHERE name_column @@ to_tsquery('blabla | test')

```

## TABLE RELATIONSHIP

Table relation feature that relation between table. ex: when we create sales table logically we must have data of products that sell.

### FOREIGN KEY

foreign key used as reference for another table, that means is column of table1/sales table reference for table2/product table. type column of foreign key have to same with refrence table column. Value of foreign key have to same with refrence value in related column of table.

### BENEFIT OF FOREIGN KEY

foreign makesure the data that want to input in column of table
have to same with table of reference. Foreign key as a constraint which is the table of reference related to the foreign key cannot remove from table.

> [!NOTE]
> As default, value of reference table cannot be removed when data column of foreign-key have same value with reference column table. But that not means, cannot be removed. See how to know about behavior of foreign-key at the folder provided.



```postgresql
<!-- create foreign key -->
create table wishlist (
id UUID not null,
id_product VARCHAR(10) not null,
description TEXT,
primary key(id),
constraint fk_wishlist_product foreign KEY (id_product) references products (id)

<!-- delete foreign key -->
ALTER TABLE name_table
DROP CONSTRAINT fk_wishlist_product;

<!-- add foreign key that product table had created -->
ALTER TABLE name_table
ADD CONSTRAINT fk_wishlist_product foreign KEY (id_product) references products (id);
)


```

### JOIN TABLE
menggabungkan beberapa table menjadi 1 table, dimana kita perlu menentukan table mana yang memiliki referensi atas foreign key dari sebuah table.

> [!NOTE]
> perlu diingat semakin banyak join table akan semakin berat proses dari quernya, idealnya melakukan join table maksimal adalah 5 table.

```sql
-- table wishtlist ingin join dengan table product
Select * from wishlist_table 
-- join di table product di kolom product.id dengan wishlist_table.id_product
JOIN product ON product.id = wishlist_table.id_product

-- join multiple table
SELECT customer.email, products.id, products.price , wishlist.description 
FROM wishlist
JOIN product ON product.id = wishlist.id_product
JOIN customer ON customer.id = wishlist.id_customer;
```

### ONE TO ONE RELATIONSHIP TABLE
One to one relationship is very simple relation between table, its mean one table just only relation to one table not more. 

```sql
select c.id ,c.email, c.username, w.balance 
from customer as c
join wallet as w on w.id_customer  = c.id;

```

### ONE TO MANY RELATIONSHIP TABLE
relation that one data could using for many data in relation table. ex: 1 category could using for more than 1 products, 1 category have more than 1 products.

### MANY TO MANY RELATIONSHIP TABLE
many to many relationships are very confused for a newbie, which is many to many relation between 2 table that first table have many relation to table 2 or vice versa. ex: product table and sale, that product could sale many times,even sale could more than for 1 products.

> [!NOTE]
> brief of many to many relations:
> 1. id_product in table order: \
> a. when add id_product to order table that means, this case could products sold many times. but we just could order only 1 products because id_product column represents of 1 products not more.
> 2. id_order in table products: \
> a. this case we could 1 order have many products, but the problem is 1 products just only sold 1 times.
>
> The solution of this problem is we have to add 1 table between table products and sale, we could leverage this table as bridge for join relation many to many. 

```sql
-- create for intermediary table many to many
CREATE TABLE order_detail (
    id_product INT NOT NULL, 
    id_order INT NOT NULL,
    price INT NOT NULL,
    quantity INT NOT NULL,
    PRIMARY KEY (id_product, id_order)
)

-- dont forget to add foreign key order_detail to both of table ordern and products
ALTER TABLE order_detail ADD CONSTRAINT fk_order_detail_product FOREIGN KEY (id_product) REFERENCES products (id);

ALTER TABLE order_detail ADD CONSTRAINT fk_order_detail_order FOREIGN KEY (id_order) REFERENCES orders (id);

-- join table
select o.id, od.id_order,od.id_product,od.price,od.quantity ,p.description from orders as o
join order_detail as od on od.id_order = o.id
join products as p on od.id_product = p.id;

```

### Various JOIN TABLE
1. Inner Join: Mecachinsm that first table have relation with second table, if one of table have no relation this mechanism join cannot be used.
2. Left Join: this mechanism same with inner join the diffrent when the first table will take all the data/display the data even its no have relation on secondary table, if the second table has no relation the data will be null. EX: when category table have no relation on product table the data will be displayed, but the other side when product table have no relation on category table the data will be null.
3. Right Join: this mechanism same as LEFT JOIN but the  diffrent is the data of second table will be display even that table have no relation on second table, but the other side if table one have no relation on second table the data will be null.
4. Full Join: this mechanism combination of left and right join table which is bot of data table will be display even each table have no relation.

```sql
-- this will display only product that have a cateogry or vice versa
SELECT * FROM category INNER JOIN products ON products.id_category = category.id;

-- LEFT JOIN
SELECT * FROM category lEFT JOIN products ON products.id_category = category.id;

-- RIGHT JOIN
SELECT * FROM category RIGHT JOIN products ON products.id_category = category.id;

-- FULL JOIN
SELECT * FROM category FULL JOIN products ON products.id_category = category.id;


```

### SUBQUERY
Feature that help seek the data with select inside WHERE CLAUSE or FROM. Subquery could do in FROM clause.

```sql
-- subquery, FIND AVERAGE DATA WITH SUBQUERY
SELECT * FROM products where price > (SELECT AVG(price) from PRODUCTS);

-- subquery with from
select MAX(price) from (
    select products.price as price from category join products on products.id_category = category.id
) as contoh;
```

### SET OPERATOR
Operation of 2 result from SELECT query. there is more operator set as follows: 
1. UNION: combine 2 select query where have duplicate data, the duplicate data will be remove from query result.
2. UNION ALL: same as UNION but the duplicates data stay still display.
3. INTERSECT: COMBINE 2 query, however the data that only fetch just only  there is of first query and second query.
4. EXCEPT: OPERATION when the first query will be remove with secondary query. its mean,if there is data in first query same with second query then the result query will be removed from EXCEPT
   
```SQL
-- union query combine 2 data or table become 1 when the data have duplicate result of query will be remove the duplicate data
-- could using without DISTINC
-- the main point is, it will be display all data even duplicate or not but when first table and second table have duplicate the result will display only one.
SELECT DISTINCT email from customer
UNION 
SELECT DISTINCT email from guestbooks; 

-- union all combine 2 table bocome 1 for aggregate resul or count all table become 1 table
select email, COUNT(email) from (select email from customer union all select email from guestbooks) as combine_table group by email;

-- INTERSECT: THE FIRST QUERY WILL BE INTERSECT WITH SECONDARY QUERY,
-- when the first table have'nt duplicate on secondary table, this will be display the data have duplicate but the result of data will be 1 data for each duplicate.
-- only display duplicate data then duplicate data will represent one of both table means only 1 data will be displayed.
SELECT DISTINCT email from customer
INTERSECT 
SELECT DISTINCT email from guestbooks; 

-- EXCEPT: FIND DATA THAT customer not write down on the guestbooks, display data that have a duplicate on the secont table
SELECT DISTINCT email from customer
EXCEPT 
SELECT DISTINCT email from guestbooks; 

```

### TRANSACTION
Mechanism of more than one action with 1 command. ex: when we create online shop and then go with order button then we have more to do like create order data, create order_detail. its means we could 1 act with 1 command at once. if error occurs in one of command, hopefully previous command will be cancelled, to keep data consistent.

Database Transaction is DBMS feature where some actions considered to be a unit command. if there is failed process in transaction then automatically previous command will be cancelled. and if the command successfully then all command will be successfully to.

> [!NOTE]
> transaction cannot be used in DDL (data defintion language) command like create table, remove column etc, just only used in DML (data manipulation language) like INSERT, UPDATE, DELETE

Command transaction in PostgresSql:
1. START TRANSACTION: starting proccess  transaction, the next proccess will be considered transaction after COMMIT OR ROLLBACK COMMAND
2. COMMIT: Saving the proccess transaction or data permanently in database.
3. ROLLBACK: Canceling the proccess transaction or data will not be saved in database.

``` sql
-- ALWAYS BEGIN WITH START TRANSACTION, WHEN THE DATA HAVE BEEN COMMIT OR ROLLBACK THE START TRANSACTION WILL BE DONE.SO,IF WE WANNA GO WITH ANOTHER TRANSACTION BEGIN WITH START TRANSACTION AGAIN.

START TRANSACTION
INSERT INTO guestbooks(email, title, content) 
VALUES ('transaction@gmail.com', 'transaction1', 'transaction 1'), 
	('transaction2@gmail.com', 'transaction2', 'transaction 2')
;

commit

INSERT INTO guestbooks(email, title, content) 
VALUES ('rollback3@gmail.com', 'rollback3', 'rollback 3'), 
('rollback4@gmail.com', 'rollback 4', 'rollback 4');

rollback

```

### LOCKING
process locking data in dbms, locking data is very important thas make db consistent, beacause there is condition many user will be data in the same time, if do not have LOCKING it'll be RACE CONDITION when change user in the same time.
locking record, when do TRANSACTION process , then we go to change the data, automatically the data will be lock. so TRANSACTION FEATURE IS VERY USEFULL AND SAFE FOR DATA MANIPULATION. especially manipulation than 1 times.  Data will lock ntil reach COMMIT OR ROLLBACK.

>[!WARNING]
> be cautios with DEADLOCK this condition occurs when 2 data prcess waiting each other that both of data awaited locked by another process, so that waiting it will be never finish.

### SCHEMA
When we created database postgres, automatically have schema with name public, and we created table that table will save in schema public.

when we created table in schema selected, the table will be automatically saved inside schema selected. if we decided to save with manually method, we could add some prefix of table name. ex: schemaname.schematable.

```sql
select current_schema();

SHOW search_path;
<!-- create and delete schema -->
CREATE SCHEMA EX;
-- BE CAUTION WHEN DROP SCHEMA, ALL TABLE INSIDE SCHEMA WILL BE REMOVE TO
DROP SCHEMA EX;

-- move schema
SET search_path TO SCHEMA_NAME;

-- example when we not selected the schema 
-- create in new schema, just called prefix schema that what we wanna call.
CREATE TABLE schema_name.name_table(id SERIAL NOT NULL, name VARCHAR(250));

```

### USER MANAGEMENT
user root as default postgresql make main user as super administrator that means freely to do anything like SELECT, OR MANIPUTATION DATABASE. BUT in best practice no using user root, we have to specified user based on the applikaction or database.

```sql
CREATE ROLE ilham

DROP ROLE ilham
```

### backup database

```sql
pg_dump --host=localhost --port=5432 --dbname=belajar --username=nama_users --format=plain --file=/Users/fdn-user/Documents/bakcup/backup.sql

-- UNTUK RESTORE 
psql --host=localhost --port=5432 --dbname=belajar_restore --username=nama_users --file=/Users/fdn-user/Documents/bakcup/backup.sql
```


## ANOTHER EXAMPLE SQL CODE
Remains of another example sql code

```postgresql
1. \dt (to check table in database)
2. \d (to check type of table)
3. drop table => alter table products
drop column deskripsi;
4. rename table => alter table products
rename column name to namaea;
5. recreate table => truncate name_tables;


<!-- add primary key -->
ALTER TABLE products
    add PRIMARY KEY (id)

<!-- add type data enum -->
<!-- for validate data with enum -->
CREATE TYPE type_name AS ENUM("food", "drink", "etc")

<!-- add column -->
ALTER TABLE table_name
add column INT;
```
