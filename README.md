# Data_Admin_101

# Objectives
- Create a SQL database 
- Create a SQL table 
- Create rows in a SQL table 
- Alter entries 
- Delete entries 
- Commit changes using SQLite3

## Working Directory - Previewing Files
In bash, you can use `ls` command to preview files and folders in the current working directory. 

```python
ls
```

    Data_admin_101.ipynb       README.md 

## Creating a Database
creating a database is as easy as connecting a database to non-existing database. 

```python
import sqlite3

conn = sqlite3.connect('pets.db')
c = conn.cursor()
```

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
    
## Altering a Table 
You can update a table using this general patter: 
`ALTER TABLE table_name ADD COLUMN column_name column_type;`

## Updating data
The `UPDATE` keyword is used to change preexisting rows within a table. 

A boilerplate `UPDATE` statement looks like below:
```python
c.execute('''UPDATE [table_name]
            SET [column_name] = [new_value]
            WHERE [column_name] = [value]
        ''')
 ```
 ### Example: 
 ```python
 c.execute('''UPDATE cats
            SET name = 'Hana'
            WHERE name = 'Hannah';
        ''')
 ```
 ## Deleting Data
A boiler plate of a `DELETE` statement looks like this: 
```python
c.execute('''DELETE FROM [table_name] WHERE [column_name] = [value];''')

c.execute('''DELETE FROM cats WHERE id = 2;''')
```
    <sqlite3.Cursor at 0x103083ab0>
    
## Saving Changes
Changes need to be saved if you are planning to connect the database from another jupyter notebook. You have to commit changes to the master database so that other users and connections can also view the updates. 
```python
# preview the table 
c.execute('''SELECT * FROM cats;''').fetchall()
```
    [(1, 'Hodor', 4, 'Russian Blue')]
    
To demonstrate these changes aren't reflected to other connections, create a second connection/cursor and try it out. 
```python 
#Preview the table via a second current cursor/connection 
#Don't overwrite the previous connection: you'll lose all of your work!
conn2 = sqlite3.connect('pets.db')
cur2 = conn2.cursor()
cur2.execute("""SELECT * FROM cats;""").fetchall()
```
    []
    
The second connection doesn't dipslay the data or even read the `cats` table we created. To make changes universally accessible, you must commit the changes. 

`conn.commit()`

Now, try to reload the second connection. The updates should populate the table.
```python 
#Preview the table via a reloaded second current cursor/connection 
conn2 = sqlite3.connect('pets.db')
cur2 = conn2.cursor()
cur2.execute("""SELECT * FROM cats;""").fetchall()
```
    [(1, 'Hodor', 4, 'Russian Blue')]
    
Voila! You've created, edited and deleted tables and databases using SQL! 
