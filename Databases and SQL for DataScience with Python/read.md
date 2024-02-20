# SQL Cheat Sheet: Accessing Databases using Python

## SQLite

| Topic        | Syntax                         | Description                                                                                                                         | Example                                                           |
|--------------|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| connect()    | `sqlite3.connect()`            | Create a new database and open a database connection to allow sqlite3 to work with it. Call `sqlite3.connect()` to create a connection to the database INSTRUCTOR.db in the current working directory, implicitly creating it if it does not exist. | ```python
import sqlite3
con = sqlite3.connect("INSTRUCTOR.db")
``` |
| cursor()     | `con.cursor()`                 | To execute SQL statements and fetch results from SQL queries, use a database cursor. Call `con.cursor()` to create the Cursor.    | ```python
cursor_obj = con.cursor()
``` |
| execute()    | `cursor_obj.execute()`         | The `execute` method in Python's SQLite library allows to perform SQL commands, including retrieving data from a table using a query like "Select * from table_name." When you execute this command, the result is obtained as a collection of table data stored in an object, typically in the form of a list of lists. | ```python
cursor_obj.execute('''insert into INSTRUCTOR values (1, 'Rav', 'Ahuja', 'TORONTO', 'CA')''')
``` |
| fetchall()   | `cursor_obj.fetchall()`        | The `fetchall()` method in Python retrieves all the rows from the result set of a query and presents them as a list of tuples.    | ```python
statement = '''SELECT * FROM INSTRUCTOR'''
cursor_obj.execute(statement)
output_all = cursor_obj.fetchall()
for row_all in output_all:
    print(row_all)
``` |
| fetchmany()  | `cursor_obj.fetchmany()`       | The `fetchmany()` method retrieves the subsequent group of rows from the result set of a query rather than just a single row. To fetch a few rows from the table, use `fetchmany(numberofrows)` and mention how many rows you want to fetch. | ```python
statement = '''SELECT * FROM INSTRUCTOR'''
cursor_obj.execute(statement)
output_many = cursor_obj.fetchmany(2)
for row_many in output_many:
    print(row_many)
``` |
| read_sql_query() | `read_sql_query()`          | `read_sql_query()` is a function provided by the Pandas library in Python, and it is not specific to MySQL. It is a generic function used for executing SQL queries on various database systems, including MySQL, and retrieving the results as a Pandas DataFrame. | ```python
df = pd.read_sql_query("select * from instructor;", conn)
``` |
| shape        | `dataframe.shape`             | It provides a tuple indicating the shape of a DataFrame or Series, represented as (number of rows, number of columns).             | ```python
df.shape
``` |
| close()      | `con.close()`                  | `con.close()` is a method used to close the connection to a MySQL database. When called, it terminates the connection, releasing any associated resources and ensuring the connection is no longer active. This is important for managing database connections efficiently and preventing resource leaks in your MySQL database interactions. | ```python
con.close()
``` |
| CREATE TABLE | `CREATE TABLE table_name ( column1 datatype constraints, column2 datatype constraints, ... );` | The `CREATE TABLE` statement is used to define and create a new table within a database. It specifies the table's name, the structure of its columns (including data types and constraints), and any additional properties such as indexes. This statement essentially sets up the blueprint for organizing and storing data in a structured format within the database. | ```sql
CREATE TABLE INTERNATIONAL_STUDENT_TEST_SCORES (
    country VARCHAR(50),
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    test_score INT
);
``` |

## Db2

| Topic           | Syntax                                                                           | Description                                                                                                                                                                                                                     | Example                                                          |
|-----------------|----------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| connect()       | `conn = ibm_db.connect('DATABASE=dbname; HOST=hostname;PORT=port;UID=username; PWD=password;', '', '')` | `ibm_db.connect()` is a Python function provided by the `ibm_db` library, which is used for establishing a connection to an IBM Db2 or IBM Db2 Warehouse database. It's commonly used in applications that need to interact with IBM Db2 databases from Python. | ```python
import ibm_db
conn = ibm_db.connect('DATABASE=mydb;HOST=example.com;PORT=50000;UID=myuser;PWD=mypassword;', '', '')
``` |
| server_info()   | `ibm_db.server_info()`                                                          | `ibm_db.server_info(conn)` is a Python function provided by the `ibm_db` library, which is used to retrieve information about the IBM Db2 server to which you are connected.                                                                                                    | ```python
server = ibm_db.server_info(conn)
print("DBMS_NAME: ", server.DBMS_NAME)
print("DBMS_VER:  ", server.DBMS_VER)
print("DB_NAME:   ", server.DB_NAME)
``` |
| close()         | `con.close()`                                                                    | `con.close()` is a method used to close the connection to a db2 database. When called, it terminates the connection, releasing any associated resources and ensuring the connection is no longer active. This is important for managing database connections efficiently and preventing resource leaks in your db2 database interactions. | ```python
con.close()
``` |
| exec_immediate()| `sql_statement = "SQL statement goes here"
stmt = ibm_db.exec_immediate(conn, sql_statement)` | `ibm_db.exec_immediate()` is a Python function provided by the `ibm_db` library, which is used to execute an SQL statement immediately without the need to prepare or bind it. It's commonly used for executing SQL statements that don't require input parameters or don't need to be prepared in advance.                                     | ```python
# Lets first drop the table INSTRUCTOR in case it exists from a previous attempt.
dropQuery = "drop table INSTRUCTOR"
dropStmt = ibm_db.exec_immediate(conn, dropQuery)
``` |

**Author(s):** Abhishek Gagneja, D.M Naidu
