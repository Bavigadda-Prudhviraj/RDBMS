# Lecture 1: Introduction to DBMS and SQL

## Agenda

- What is a Database
- What, What Not, Why, How of Scaler SQL Curriculum
- Types of Databases
- Intro to Relational Databases
- Intro to Keys

## What is a Database

Okay, tell me, In your day to day life whenever you have a need to save some information, where do you save it? Especially when you may need to refer to it later, maybe something like your expenses for the month, or your todo or shopping list?

Correct! Many of us use softwares like Excel, Google Sheets, Notion, Notes app etc to keep a track of things that are important for us and we may need to refer to it in future. Everyone, be it humans or organizations, have need to store a lot of data that me useful for them later. Example, let's think about Scaler. At Scaler, we would want to keep track of all of your's attendance, assignments solved, codes written, coins, mentor session etc! We would also need to store details about instructors, mentors, TAs, batches, etc. And not to forget all of your's email, phone number, password. Now, where will we do this?

For now, forget that you know anything about databases. Imagine yourself to be a new programmer who just knows how to write code in a programming language. Where will you store data so that you are able to retrieve it later and process that?

Correct! You will store it in files. You will write code to read data from files, and write data to files. And you will write code to process that data. For example you may create separate CSV (comma separated values, you will understand as we proceed) files to store information about let's say students, instructors, batches. Eg:

```
students.csv
name, batch, psp, attendance, coins, rank
Naman, 1, 94, 100, 0, 1
Amit, 2, 81, 70, 400, 1
Aditya, 1, 31, 100, 100, 2
```

```instructors.csv
name, subjects, average_rating
Rachit, C++, 4.5
Rishabh, Java, 4.8
Aayush, C++, 4.9
```

```batches.csv
id, name, start_date, end_date
1, AUG 22 Intermediate, 2022-08-01, 2023-08-01
2, AUG 22 Beginner, 2022-08-01, 2023-08-01
```

Now, let's say you want to find out the average attendance of students in each batch. How will you do that? You will have to write code to read data from students.csv, and batches.csv, and then process it to find out the average attendance of students in each batch. Right? Do you think this will be very cumbersome?

### Issues with Files as a Database

1. Inefficient

While the above set of data is very small in size, let's think of actual Scaler scale. We have 2M+ users in our system. Imagine going through a file with 2M lines, reading each line, processing it to find your relevant information. Even a very simple task like finding the psp of a student named Naman will require you to open the file, read each line, check if the name is Naman, and then return the psp. Time complexity wise, this is O(N) and very slow.

2. Integrity

Is there anyone stopping you from putting a new line in `students.csv` as ```Naman, 1, Hello, 100, 0, 1``` . If you see that `Hello` that is unexpected. The psp can't be a string. But there is no one to validate and this can lead to very bad situations. This is known as data integrity issue, where the data is not as expected.

3. Concurrency

Later in the course, you will learn about multi-threading and multi-processing. It is possible for more than 1 people to query about the same data at the same time. Similarly, 2 people may update the same data at the same time. On save, whose version should you save? Imagine you give same Google Doc to 2 people and both make changes on the same line and send to you. Whose version will you consider to be correct? This is known as concurrency issue.

4. Security

Earlier we talked about storing password of users. Imagine them being stored on files. Anyone who has access to the file can see the password of all users. Also anyone who has access to the file can update it as well. THere is no authorization at user level. Eg: a particular person may be only allowed to read, not write. '

### What's a Database

Now let's get back to our main topic. What is a database? A database is nothing but a collection of related data. Example, Scaler will have a Database that stores information about our students, users, batches, classes, instructors, and everything else. Similarly, Facebook will have a database that stores information about all of it's users, their posts, comments, likes, etc. The above way of storing data into files was also nothing but a database, though not the easiest one to use and with a lot of issues.

### What's a Database Management System (DBMS)

A DBMS as the name suggests is a software system that allows to efficiently manage a database. A DBMS allows us to create, retrieve, update, and delete data (often also called CRUD operations). It also  allows to define rules to ensure data integrity, security, and concurrency. It also provides ways to query the data in the database efficiently. Eg: find all students with psp > 50, find all students in batch 1, find all students with rank 1 in their batch, etc. There are many database management systems, each with their tradeoffs. We will talk about the types of databases later today.

