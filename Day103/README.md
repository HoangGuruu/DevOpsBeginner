![Alt texts](../Images/p1.png)

# Day 103 | Use EC2 Ubuntu Setup database MySQL, Postgresql
# MySQL
1. Install MySQL
First, update your package list and install MySQL:

```bash
sudo apt update
sudo apt install mysql-server
```
2. Start and Enable MySQL Service
Ensure the MySQL service is running and enabled to start on boot:

```bash
sudo systemctl start mysql
sudo systemctl enable mysql
```
3. Secure MySQL Installation
Run the security script to improve MySQL security:
```bash

sudo mysql_secure_installation
```
Follow the prompts to set the root password and apply security settings.
4. Access MySQL
Log in to the MySQL shell as the root user:

```bash
sudo mysql -u root -p
```
5. Create a Database
To create a new database, use the CREATE DATABASE statement:

```sql
CREATE DATABASE mydatabase;
```
6. Create a User (Optional)
If you want to create a new user, you can do so with:

```sql
CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
```
7. Grant Privileges to the User (Optional)
Grant all privileges on the database to the user:

```sql
GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';
FLUSH PRIVILEGES;
```
8. Connect to the Database
To connect to the specific database as the created user:

```bash
mysql -u myuser -p mydatabase
```
9. Create a Table
To create a table, use the CREATE TABLE statement:

```sql
CREATE TABLE mytable (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```
10. Show Databases
To list all databases:

```sql
SHOW DATABASES;
```
11. Show Tables
To list all tables in the current database:

```sql
SHOW TABLES;
```
12. Insert Data into Table
To insert data into a table:

```sql
INSERT INTO mytable (name, age) VALUES ('Alice', 30), ('Bob', 25);
```
13. Select Data from Table
To select all data from a table:

```sql
SELECT * FROM mytable;
```
14. Exit the MySQL Shell
To exit the MySQL shell:

```sql
EXIT;
```

# PostgreSQL
1. Install PostgreSQL
First, update your package list and install PostgreSQL:

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
```
2. Start and Enable PostgreSQL Service
Ensure the PostgreSQL service is running and enabled to start on boot:

```bash
sudo systemctl start postgresql
sudo systemctl enable postgresql
```
3. Access PostgreSQL
Switch to the postgres user and open the PostgreSQL prompt:

```bash
sudo -i -u postgres
psql
```
4. Create a Database
To create a new database, use the CREATE DATABASE statement:

```sql
CREATE DATABASE mydatabase;
```
5. Create a User (Optional)
If you want to create a new user, you can do so with:

```sql
CREATE USER myuser WITH PASSWORD 'mypassword';
```
6. Grant Privileges to the User (Optional)
Grant all privileges on the database to the user:

```sql
GRANT ALL PRIVILEGES ON DATABASE mydatabase TO myuser;
```
7. Connect to the Database
Connect to the specific database:

```bash
\c mydatabase
```
8. Create a Table
To create a table, use the CREATE TABLE statement:

```sql
CREATE TABLE mytable (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    age INT
);
```
9. Show Databases
To list all databases:

```sql
\l
```
10. Show Tables
To list all tables in the current database:

```sql
\dt
```
11. Insert Data into Table
To insert data into a table:

```sql
INSERT INTO mytable (name, age) VALUES ('Alice', 30), ('Bob', 25);
```
12. Select Data from Table
To select all data from a table:

```sql
SELECT * FROM mytable;
```
13. Exit the PostgreSQL Prompt
To exit the PostgreSQL prompt:

```sql
\q
```
14. Delete table
```css
\c mydatabase
DROP TABLE mytable;
```
15. Delete database
```css
DROP DATABASE mydatabase;
```
