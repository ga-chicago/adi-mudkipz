## Building SQLite support in an Android app

* Identify what a helper class is
* Create a DatabaseHelper class to work with SQLite
* Describe the purpose of SQLiteOpenHelper and why we extend from it
* Insert data into tables with the SQLiteOpenHelper class

#### Helper Class

* Not quite a model; not quite a controller
* Helps out with one specific part of our code
* Useful for working with Databases or APIs

#### Create a Helper Class

* Create a new `DatabaseHelper` class
* Extend the `SQLiteOpenHelper` class
* Identify the errors that Android Studio throws

#### SQLiteOpenHelper

This class handles opening databases if they exist and creating them if they do not. To use, you have to create your own subclass of SQLiteOpenHelper (_extend_ from it). This class should override the `onCreate` and `onUpgrade` methods.

In it, we define two static member variables - the database's `name` and `version`.

We also need _override_ the constructor and call the `super` method. We will pass in the `context` argument, then the database name, then null, and finally the database version. `       super(context, DATABASE_NAME, null, DATABASE_VERSION);`

>> **Protip**: It's good to have the database's name in one place, at the top of the class, and the constructor is calling the superclass's constructor, using the database name and version we just defined:


#### DatabaseHelper Class

Let's take a look at what this looks like:

```java
public class DatabaseHelper extends SQLiteOpenHelper {
        // Define the database name and version
    public static final int DATABASE_VERSION = 1;
    public static final String DATABASE_NAME = "Favorites.db";

        // override the SQLiteDatabase's constructor, onCreate, and onUpgrade
    public DatabaseHelper (Context context) {
        super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }

    public void onCreate(SQLiteDatabase db) {
      // when our db is created...
    }

    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
      // when we migrate/upgrade our database...
    }
}
```

#### onCreate & onUpgrade

- onCreate is called when the database helper is instantiated.
- onUpgrade is called when the database is migrated/upgraded.
- Create tables and insert initial/seed data in onCreate
- Drop tables, delete entries, then call onCreate in onUpgrade

#### Creating a table / dropping tables when upgrading

```java
public class DatabaseHelper extends SQLiteOpenHelper {
    public static final int DATABASE_VERSION = 1;
    public static final String DATABASE_NAME = "Favorites.db";

    // Define SQL statements to create and delete games table
    public static final String SQL_CREATE_GAME_TABLE = "CREATE TABLE games ( id INTEGER PRIMARY KEY, name TEXT, year TEXT )";

    public static final String SQL_DROP_GAME_TABLE = "DROP TABLE IF EXISTS games";

    public DatabaseHelper(Context context) {
        super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }

    // Create the games table when the database is created
    public void onCreate(SQLiteDatabase db) {
        db.execSQL(SQL_CREATE_ENTRIES);
    }

    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
      db.execSQL(SQL_DELETE_ENTRIES);
      onCreate(db);
    }
}
```

#### Insert into tables using ContentValues

- ContentValues is a Key/Value pair data structure for databases
- Similar to a HashMap

```java
public void insert(int id, String name, String year){
    // Get a reference to the database
    SQLiteDatabase db = getWritableDatabase();

    // create a new content value to store values
    ContentValues values = new ContentValues();
    values.put("id", id);
    values.put("name", name);
    values.put("year", year);

    // Insert the row into the games table
    db.insert("games", null, values);
}
```

#### Using in your Activity

Use this class from anywhere with access to a Context (i.e., an Activity):

```java
public class GameActivity extends Activity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);

        DatabaseHelper db = new DatabaseHelper(this);

				db.insert(1, "Super Mario", "1985");
				db.insert(2, "Legend of Zelda", "1986");

				Game retrievedGame = db.query(2);
    }
}
```


#### Additional Resources

- [Saving Data in SQL Databases (Android Developers)](http://developer.android.com/training/basics/data-storage/databases.html)
- [Android SQLite Database Tutorial](http://www.androidhive.info/2011/11/android-sqlite-database-tutorial/)