Now let me talk about how the curriculum is structured. We will be having 11 live classes, followed by a contest. In the live classes we are going to cover everything that is important for you for interviews as well as day to day job. Having said that, as I mentioned that Databases are  avery vast field, attached with every live class you will be able to see a set of recorded videos curated for you for extra learning you can gain. Those videos will mostly be around theoretical concepts behind databases that are not much asked in interviews much nor used at day to day job, but good to know. Sometimes these videos will be on solving extra problems for a particular SQL Topic. You can go through those videos if you want to gain deeper understanding but aren't mandatory to solve assignments or clear contest.

| S.No | Lecture Title |
| --- | --- |
| 1 | Introduction to Databases and SQL |
| 2 | CRUD |
| 3 | CRUD-2 and Joins |
| 4 | Joins - 2 |
| 5 | Aggregate and Subqueries |
| 6 | Indexes |
| 7 | Transactions |
| 8 | Schema Design - 1 |
| 9 | Schema Design - 2 |
| 10 | Views and Window Functions |
| CONTEST | - |

I hope this excites you for your learning journey in this module and I wish you are able to make the most out of it. 

## Types of Databases

Welcome back after the break. Hope you had a good rest and had some water, etc. Now let's start with the next topic for the day and discuss different types of databases that exist. Okay, tell me one thing, when you have to store some data, eg let's say you are an instructor at Scaler and want to keep a track of attendance and psp of every student of you, in what form will you store that?


Correct! Often one of the easiest and most intuitive way to store data can be in forms of tables. Example for the mentioned use case, I may create a table with 3 columns: name, attendance, psp and fill values for each of my students there. This is very intuitive and simple and is also how relational databases work.

### Relational Databases

Relational Databases allow you to represent a database as a collection of multiple related tables. Each table has a set of columns and rows. Each row represents a record and each column represents a field. Example, in the above case, I may have a table with 3 columns: name, attendance, psp and fill values for each of my students there. Let's learn some properties of relational databases.

1. Relational Databases represent a database as a collection of tables with each table storing information about something. This something can be an entity or a relationship between entities. Example: I may have a table called students to store information about students of my batch (an entity). Similarly I may have a table called student_batches to store information about which student is in which batch (a relationship betwen entities).
2. Every row is unique. This means that in a table, no 2 rows can have same values for all columns. Example: In the students table, no 2 students can have same name, attendance and psp. There will be something different for example we might also want to store their roll number to distingusih 2 students having the same name.
3. All of the values present in a column hold the same data type. Example: In the students table, the name column will have string values, attendance column will have integer values and psp column will have float values. It cannot happen that for some students psp is a String.
4. Values are atomic. What does atomic mean? What does the word `atom` mean to you?

Correct. Similarly, atomic means indivisible. So, in a relational database, every value in a column is indivisible. Example: If we have to store multiple phone numbers for a student, we cannot store them in a single column as a list. How to store those, we will learn in the end of the course when we do Schema Design. Having said that, there are some SQL databases that allow you to store list of values in a column. But that is not a part of SQL standard and is not supported by all databases. Even those that support, aren't most optimal with queries on such columns.

5. The columns sequence is not guaranteed. This is very important. SQL standard doesn't guarantee that the columns will be stored in the same sequence as you define them. So, if you have a table with 3 columns: name, attendance, psp, it is not guaranteed that the data will be stored in the same sequence. So it is recommended to not rely on the sequence of columns and always use column names while writing queries. While MySQL guaranteees that the order of columns shall be same as defined at time of creating table, it is not a part of SQL standard and hence not guaranteed by all databases and relying on order can cause issues if in future a new column is added in between.

6. The rows sequence is not guaranteed. Similar to columns, SQL doesn't guarantee the order in which rows shall be returned after any query. So, if you want to get rows in a particular order, you should always use `ORDER BY` clause in your query which we will learn about in the next class. So when you write an SQL query, don't assume that the first row will always be the same. The order of rows may change across multiple runs of same query. Having said that, MySQL does return rows in order of their primary key (we will learn about this later today), but again, don't rely on that as not guaranteed by SQL standard.
  
7. The name of every column is unique. This means that in a table, no 2 columns can have same name. Example: In the students table, I cannot have 2 columns with name `name`. This is because if I have to write a query to get the name of a student, I will have to write `SELECT name FROM students`. Now if there are 2 columns with name `name`, how will the database know which one to return? Hence, the name of every column is unique.


### Non-Relational Databases

