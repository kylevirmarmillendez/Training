# Laravel Fundamentals Raw SQL Queries

### Inserting Data
- Using MYSQL query "insert into" then indicate the table name and the values you want to input to the database.

```code
Route::get('/insert',function(){
    DB::insert('insert into posts(title, body) values(?,?)',['PHP with Laravel','Laravel is the best thing that has happen to php']);
});
```


### Reading Data
- Using MYSQL query "select * from" then indicate the table name and "where id = ?" then put the id [1]
- Since the result is array your need to iterate it to display.

```code
Route::get('/read',function(){
    $results = DB::select('select * from posts where id = ?',[1]);

   foreach($results as $result){
    return $result->title;
   }
});
```


### Updating Data
- Using MYSQL query "update (table name) set title = (insert the new data)" where id = 1 It means that if there is a data in the database that has an id equals to 1 then update the the title with new value.



```code
Route::get('/update', function(){
    $updated = DB::update('update posts set title = "update title no.2" where id = ?',[1]);

    return $updated."is now updated";
});
```
### Deleting Data
- Deleting data is where you get the id of the data from the posts table. If the data has the id, the data will deleted the particular data. 


```code
Route::get('/delete', function(){
  $deleted = DB::delete('delete from posts where id = ?',[3]);
  return $deleted;
});

```
