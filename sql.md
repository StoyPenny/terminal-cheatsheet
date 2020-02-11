# MySQL
A collection of useful MySQL terminal commands. 

---------------


### Access MySQL
Login to a MySQL session. 
```cmd
mysql -u [username] -p;  // will prompt for password
```
<br>

### Show All Databases
Show all of the available databases.
```cmd
show databases;
```
<br>

### Create A Database
Select a database.
```cmd
create database [database];
```
<br>

### Select A Database
Select a database.
```cmd
use [database];
```
<br>

### Show All Tables
Show all of the tables in the active database.
```cmd
show tables;
```
<br>

### Show Table Structure
Show the table structure for a specific table.
```cmd
describe [table];
```
<br>

### Select Data From Table
Select data from the active database.
```cmd
SELECT * FROM [table];
```
<br>

### Update Data In A Table
Update a row in the database based on conditions.
```cmd
UPDATE [table] SET [column] = '[updated-value]' WHERE [column] = [value];
```
<br>

### Clone A Database
Copy a database to another database on the same server.
```cmd
mysqldump -u <user name> --password=<pwd> <original db> | mysql -u <user name> -p <new db>
```
<br>

### Backup Database
Create a backup of a single database. You must specify the database name as well as the folder where the database will be saved to. 
```
mysqldump -u USER -p products > /mnt/backups/products.sql
```
<br>

### Backup All Databases
Backup all databases in one command, just specifiy a location to store the backup. 
```
mysqldump -u USER -p --all-databases > /mnt/backups/all_databases.sql
```
<br>

### Backup and Compress Databases
Make a backup of the database and also compress the database to save space on the server. You will need to specify the database that you would like to backup as well as where you would like to store it. 
```
mysqldump -u USER -p -C products > /mnt/backups/products.sql.tgz
```
<br>

### Get Size of All Tables in Database (KB)
Get the KB size of all the tables in a database.
```sql
SELECT
  TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024) AS `Size (KB)`
FROM
  information_schema.TABLES
WHERE
  TABLE_SCHEMA = "{{database_name}}"
ORDER BY
  (DATA_LENGTH + INDEX_LENGTH)
DESC;
```
<br>

### Get Size of All Tables in Database (MB)
Get the MB size of all the tables in a database.
```sql
SELECT
  TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024 / 1024) AS `Size (MB)`
FROM
  information_schema.TABLES
WHERE
  TABLE_SCHEMA = "{{database_name}}"
ORDER BY
  (DATA_LENGTH + INDEX_LENGTH)
DESC;
```
<br>

### Get Size of One Table in a Database (KB)
Get the KB size of all the tables in a database.
```sql
SELECT
  TABLE_NAME AS `Table`,
  ROUND((DATA_LENGTH + INDEX_LENGTH) / 1024) AS `Size (KB)`
FROM
  information_schema.TABLES
WHERE
  	TABLE_SCHEMA = "{{database_name}}"
  AND
    TABLE_NAME = "{{table_name}}"
ORDER BY
  (DATA_LENGTH + INDEX_LENGTH)
DESC;
```