Now that we have learnt about relational databases, let's talk about non-relational databases. Non-relational databases are those databases that don't follow the relational model. They don't store data in form of tables. Instead, they store data in form of documents, key-value pairs, graphs, etc. In the DBMS module, we will not be talking about them. We will talk about them in the HLD Module. 

In the DBMS module, our goal is to cover the working of relational databases and how to work with them, that is via SQL queries. 

## Keys in Relational Databases

Now we are moving to probably the most important foundational concept of Relational Databases: Keys. let's say you are working at Scaler and are maintaining a table of every students' details. Someone tells you to update the psp of Naman to 100. How will you do that? What can go wrong?

What if there are 2 Namans?
 
Correct. If there are 2 Namans, how will you know which one to update? This is where keys come into picture. Keys are used to uniquely identify a row in a table. There are 2 important types of keys: Primary Key and Foreign Key. There are also other types of keys like Super Key, Candidate Key etc. Let's learn about them one by one.

### Super Keys

To understand this, let's take an example of a students table at scaler with following columns.

| name | psp | email | batch | phone number |
| - | - |- | - | - |
|Naman | 1 | 94 | 100 | 0 | 1 |
|Amit |  2 | 81 |  70 | 400 | 1 |
|Aditya| 1| 31| 100| 100| 2 |

Which are the columns that can be used to uniquely identify a row in this table?

Let's start with name. How many of you think name can be used to uniquely identify a row in this table? 

Correct. Name is not a good idea to recognize a row. Why? Because there can be multiple students with same name. So, if we have to update the psp of a student, we cannot use name to uniquely identify the student. Email, phone number on the other hand are a great idea, assuming no 2 students have same email, or same phone number. 

Do you think the value of combination of columns (name, email) can uniquely identify a student? Do you think there will be only 1 student with a particular combination of name and email. Eg: will there be only 1 student like (Naman, naman@scaler.com)?

Correct, similarly do you think (name, phone number) can uniquely identify a student? What about (name, email, phone number)? What about (name, email, psp)? What about (email, psp)?

The answer to each of the above is Yes. Each of these can be considered a `Super Key`. A super key is a combination of columns whose values can uniquely identify a row in a table. What do you think are other such super keys in the students table?

In the above keys, did you ever feel something like "but this column was useless to uniquely identify a row.." ? Let's take example of (name, email, psp). Do you think psp is required to uniquely identify a row? Similarly, do you think name is required as you anyways have email right? 

Now let's remove the columns that weren't necessary. 

Also, let's say we were an offline school, and students don't have email or phone number. In that case what do you think schools use to uniquely identify a student? Eg: If we remove redundant columns from (name, email, psp), we will be left with (email). Similarly, if we remove redundant columns from (name, email, phone number), we will be left with (phone number) or (email). These are known as `candidate keys`. A candidate key is a super key from which no column can be removed and still have the property of uniquely identifying a row. If any more column is removed from a candidate key, it will no longer be able to uniquely identify a row. Let's take another example. Consider a table Scaler has for storing students's attendance for every class

| student_id | class_id | attendance |

What do you think are the candidate keys for this table? Do you think (student_id) is a candidate key? Will there be only 1 row with a particular student_id?

Is (class_id) a candidate key? Will there be only 1 row with a particular class_id?

Is (student_id, class_id) a candidate key? Will there be only 1 row with a particular combination of student_id and class_id?

Yes! (student_id, class_id) is a candidate key. If we remove any of the columns of this, the remanining part is not a candidate key. Eg: If we remove student_id, we will be left with (class_id). But there can be multiple rows with same class_id. Similarly, if we remove class_id, we will be left with (student_id). But there can be multiple rows with same student_id. Hence, (student_id, class_id) is a candidate key.

Is (student_id, class_id, attendance) a candidate key? Will there be only 1 row with a particular combination of student_id, class_id and attendance?

But can we remove any column from this and still have a candidate key? Eg: If we remove attendance, we will be left with (student_id, class_id). This is a candidate key. Hence, (student_id, class_id, attendance) is not a candidate key.

### Primary Key

We just learnt about super keys and candidate keys. Can 1 table have mulitiple candidate keys? Yes. The table earlier had both (email), (phone number) as candidate keys. A key in MySQL plays a very important role. Example, MySQL orders the data in disk by the key. Similarly, by default, it returns answers to queries ordered by key. Thus, it is important that there is only 1 key. And that is called `primary key`. A primary key is a candidate key that is chosen to be the key for the table. In the students table, we can choose (email) or (phone number) as the primary key. Let's choose (email) as the primary key.

