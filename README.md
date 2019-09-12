# Data_Admin_101

# Objectives
- Create a SQL database 
- Create a SQL table 
- Create rows in a SQL table 
- Alter entries 
- Delete entries 
- Commit changes using SQLite3

# Working Directory - Previewing Files
In bash, you can use `ls` command to preview files and folders in the current working directory. 

```python
ls
```

    Data_admin_101.ipynb       README.md 

# Creating a Database
creating a database is as easy as connecting a database to non-existing database. 

```python
import sqlite3

conn = sqlite3.connect('pets.db')
c = conn.cursor()

## Repreview your Files 
Use the `ls` command again. You should see you newly created database there.

```python
ls
```
    Data_admin_101.ipynb       README.md        pets.db
    
## Creating Tables 
Remember we use our cursor to execute our SQL statments and statements must be wrapped in quotes ('''SQL statement here''') 

```python
c.execute('''CREATE TABLE cats (
                                id INTEGER PRIMARY KEY, 
                                name TEXT,
                                age INTEGER,
                                breed TEXT)
            ''')
```
    <sqlite3.Cursor at 0x103083ab0>
    
## Populating Tables 
- `INSERT INTO` command to populate a table
- followed by `VALUES` keyword accompanied by a parentheses with values enclosed that correspond to each column name. 

Important: You don't have to specify the "id" column name or value because the `PRIMARY KEY` columns are auto-incrementing. An id will automatically generate once you input new data. 

### `INSERT INTO`
```python
c.execute('''INSERT INTO cats (name, age, breed)
            VALUES ('Hodor', 4, 'Russian Blue');
        ''')
```
    <sqlite3.Cursor at 0x103083ab0>
