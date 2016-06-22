## Introduction to Cursors

#### LEARNING OBJECTIVES
*After this lesson, you will be able to:*
- Describe the purpose of a Cursor
- Manipulate a Cursor

So far we've been introduced to what databases are and how to use SQL to access and manipulate the data. These are all key pieces of information, but how does it all fit into Android? In Android, whenever we query data from the database, it is given back to us in a special object called a Cursor.

#### What is a Cursor?

Data retrieved from the SQLite database in Android is always returned to us in a Cursor object. The Cursor gives us a way to access the data in an organized manner with many helper methods.

You can think of it similar to how we have arrays and ArrayLists - instead of containing the results in some raw data type we would manually work through, the Cursor object helps us to do all of this.

> **Like a Baws**: Make sure you set breakpoints _after_ a Cursor is used so you may debug to inspect the data type in depth.

#### Cursors are Objects from the Database

`Cursor` is the class which represents a 2 dimensional table of any database. When you try to retrieve some data using `SELECT` statement, then the database will first create a `CURSOR` object and return its reference to you.