Sometimes, we may have to or want to create a new column to be the primary key. Eg: If we have a students table with columns (name, email, phone number), we may have to create a new column called roll number or studentId to be the primary key. This may be because let's say a user can change their email or phone number. Something that is used to uniquely identify a row should ideally never change. Hence, we create a new column called roll number or studentId to be the primary key.

We will see later today on how MySQL allows to create primary keys etc. Before we go to foreign keys and composite keys, let's actually get our hands dirt with SQL. 

### Foreign Keys

Now let's get to the last topic of the day. Which is foreign keys. Let's say we have a table called batches which stores information about batchesat Scaler. It has columns (id, name, startDate, endDate). We would want to know for every student, which batch do they belong to. How can we do that?

Correct, We can add batchId column in students table. But how do we know which batch a student belongs to? How do we ensure that the batchId we are storing in the students table is a valid batchId? What if someone puts the value in batchID column as 4 but there is no batch with id 4 in batches table. We can set such kind of constraints using foreign keys. A foreign key is a column in a table that references a column in another table. It has nothing to do with primary, candidate, super keys. It can be any column in 1 table that refers to any column in other table. In our case, batchId is a foreign key in the students table that references the id column in the batches table. This ensures that the batchId we are storing in the students table is a valid batchId. If we try to insert any value in the batchID column of students table that isn't present in id column of batches table, it will fail. ANother example:

Let's say we have `years` table as:
`| id | year | number_of_days |`

and we have a table students as:
`| id | name | year |`

Is `year` column in students table a foreign key? 

The correct answer is yes. It is a foreign key that references the id column in years table. Again, foreign key has nothing to do with primary key, candidate key etc. It is just any column on one side that references another column on other side. Though often it doesn't make sense to have that and you just keep primary key of the other table as the foreign key. If not a primary key, it should be a column with unique constraint. Else, there will be ambiguities.

Okay, now let's think of what can go wrong with foreign keys?

Correct, let's say we have students and batches tables as follows:

| batch_id | batch_name |
|----------|------------|
| 1        | Batch A    |
| 2        | Batch B    |
| 3        | Batch C    |


| student_id | first_name | last_name | batch_id |
|------------|------------|-----------|----------|
| 1          | John       | Doe       | 1        |
| 2          | Jane       | Doe       | 1        |
| 3          | Jim        | Brown     | 2        |
| 4          | Jenny      | Smith     | 3        |
| 5          | Jack       | Johnson   | 2        |

Now let's say we delete the row with batch_id 2 from batches table. What will happen? Yes, the students Jim and Jack will be orphaned. They will be in the students table but there will be no batch with id 2. This is called orphaning. This is one of the problems with foreign keys. Another problem is that if we update the batch_id of a batch in batches table, it will not be updated in students table. Eg: If we update the batch_id of Batch A from 1 to 4, the students John and Jane will still have batch_id as 1. This is called inconsistency.

To fix for these, MySQL allows you to set ON DELETE constraints so that cascading deletes happen when such a delete happens. Implementation details will be discussed in the next set of classes.  

# Lecture 2: CRUD

## What is CRUD?

Hello Everyone  
Today we are going to start the journey of learning MySQL queries by learning about CRUD Operations. Okay tell me one thing. Let's say there is a table in which we are storing information about students. What all can we do in that table or its entries?

Correct. Primarily, on any entity stored in a table, there are 4 operations possible:

1. Create (or inserting a new entry)
2. Read (fetching some entries)
3. Update (updating information about an entry already stored)
4. Delete (deleting an entry)

Today we are going to discuss about these operations in detail. Understand that read queries can get a lot more complex, involving aggregate functions, subqueries etc, which we shall talk about in detail in later classes. So don't worry about that. Take today's class as an introduction to the world of MySQL queries.

We will be starting with learning about Create, then go to Read, then Update and finally Delete. So let's get started. For today's class as well as most of the classes ahead, we will be using Sakila database, which is an official sample database provided by MySQL. I hope you have downloaded and set that up on your machine already, following instructions shared in the earlier classes.

## Sakila Database Walkthrough

