
## Simple Cursor Adapters

Just as the ArrayAdapter allows us to create a quick adapter for a simple collection (instead of using a more complicated ListAdapter), the SimpleCursorAdapter allows us to create a CursorAdapter with a single line of code. While this may not work for every situation, it is very useful for layouts that don't require too much customization.

> Open up the documentation for SimpleCursorAdapter http://developer.android.com/reference/android/widget/SimpleCursorAdapter.html

The constructor takes 6 parameters:
1) The current context
2) The layout to use
3) The cursor that contains the data
4) An array of strings that contains the column titles to take from the cursor
5) An array of ints that contains the id of the view item in the layout to assign to the corresponding cursor data value
6) An integer for flags

## SimpleCursorAdapter

Now we're going to try to display the name column in the listView using a SimpleCursorAdapter. Let's comment out the CursorAdapter we defined before, and start writing a SimpleCursorAdapter.

```java
//Create SimpleCursorAdapter
String[] columns = new String[]{ExampleSQLiteOpenHelper.COL_ITEM_NAME};
int[] viewNames = new int[]{android.R.id.text1};
CursorAdapter simpleCursorAdapter = new SimpleCursorAdapter(MainActivity.this,android.R.layout.simple_list_item_1,cursor,columns,viewNames,0);

//Set adapter
listView.setAdapter(simpleCursorAdapter);
```

## SimpleCursorAdapter

Let's change the SimpleCursorAdapter to use the custom layout we created earlier. Once again, we need to change the layout name, the columns we are retrieving the data from, and the view names where we are assigning data.

```java
//Create SimpleCursorAdapter
String[] columns = new String[]{ExampleSQLiteOpenHelper.COL_ITEM_NAME,ExampleSQLiteOpenHelper.COL_ITEM_DESCRIPTION};
int[] viewNames = new int[]{R.id.name_text_view,R.id.description_text_view};
CursorAdapter simpleCursorAdapter = new SimpleCursorAdapter(MainActivity.this,R.layout.list_item_layout,cursor,columns,viewNames,0);
```
