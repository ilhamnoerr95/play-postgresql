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
6. etc:https://www.postgresql.org/docs/current/datatype.html

### TABLE

how to create table:

1. CREATE TABLE name_tables (
   name TEXT.
   kode VARCHAR(20) not null,
   price INT,
   <!-- current timestamp akan mengisi value waktu saat ini -->
   created_at TIMESTAMP not null default current_timestamp
   ); => adjust as you want
2. \dt (to check table in database)
3. \d (to check type of table)

another example code sql:
a. drop table => alter table products
drop column deskripsi;
b. rename table => alter table products
rename column name to namaea;
c. drop table => drop table name_tables;
d. recreate table => truncate name_tables;

```
HOW TO INSERT DATA:
```