Let me give you all a brief idea about what Sakila database represents so that it is easy to relate to the conversations that we shall have around this over the coming weeks. Sakila database represents a digital video rental store, assume an old movie rental store before Netflix etc came. It's designed with functionality that would allow for all the operations of such a business, including transactions like renting films, managing inventory, and storing customer and staff information. Example: it has tables regarding films, actors, customers, staff, stores, payments etc. You shall get more familiar with this in the coming classes, don't worry!

## Create

### CREATE Query

First of all, what is SQL? SQL stands for Structured Query Language. It is a language used to interact with relational databases. It allows you to create tables, fetch data from them, update data, manage user permissions etc. Today we will just focus on creation of data. Remaining things will be covered over the coming classes. Why "Structured Query" bceause it allows to query over data arranged in a structured way. Eg: In Relational databases, data is structured into tables. 

A simple query to create a table in MySQL has:
  - column names
  - data type of column (integer, varchar, boolean, date, timestamp)
  - properties of column (unique, not null, default)

Similarily, the table could also have properties (primary key, key)

```sql
CREATE TABLE students (
    id INT AUTO_INCREMENT,
    firstName VARCHAR(50) NOT NULL,
    lastName VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    dateOfBirth DATE NOT NULL,
    enrollmentDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    psp DECIMAL(3, 2) CHECK (psp BETWEEN 0.00 AND 100.00),
    batchId INT,
    isActive BOOLEAN DEFAULT TRUE,
    PRIMARY KEY (id),
);
```

Here we are creating a table called students. Inside brackets, we mention the different columns that this table has. Alongwith each columns, we mention the data type of that column. Eg: firstName is of type VARCHAR(50). Please do watch the video on SQL Data Types attached to today's class to understand what VARCHAR, TIMESTAMP etc means. For our today's discussion, it suffices to know that these are different data types supported by MySQL. After the data type, we mention any constraints on that column. Eg: NOT NULL means that this column cannot be null. In tomorrow's class when we will learn how to insert data, if we try to not put a value of this column, we will get an error. UNIQUE means that this column cannot have duplicate values. If we insert a new row in a table, or update an existing row that leads to 2 rows having same value of this column, the query will fail and we will get an error. DEFAULT specifies that if no value is provided for this column, it will take the given value. Example, for enrollmentDate, it will take the value of current_timestamp, which the time when you are inserting the row. CHECK (psp BETWEEN 0.00 AND 100.00) means that the value of this column should be between 0.00 and 100.00. If some other value is put, the query will fail.


### INSERT Query

Now let's start with the first set of operation for the day: The Create Operation. As the name suggests, this operation is used to create new entries in a table. Let's say we want to add a new film to the database. How do we do that?

`INSERT` statement in MySQL is used to insert new entries in a table. Let's see how we can use it to insert a new film in the `film` table of Sakila database.

```sql
INSERT INTO film (title, description, release_year, language_id, rental_duration, rental_rate, length, replacement_cost, rating, special_features) 
VALUES ('The Dark Knight', 'Batman fights the Joker', 2008, 1, 3, 4.99, 152, 19.99, 'PG-13', 'Trailers'),
       ('The Dark Knight Rises', 'Batman fights Bane', 2012, 1, 3, 4.99, 165, 19.99, 'PG-13', 'Trailers'),
       ('The Dark Knight Returns', 'Batman fights Superman', 2016, 1, 3, 4.99, 152, 19.99, 'PG-13', 'Trailers');
```

Let's dive through the syntax of the query. First we have the `INSERT INTO` clause, which is used to specify the table in which we want to insert the new entry. Then we have the column names in the brackets, which are the columns in which we want to insert the values. Then we have the `VALUES` clause, which is used to specify the values that we want to insert in the columns. The values are specified in the same order as the columns are specified in the `INSERT INTO` clause. So the first value in the `VALUES` clause will be inserted in the first column specified in the `INSERT INTO` clause, and so on.

A few things to note here:

1. The column names is optional. If you don't specify the column names, then the values will be inserted in the columns in the order in which they were defined at the time of creating the table. Example: in the above query, if we don't specify the column names, then the values will be inserted in the order `film_id`, `title`, `description`, `release_year`, `language_id`, `original_language_id`, `rental_duration`, `rental_rate`, `length`, `replacement_cost`, `rating`, `special_features`, `last_update`. So the value `The Dark Knight` will be inserted in the `film_id` column, `Batman fights the Joker` will be inserted in the `title` column and so on.  
   - This is not a good practice, as it makes the query prone to errors. So always specify the column names. 
   - This makes writing queries tedious as while writing query you have to keep a track of what column was where. And even a small miss can lead to a big error. 
   - Also, if you don't specify the column names, then you have to specify values for all the columns. If you don't want to specify values for all the columns, then you have to specify the column names. Example: if you don't specify column names, then you have to specify values for all the columns, including `film_id`, `original_language_id` and `last_update`, which we may want to keep `NULL`.

