# Database Basics 

## Learning Goals

- Describe how relational databases store data in tables composed of columns and rows
- Use lower case and snake_case conventions for column names
- Use the `CREATE TABLE` keywords to create a new table with columns, including the `id` column
- Use the `.help` command to get a complete list of SQL commands
- Use the `.tables` command to list all the tables in a database
- Use the `.schema` command to look at the structure of a database
- Use the `ALTER TABLE` keywords to add columns to a table
- Use the `DROP TABLE` keywords to delete a table

## Introduction

We'll cover how to create and delete database tables in SQLite as well as how to
add columns to an existing table.  

## Database Structure

Relational Databases like SQLite store data in a structure we refer to as a
table. You can think of a table in a database a lot like you would a
spreadsheet. We define specific columns in our table, and then we store any
number of what we refer to as 'records' as rows in our database. A record is
just information referring to one specific entity. For instance, if you had a
table called "People" you could imagine a structure like this:

<table border="1" cellpadding="4" cellspacing="0">
  <tr>
    <th>name</th>
    <th>age</th>
    <th>email</th>
  </tr>

  <tr>
    <td>Bob</td>
    <td>29</td>
    <td>bob@flatironschool.com</td>
  </tr>
  <tr>
    <td>Avi</td>
    <td>28</td>
    <td>avi@flatironschool.com</td>
  </tr>
  <tr>
    <td>Adam</td>
    <td>28</td>
    <td>adam@flatironschool.com</td>
  </tr>
</table>

Each column has a name, and each row contains the corresponding information
about a person.

### Note on Column Names

When we name columns in our database, there are a couple of conventions we will
follow. The first is that we will always use lowercase letters when referring to
columns in our database. SQLite isn't case sensitive about its commands or
column names, but it is generally best practice for us to stick to lowercase for
our column names.

The second convention we want to follow is more important. That is, when we have
multiple words in a column name, we link them together using underscores rather
than spaces. We call this convention "snake_case". So, for instance, if we
wanted to be more specific with our email column above, we can name it
email\_address. If we wanted to split up name to first and last we might have
columns called first\_name and last\_name.

## Database Tables

In the following sections, we'll cover how to create, alter, and delete database
tables. This reading is accompanied by a code along exercise that you can do in
your terminal. You don't need to fork this repository, and there are no tests to
pass. Follow along with the reading and code along instructions.

### Create Table

When we create a new database, it comes like a sort of blank slate. We can then
create a table inside our database using the following statement:

```sql
CREATE TABLE table_name;
```

But before we're able to store any actual data in a table, we'll need to define
the columns in the table as well as the specific type of data each column will
store.

Let's give it a shot. For the purposes of this code along, you'll be typing
these commands into your terminal.

### Code Along I: Creating a Table

* In the terminal let's create our new database and start sqlite3 by running the
  following:

```sql
sqlite3 pet_database.db
```

* Now, at our sqlite prompt, let's create our table:

```bash
CREATE TABLE cats;
```

You should see the following error:

```sql
Error: near ";": syntax error
```

SQLite expects us to include at least some definition of the structure of this
table as well. In other words, when we create database tables, we need to
specify some column names, along with the type of data we are planning to store
in each column. More on data types later.

Let's try that table statement again:

```sql
CREATE TABLE cats (
  id INTEGER PRIMARY KEY,
  name TEXT,
  age INTEGER
);
```

Let's break down the above code:

1. Use the `CREATE TABLE` command to create a new table called "cats".
2. Include a list of column names along with the type of data they will be
   storing. `TEXT` means we'll be storing plain old text, `INTEGER` means we'll
   store a number. Note that the use of capitalization is arbitrary, but it is a
   convention to help separate the SQL commands from the names we make up for
   our tables and columns.
3. Every table we create, regardless of the other column names and data types,
   should be defined with an id INTEGER PRIMARY KEY column, including the
   integer data type and primary key designation. Our SQLite database tables
   *must be indexed by a number*. We want each row in our table to have a
   number, which we'll call "id", just like in an Excel spreadsheet. Numbering
   our table rows makes our data that much easier to access, update, and
   organize. SQLite comes with a data type designation called "Primary Key".
   Primary keys are unique and auto-incrementing, meaning they start at 1 and
   each new row automatically gets assigned the next numeric value.

Okay, let's check and make sure that we successfully created that table. To do
this we'll be using SQL commands. To get a complete list of commands, you can
type `.help` into the sqlite prompt.

![Sqlite help output](https://curriculum-content.s3.amazonaws.com/phase-3/database-basics/sqlite-help.png)

Woah, that's a lot. Don't worry too much about all of these different commands
right now. Just know that you can always use `.help` to check out the available
options.

Okay, let's check out our new table. To list all the tables in the database
we'll use the `.tables` command. Type it into the sqlite prompt and hit enter,
and you should see our `cats` table listed.

We can look at the structure, or "schema", of our database (i.e. the tables and
their columns + column data types) with the `.schema` command:

```sql
sqlite> .schema
CREATE TABLE cats (
  id INTEGER PRIMARY KEY,
  name TEXT,
  age INTEGER
);
```

Let's move on to altering our table.

### Alter Table

Let's say that, after creating a database and creating a table to live inside
that database, we decide we want to add or remove a column. We can do so with
the `ALTER TABLE` statement.

### Code Along II: Adding, Removing and Renaming Columns

* Let's say we want to add a new column, `breed`, to our `cats` table:

```sql
ALTER TABLE cats ADD COLUMN breed TEXT;
```

Let's check out our schema now:

```sql
sqlite> .schema
CREATE TABLE cats (
  id INTEGER PRIMARY KEY,
  name TEXT,
  age INTEGER,
  breed TEXT
);
```

Notice that the `ALTER` statement isn't here, but instead SQLite has updated our
original CREATE statement. The schema reflects the current structure of the
database, which is reflected as the CREATE statement necessary to create that
structure.

Unfortunately, altering a column name and/or deleting a column can be tricky in
SQLite3. There are workarounds, however. We're not going to get into that right
now, but you can explore the [documentation on this topic](https://www.sqlite.org/lang_altertable.html).

Fortunately, SQLite still supports most of what we'll need one way or another.
For now, if you need to change a column name, it's best to simply delete the
table and re-create it.

### Drop Table

Lastly, we'll discuss how to delete a table from a database with the `DROP
TABLE` statement.

### Code Along III: Deleting a Table

Deleting a table is very simple:

```sql
DROP TABLE cats;
```

And that's it! You can exit out of the sqlite prompt with the `.quit` command.

## Resources

- [SQL keywords](https://www.sqlite.org/lang_keywords.html)
