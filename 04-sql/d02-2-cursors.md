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

#### Cursor constructor

```java
SQLiteDatabase db = this.getReadableDatabase();
Cursor cursor = db.query(SHOPPING_LIST_TABLE_NAME, // a. table
                    SHOPPING_COLUMNS, // b. column names
                    null, // c. selections
                    null, // d. selections args
                    null, // e. group by
                    null, // f. having
                    null, // g. order by
                    null); // h. limit
return cursor;
```

#### Cursors are Objects from the Database

`Cursor` is the class which represents a 2 dimensional table of any database. When you try to retrieve some data using `SELECT` statement, then the database will first create a `CURSOR` object and return its reference to you.


## Using Cursors

The first step to using a Cursor is to obtain one. As we mentioned earlier, any query results are returned in a Cursor:

```java
Cursor cursor = db.query("tbl_countries",null, null, null, null, null, null);
```

At a high level, this syntax connects to and queries the `tbl-countries` data table in your database. We will go into more depth about connecting to and modifying a database in a later lesson.

For now, let's look at some of the helper methods the Cursor object gives us.

To get the number of results in the query:

```java
cursor.getCount()
```

To get the number of columns in the results:

```java
cursor.getColumnCount()
```

We can even get the names of the columns:

```java
cursor.getColumnNames()
```

Since our Cursor has a position, we need to move it to the beginning of the cursor if we want to iterate through the results. Then, we'll be able to use a while loop and `moveToNext` to make your way through the results.

`Get` methods include methods like the ones above and can be used to get individual column values from the position the pointer is currently referencing. The parameter these methods take is the column index, and you pass this as an integer:

```java
cursor.moveToFirst();
while (cursor.isAfterLast() == false) {
  Log.d(TAG,"DB result "+cursor.getString(0));
  cursor.moveToNext();
}
```

The last thing to remember is to always close your cursors when you're finished with them. This helps free up memory because an open cursor still has some connections remaining to the database object.

```java
cursor.close();
```

#### Listing all Rows Example

```java
SQLiteDatabase db;

  db = openOrCreateDatabase(
          "TestingData.db"
          , SQLiteDatabase.CREATE_IF_NECESSARY
          , null
  );
  db.setVersion(1);
  db.setLocale(Locale.getDefault());

  String[] countryNames = new String[]{"Cananda","USA","Mexico"};
  int[] populations = new int[]{35,318,125};
  // uncomment on first run
  /*db.execSQL("CREATE TABLE IF NOT EXISTS tbl_countries (country_name VARCHAR, population VARCHAR);");
  for (int i=0; i<countryNames.length;i++) {
      db.execSQL("INSERT INTO tbl_countries Values ('" + countryNames[i] + "', '"+ populations[i] + "');");
  }*/


  Cursor cursor = db.query("tbl_countries",
          null, null, null, null, null, null);

  Log.d(TAG,"Number of results: "+cursor.getCount());

  Log.d(TAG,"Number of columns: "+cursor.getColumnCount());

  Log.d(TAG, "Column names: " + Arrays.toString(cursor.getColumnNames()));

  cursor.moveToFirst();
  while (cursor.isAfterLast() == false) {
      Log.d(TAG, "DB result " + cursor.getString(0)+" "+cursor.getString(1));

      cursor.moveToNext();
  }

  cursor.close();
}
```
