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