Anyways, an example of a query without column names is as follows:

```sql
INSERT INTO film
VALUES (default, 'The Dark Knight', 'Batman fights the Joker', 2008, 1, NULL, 3, 4.99, 152, 19.99, 'PG-13', 'Trailers', default);
```

NULL is used to specify that the value of that column should be `NULL`, and `default` is used to specify that the value of that column should be the default value specified for that column. Example: `film_id` is an auto-increment column, so we don't need to specify its value. So we can specify `default` for that column, which will insert the next auto-increment value in that column.

So that's pretty much all that's there about Create operations. There is 1 more thing about insert, which is how to insert data from one table to another, but we will talk about that after talking about read. Any doubts till now? Via thumbs up/ down can you all let me know how many of you are 100% clear till here?

So seems like all doubts are clear. Before I start with read operations, let me have 2 small Quiz questions for you.

## Read

Now let's get to the most interest, and also maybe most important part of today's session: Read operations. . `SELECT` statement is used to read data from a table. Let's see how we can use it to read data via different queries on the `film` table of Sakila database. A basic select query is as follows:

```sql
SELECT * FROM film;
```

Here we are selecting all the columns from the `film` table. The `*` is used to select all the columns. This query will give you the value of each column in each row of the film table. If we want to select only specific columns, then we can specify the column names instead of `*`. Example:

```sql
SELECT title, description, release_year FROM film;
```

Here we are selecting only the `title`, `description` and `release_year` columns from the `film` table. Note that the column names are separated by commas. Also, the column names are case-insensitive, so `title` and `TITLE` are the same. Example following query would have also given the same result:

```sql
SELECT TITLE, DESCRIPTION, RELEASE_YEAR FROM film;
```

Now, let's learn some nuances around the `SELECT` statement.

### Selecting Distinct Values

Let's say we want to select all the distinct values of the `rating` column from the `film` table. How do we do that? We can use the `DISTINCT` keyword to select distinct values. Example:

```sql
SELECT DISTINCT rating FROM film;
```

This query will give you all the distinct values of the `rating` column from the `film` table. Note that the `DISTINCT` keyword, as all other keywords in MySQL, is case-insensitive, so `DISTINCT` and `distinct` are the same.

We can also use the `DISTINCT` keyword with multiple columns. Example:

```sql
SELECT DISTINCT rating, release_year FROM film;
```

This query will give you all the distinct values of the `rating` and `release_year` columns from the `film` table. Let's talk about how this works. A lot of SQL queries can be easily understood by relating them to basic for loops etc. Over this class, and the coming classes, I will relate every complex query with a corresponding pseudo code has you tried to do the same in a programming language. As all of you have already solved many DSA problems, this shall be much more easy and fun for you to learn. BTW: At the end, I will also share a final diagram that relates an SQL query to a corresponding pseudo code, with select, aggregate, group by, having, order by, limit, join, subquery, etc.

So, let's try to understand the above query with a pseudo code. The pseudo code for the above query would be as follows:

```python
answer = []

for each row in film:
    answer.append(row)

filtered_answer = []

for each row in answer:
    filtered_answer.append(row['rating'], row['release_year'])

unique_answer = set(filtered_answer)

return unique_answer
```

So what you see is that DISTINCT keyword on multiple column gives you for all of the rows in the table, the distinct value of pair of these columns.

### Select statement to print a constant value

Let's say we want to print a constant value in the output. Eg: The first program that almost every programmer writes: "Hello World". How do we do that? We can use the `SELECT` statement to print a constant value. Example:

```sql
SELECT 'Hello World';
```

That's it. No from, nothing. Just the value. You can also combine it with other columns. Example:

```sql
SELECT title, 'Hello World' FROM film;
```

### Operations on Columns

Let's say we want to select the `title` and `length` columns from the `film` table. If you see, the value of length is currently in minutes, but we want to select the length in hours instead of minutes. How do we do that? We can use the `SELECT` statement to perform operations on columns. Example:

```sql
SELECT title, length/60 FROM film;
```

Later in the course we will learn about Built In functions in SQL as well. You can use those functions as well to perform operations on columns. Example:

