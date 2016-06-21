## Relationships

#### One to One
- not frequently used, but important to know it's an option
- both tables can have only one record on either side of the relationship; each primary key value relates to only one (or no) record in the related table
- imagine a Library table ```has_one``` location, and a location ```belongs_to``` a specific library - that lets us look up solely by location, and see the connected library
- often, in situations like that, you can make the location an attribute of the library, but when a location has, for example, multiple fields (address 1, address 2, state, zip, etc.), it might make sense to create another table for addresses and set up a ```has_one``` relationship

#### One to Many
- the most common type of database relationship
- the primary key table contains only one record that relates to none, one, or many records in the related table
- an author ```has_many``` books, but a book ```belongs_to``` only one author

#### Many to Many
- also very frequent
- each record in both tables can relate to any number of records (or no records) in the other table.
- a book probably "has many" categories, and a category also probably "has many" books

##### Notes

Keep in mind, the ```belongs_to``` part always goes on the opposite side of the ```has_many``` or ```has_one```. And the way it's stored is that the ID of the model that "has" something is stored in a field on the child, like "customer_id" or "author_id".  In our example with authors and books, the Book model ```belongs_to``` the Author model, while the Author, as mentioned, ```has_many``` books.
