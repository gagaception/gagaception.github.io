James Coglan, a Developer at FutureLearn, explains a common problem with STI and how we refactored our Rails app to solve it.

Single-table inheritance (STI) is the practice of storing multiple types of values in the same table, where each record includes a field indicating its type, and the table includes a column for every field of all the types it stores. In Rails, the type column is used to determine which type of model to instantiate for each row; a row with type = 'Article' will make Rails call Article.new when turning that row into an object.

A common problem with STI

A common problem with STI is that, over time, more types get added to that table, and it grows more and more columns, and the records in the table have less and less in common with one another. Each type of record uses some subset of the table’s columns, and none uses all of them, so you end up with a very sparsely populated table. Those types create costs for one another: when you query for articles, you must remember to filter out all the other types of values and to only select columns relevant to articles, or else pay a huge performance cost. You reproduce a lot of work the database would do for you, if you only had each data type in its own table.
