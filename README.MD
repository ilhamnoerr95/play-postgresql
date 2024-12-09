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

When we query select, someime we got duplicates data. there is many duplicates of data, so when you want to avoid duplicate you can using DISTINC. add before column.

```postgresql
SELECT DISTINCT category
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
> easy for for create index in full text search to automatically is when create a new table just put on type TSVECTOR for column, so that column will be automatically created index for FULL TEXT SEARCH.

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
```
