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

```postgresql
CREATE TABLE name_tables (
   name TEXT.
   kode VARCHAR(20) not null,
   price INT,
   <!-- current timestamp akan mengisi value waktu saat ini -->
   created_at TIMESTAMP not null default current_timestamp
   ); => adjust as you want
```

## another example code sql:

```postgresql
1. \dt (to check table in database)
2. \d (to check type of table)
3. drop table => alter table products
drop column deskripsi;
4. rename table => alter table products
rename column name to namaea;
5. recreate table => truncate name_tables;

```

## HOW TO INSERT TABLE

```postgresql
INSERT INTO products(id, name, price, qty)
VALUES ('POOO1', null, 15000, 11);

<!-- insert multiple values -->
INSERT INTO products (id, name,price, qty)
VALUES ('POOO2', 'test', 20000, 12),
         ('POOO3', 'test3', 40000, 1),
          ('POOO4', 'test4', 30000, 10);
```

## HOW TO DISPLAY DATA TABLE

```postgresql
<!-- for all column -->
SELECT * FROM nama_tables;

<!-- could pick specific name columnt -->
SELECT name, id from table_name;

```