```sql
SELECT title, ROUND(length/60) FROM film;
```

ROUND function is used to round off a number to the nearest integer. So the above query will give you the title of the film, and the length of the film in hours, rounded off to the nearest integer.

### Inserting Data from Another Table

BTW, select can also be used to insert data in a table. Let's say we want to insert all the films from the `film` table into the `film_copy` table. We can combine the `SELECT` and `INSERT INTO` statements to do that. Example:

```sql
INSERT INTO film_copy (title, description, release_year, language_id, rental_duration, rental_rate, length, replacement_cost, rating, special_features)
SELECT title, description, release_year, language_id, rental_duration, rental_rate, length, replacement_cost, rating, special_features
FROM film;
```

Here we are using the `SELECT` statement to select all the columns from the `film` table, and then using the `INSERT INTO` statement to insert the selected data into the `film_copy` table. Note that the column names in the `INSERT INTO` clause and the `SELECT` clause are the same, and the values are inserted in the same order as the columns are specified in the `INSERT INTO` clause. So the first value in the `SELECT` clause will be inserted in the first column specified in the `INSERT INTO` clause, and so on.

Okay, let's take a pause to answer any doubts anyone may be having till now. For those who are absolutely clear can you please do a thumbs up in the chat. If any doubt, can you please do a thumbs down and post the doubt in chat.

Okay, let me also verify how well you have learnt till now with a few quiz questions.

Till now, we have been doing basic read operations. SELECT query with only FROM clause is rarely sufficient. Rarely do we want to return all rows. Often we need to have some kind of filtering logic etc. for the rows that should be returned. Let's learn how to do that.

### WHERE Clause

Let's say we want to select all the films from the `film` table which have a rating of `PG-13`. How do we do that? We can use the `WHERE` clause to filter rows based on a condition. Example:

```sql
SELECT * FROM film WHERE rating = 'PG-13';
```

Here we are using the `WHERE` clause to filter rows based on the condition that the value of the `rating` column should be `PG-13`. Note that the `WHERE` clause is always used after the `FROM` clause. In terms of pseudocode, you can think of where clause to work as follows:

```python
answer = []

for each row in film:
    if row.matches(conditions in where clause) # new line from above
        answer.append(row)

filtered_answer = []

for each row in answer:
    filtered_answer.append(row['rating'], row['release_year'])

unique_answer = set(filtered_answer) # assuming we also had DISTINCT

return unique_answer
```

If you seem where clause can be considered analgous to `if` in a programming language. With if as well there are many other operators that are used, right. Can you name which operators do we often use in programming languages with `if`?

> NOTE: Wait for students to give answer. Give hints to get AND, OR, NOT from them.

### AND, OR, NOT

Correct. We use things like `and` , `or`, `!` in programming languages to combine multiple conditions. Similarly, we can use `AND`, `OR`, `NOT` operators in SQL as well. Example: We want to get all the films from the `film` table which have a rating of `PG-13` and a release year of `2006`. We can use the `AND` operator to combine multiple conditions.

```sql
SELECT * FROM film WHERE rating = 'PG-13' AND release_year = 2006;
```

Similarly, we can use the `OR` operator to combine multiple conditions. Example: We want to get all the films from the `film` table which have a rating of `PG-13` or a release year of `2006`. We can use the `OR` operator to combine multiple conditions.

```sql
SELECT * FROM film WHERE rating = 'PG-13' OR release_year = 2006;
```

Similarly, we can use the `NOT` operator to negate a condition. Example: We want to get all the films from the `film` table which do not have a rating of `PG-13`. We can use the `NOT` operator to negate the condition.

```sql
SELECT * FROM film WHERE NOT rating = 'PG-13';
```

An advice on using these operators. If you are using multiple operators, it is always a good idea to use parentheses to make your query more readable. Else, it can be difficult to understand the order in which the operators will be evaluated. Example:

```sql
SELECT * FROM film WHERE rating = 'PG-13' OR release_year = 2006 AND rental_rate = 0.99;
```

Here, it is not clear whether the `AND` operator will be evaluated first or the `OR` operator. To make it clear, we can use parentheses. Example:

```sql
SELECT * FROM film WHERE rating = 'PG-13' OR (release_year = 2006 AND rental_rate = 0.99);
```

