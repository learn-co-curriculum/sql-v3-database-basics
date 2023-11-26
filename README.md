# Database Basics

## Learning Goals

- Introduce database management system concepts.
- Introduce relational database structure.
- Introduce SQL statements.

## Introduction

Databases often contain massive amounts of data and support thousands
of simultaneous users, and thus must be managed with sophisticated software tools.


## Relational Database Management Systems

- **Data** is information that can be represented in many formats
  including numeric, textual, visual, or audio.
- A **database** is a collection of data in a structured format.
- A **database management systems** or **DBMS** is software that reads and writes data
  and often provides additional features including security, performance, transactions, multi-user access, and recovery. 
- A **relational database management system** or **RDBMS** stores data in tables, columns and rows.
  - A table holds information about objects of a similar type.
  - Each column within a table has a unique name.  A column may also be referred to as a field or attribute.
  - All values within a column have the same type and are atomic.
  - A row within a table represents a unique object or entity.  A row may also be referred to as a record.
  - Each table must define a unique identifier, called a **primary key**. 
    - The primary key consists of one or more columns.
    - Two rows can't contain the same set of values in their primary key column(s).
  - Rows among multiple tables can be related using **foreign keys**, in which one or more columns in
    one table store the values of the primary key of another table.
- A **query language** is a specialized programming language designed for database systems.
  - **Structured Query Language** or **SQL** is a query language designed for relational databases.
- **PostgreSQL** is a popular open source RDBMS.  Other RDMBS products include Oracle, MySQL, SQLite, and SQL Server.

## Relational Database Structure

A relational database stores data in a table that consists of
columns and rows.  Each row contains data about a unique
entity or object, such as a person, product, or event.
Each column stores a single atomic attribute
such as a person's date of birth, a product price, or a meeting date.

For example, assume we want a database to store information about
pets and their owners.  We will need one table to store data about
owners, and a separate table to store data about pets.
Our database model should specify the attributes
to store for each owner and each pet, along with the cardinality of the
relationship between owner and pet. We'll assume each pet has one owner,
while an owner may own many pets.   Thus, our `owner` and `pet` tables
need columns to store the following data:

- **owner**: unique identifier, first name, last name, and phone number.
- **pet**: unique identifier, name, species (cat, dog, etc), breed, age, and owner's unique identifier.

An **entity-relationship model** of `owner` and `pet` is shown below.  The relationship connecting
pet and owner indicates each pet has exactly one owner ( indicated by single line | ),
while an owner may have many pets ( indicated by three forked lines, also called "crows feet" ).
This type of relationship is called "one-to-many".

![pet er diagram](https://curriculum-content.s3.amazonaws.com/6036/database-basics/pet_erd.png)


Example database tables containing data for 3 owners and 9 pets could look like the following:

| owner table                                                                                      | pet  table                                                                                   |
|--------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| ![owner table](https://curriculum-content.s3.amazonaws.com/6036/database-basics/owner_table.png) | ![pet table](https://curriculum-content.s3.amazonaws.com/6036/database-basics/pet_table.png) |

Each table column has a name, which appears as the headings shown above the first row of data.
Each row contains the data about a specific owner or pet.

The first column in each table contains the unique identifier
called a **primary key**.  As each table row must be unique, every table 
should have a primary key.

The `owner_id` column in the `pet` table stores the relationship
between a pet and their owner, and represents something called a **foreign key**.
The `owner_id` value should contain an integer that corresponds to an `id` value
from one of the rows in the `owner` table.  For example, the dog named Wags
is owned by the owner with id 3, i.e. Dana Abcer.  **Foreign key** references
are what makes relational databases so powerful in terms of modeling
real-world entities and their complex relationships.

Imagine how we might connect the idea of a table
in SQL to a class in Java, and a record within a
table to an instance of a class.
For the `owner` table, the Java representation would be an `Owner` class such as the following:

```java
public class Owner {
    private int id;
    private String firstName;
    private String lastName;
    private String phone;
}
```

The Java representation of the `pet` table would be the `Pet` class shown below.  Note
that the owner is represented as a reference to an instance of the `Owner` class,
rather than an integer identifier as stored in the `pet` database table:

```java
public class Pet {
    private int id;
    private String name;
    private String species;
    private String breed;
    private int age;
    private Owner owner;
}
```

In a subsequent lesson we will see how to automatically map Java classes
and database tables, which is called **Object-Relational Mapping** or **ORM**.

## Structured Query Language

**SQL** is a popular query language used with most relational database systems.
SQL is a declarative language consisting of different types of statements
for managing data.  The statements are organized into several types,
each defined by a language subset of SQL:

- DDL – Data Definition Language
- DQL – Data Query Language
- DML – Data Manipulation Language
- DCL – Data Control Language
- TCL - Transaction Control Language

We will work primarily with DDL, DQL, and DML statements.

### DDL (Data Definition Language)

**Data Definition Language** or **DDL** statements define tables
and other structural and functional database objects.
We will primarily work with the following DDL statements:

- **CREATE** - create a database structural or functional object such as a table.
- **DROP** - delete a database object.
- **ALTER** - alter a database object.
- **RENAME** - rename a database object.

For example, we can create the owner table with the following SQL statement:

```sql
CREATE TABLE owner (
  id INTEGER PRIMARY KEY,
  first_name TEXT,
  last_name TEXT,
  phone TEXT
);
```

### DQL (Data Query Language) 

**Data Query Language** or **DQL** statements are used to perform queries on the data.
A query selects a subset of rows and/or columns in one or more tables, and may
perform various functions on the selected data. We will work with one DQL statement:

- **SELECT** - retrieve data from the database.

For example, the following SQL statement will retrieve all rows
from the `pet` table where the `species` column contains the value "cat".
The `*` means that every column should be displayed for each row retrieved:


```sql
SELECT *
FROM pet
WHERE species = 'cat';
```


### DML (Data Manipulation Language)

**Data Manipulation Language** or **DML** statements are used to manipulate
and control the data in a table.
We will primarily manipulate tables using the following DML statements:

- **INSERT** - insert a row into a table.
- **UPDATE** - update existing data within a table.
- **DELETE** - delete rows from a table.

For example, the following SQL statement will insert a new row
into the `owner` table:

```sql
INSERT INTO owner (id, first_name, last_name, phone)
VALUES (4, 'Rosario', 'Willow','800-555-0333');
```


## Conclusion

Relational database management systems store data in tables, columns and rows.
Each row represents a unique object identified
by a primary key.  Relationships between entities are stored in foreign keys.
Relational databases are powerful because they connect
data from different tables to create useful information.

SQL is a language specifically designed to create, manipulate, and query
relational database tables.  

## Resources

- [PostgreSQL](https://www.postgresql.org/)  
- [PostgreSQL SQL Statements](https://www.postgresql.org/docs/current/sql-commands.html)
