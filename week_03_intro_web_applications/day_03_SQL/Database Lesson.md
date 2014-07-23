## Database Lesson 

###Objectives

1. Define what databases are
2. Explain how to create databases
3. Design a simple schema
4. CRUD on a DB 
5. Run more complex queries on a DB
6. Understand relationships
7. Understand how to join two tables

First make sure everyone has psql running -> connect using postgres app 

### Backup and talk about last lesson

How were we storing data? We used an array, why was this nice, why wasn't it?
What's a database?
What do we store in it?
Talk about data types (include serial, integer, varchar, text, boolean, date)

Awesome so we know what a db does, what we store and what data types are - let's try to visualize what that might look like and then well do an example and then code it and explain how this connects to previous lessons

1st example - instructors table (just an id and first_name)

VISUALIZE - Compare to an excel sheet, draw rows, columns (actually make this!)

EXAMPLE - Move to talk about relationships between tables and a explain what a schema is.

CODE - Alright nice! We have this in our head let's talk about how we actually code this

Then - talk about some pitfalls with SQL + Postgres 

- Semicolons and apostrophes
- Single quotes vs double quotes
- Best practices for table naming

- Now let's get coding
	+ create a db -> create database learnsql
	+ move to that db -> \c or \connect dbname
	+ show all the databases we have \list
	+ create a table -> CREATE TABLE Instructors(instructor_id serial primary key, first_name varchar(10)); 
	+ Forget the semicolon and show what happens when you miss one
	+ insert my name -> INSERT INTO Instructors (first_name) VALUES ('Ellie');
	+ select it -> SELECT * FROM Instructors;
	+ update it -> UPDATE Instructors SET first_name = 'Elie' WHERE first_name = 'Ellie';
	+ forget it, let's just delete me -> DELETE FROM Instructors WHERE first_name = 'Elie'

We just did CRUD on our DB, map the SQL verbs 

1. Insert = create INSERT INTO ____ (fields) VALUES (values);
2. Select = read SELECT * FROM table;
3. Update = update UPDATE table SET field = newvalue where field = oldvalue
4. Delete = delete DELETE FROM table 

NOW ITS YOUR TURN (DO THIS IN PAIRS)
- do example -> follow our example - create a db, add a table,

- Using the db learnsql:
	1. Create a table Students with an ID and first_name
	2. Insert your name
	3. Select everything from the table
	4. Update your name with your full name
	5. Delete it
	6. Add the name of your partner in your DB

Let's dive deeper into select - how do we get more specific?

- Now you should have more than 1 student in your DB
- How can we select just one student? 
	- What about ordering? ASC/DESC
	- Counting the total amount?	

- WHERE - SELECT * FROM instructors WHERE first_name = 'Anil';
- BETWEEN - SELECT * FROM instructors WHERE instructor_id BETWEEN 3 AND 5;
- ORDER BY - SELECT * FROM instructors ORDER BY first_name DESC;
- LIKE - SELECT * FROM instructors WHERE first_name LIKE '%i%';
- COUNT - SELECT COUNT(*) FROM instructors;
- MIN/MAX - SELECT MIN(instructor_id) FROM instructors;
- LIMIT + OFFSET - SELECT * FROM instructors LIMIT 1 OFFSET 1;

###Relationships

What if we want to include the courses that the students are taking? How would we go about this? Ask why we can't just include that in the students table and talk very briefly about normalization

### Let's build a shopping database with orders table (think Amazon):
- Two tables -> Orders and items
- One order has many items (known as a one to many relationship)
	- Create an orders table
		- id
		- shipping method
	- Create an items table	
		- id
		- category
		- description
		- order_id
	- I want to now combine these two tabels together!
	- How do we model this relationship?
	- JOINS
		
## Let's think about constraints a bit more

- Now we want to enforce our data a bit better, the parent table should not be able to be deleted - this is a principal called data integrity
- We need a foreign key (goes in one table and is almost always the primary key of another table) 

## TO SEE OUR CONSTRAINTS
- SELECT * FROM information_schema.table_constraints where table_schema = 'public';

## TO MAKE A COLUMN UNIQUE
- ALTER TABLE owners ADD CONSTRAINT one_name_only UNIQUE (name);


## Foreign KEY
A foreign key enforces the consistency of data that points elsewhere. It ensures that the data which is pointed to actually exists. In a typical parent-child relationship, a foreign key ensures that every child always points at a parent and that the parent actually exists. Without the foreign key you could have "orphaned" children that point at a parent that doesn't exist.

- Add our FK
	- What is it? What does it do?
	- Do we need it?
		- Which table will we be able to drop and which one won't we? Parent can not be dropped 

## TO ADD A FK
ALTER TABLE items ADD CONSTRAINT owner_fk FOREIGN KEY (order_id) REFERENCES orders (order_id) ON DELETE NO ACTION;

Then, run drop table orders;