Till now, we have used only `=` for doing comparisons. Like traditional programming languages, MySQL also supports other comparison operators like `>`, `<`, `>=`, `<=`, `!=` etc. Just one special case, `!=` can also be written as `<>` in MySQL. Example:

```sql
SELECT * FROM film WHERE rating <> 'PG-13';
```

### IN Operator

With comparison operators, we can only compare a column with a single value. What if we want to compare a column with multiple values? For example, we want to get all the films from the `film` table which have a rating of `PG-13` or `R`. One way to do that can be to combine multiple consitions using `OR`.  A better way will be to use the `IN` operator to compare a column with multiple values. Example:

```sql
SELECT * FROM film WHERE rating IN ('PG-13', 'R');
```

Okay, now let's say we want to get those films that have ratings anything oter than the above 2. Any guesses how we may do that?

Correct! We had earlier discussed about `NOT`. You can also use `NOT` before `IN` to negate the condition. Example:

```sql
SELECT * FROM film WHERE rating NOT IN ('PG-13', 'R');
```

Think of IN to be like any other operator. Just that it allows comparison with multiple values.

Hope you had a good break. Let's continue with the session. In this second part of the session, we are going to start the discussion by discussing about another important keyword in SQL, `BETWEEN`.

### IS NULL Operator

Now we are almost at the end of the discussion about different operators. Do you all remember how we store emptiess, that is, no value for a particular column for a particular row? We store it as `NULL`. Interestingly working with NULLs is a bit tricky. We cannot use the `=` operator to compare a column with `NULL`. Example:

```sql
SELECT * FROM film WHERE description = NULL;
```

The above query will not return any rows. Why? Because `NULL` is not equal to `NULL`. Infact, `NULL` is not equal to anything. Nor is it not equal to anything. It is just `NULL`. 

Example:

```sql
SELECT NULL = NULL;
```

The above query will return `NULL`. Similarly, `3 = NULL` , `3 <> NULL` , `NULL <> NULL` will also return `NULL`. So, how do we compare a column with `NULL`? We use the `IS NULL` operator. Example:

```sql
SELECT * FROM film WHERE description IS NULL;
```

Similarly, we can use the `IS NOT NULL` operator to find all the rows where a particular column is not `NULL`. Example:

```sql
SELECT * FROM film WHERE description IS NOT NULL;
```

In many assignments, you will find that you will have to use the `IS NULL` and `IS NOT NULL` operators. Without them you will miss out on rows that had NULL values in them and get the wrong answer. Example:
find customers with id other than 2. If you use `=` operator, you will miss out on the customer with id `NULL`. Example:

```sql
SELECT * FROM customers WHERE id != 2;
```

The above query will not return the customer with id `NULL`. So, you will get the wrong answer. Instead, you should use the `IS NOT NULL` operator. Example:

```sql
SELECT * FROM customers WHERE id IS NOT NULL AND id != 2;
```

## Update

Now let's move to learn U of CRUD. Update and Delete are thankfully much simple, so don't worry, we will be able to breeze through it over the coming 20 mins. As the name suggests, this is used to update rows in a table. The general syntax is as follows:

```sql
UPDATE table_name SET column_name = value WHERE conditions;
```

Example:

```sql
UPDATE film SET release_year = 2006 WHERE id = 1;
```

The above query will update the `release_year` column of the row with `id` 1 in the `film` table to 2006. You can also update multiple columns at once. Example:

```sql
UPDATE film SET release_year = 2006, rating = 'PG' WHERE id = 1;
```

Let's talk about how update works. It works as follows:

```python
for each row in film:
    if row.matches(conditions in where clause)
        row['release_year'] = 2006
        row['rating'] = 'PG'
```

So basically update query iterates through all the rows in the table and updates the rows that match the conditions in the where clause. So, if you have a table with 1000 rows and you run an update query without a where clause, then all the 1000 rows will be updated. So, be careful while running update queries. Example:

```sql
UPDATE film SET release_year = 2006;
```

## Delete

Finally, we are at the end of CRUD. Let's talk about Delete operations. The general syntax is as follows:

```sql
DELETE FROM table_name WHERE conditions;
```

Example:

```sql
DELETE FROM film WHERE id = 1;
```

The above query will delete the row with `id` 1 from the `film` table. If you don't specify a where clause, then all the rows from the table will be deleted. Example:

```sql
DELETE FROM film;
```

Let's talk about how delete works as well in terms of code.

```python
for each row in film:
    if row.matches(conditions in where clause)
        delete row
```

