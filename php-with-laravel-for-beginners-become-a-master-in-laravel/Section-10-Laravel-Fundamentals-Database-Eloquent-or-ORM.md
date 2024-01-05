# Laravel Fundamentals Database - Eloquent/ORM

### Reading Data

- Reading data using the model is showing all the data inside the database.

```code
Route::get('/find',function(){
    $posts = Post::all();

    foreach($posts as $post){
        return $post->title;
    }
});
```

### Reading/Finding with Constraints

- Read a particular data where id is equal to 5, and chain with another method calle orderBy descending order then take 1 data and get the data

```code
Route::get('/findwhere',function(){

    $posts = Post::where('id',5)->orderBy('id','desc')->take(1)->get();
    return $posts;
});
```

### Inserting/Saving Data

- save the Post model as a variable
- override each data inside the "$post" then the data will be changed.

```code
Route::get('/basicinsert', function(){
    $post = new Post;
    $post->title = 'new ORM title insert';
    $post->body= 'Kyle is Real cool';

    $post->save();
});


Route::get('/basicinsert2', function(){
    $post = Post::find(3);
    $post->title = 'new ORM title override';
    $post->body= 'ORM makalibug';

    $post->save();
});
```

### Creating Data and Configuring mass Assigments
- Mass Assignment or Mass input is like you assign a string to variable.


```code
Route::get('/create', function(){
    Post::create(['title'=>'udate kyle gwapo', 'body'=>'I am so gwapo with marjorie']);
});


  protected $fillable = [
    'title',
    'body'
    ];

```

### Updating the Eloquent
- Updating a specific data using update() method.

```code
Route::get('/update',function(){
    Post::where('id','3')->where('is_Admin', 0)->update(['title'=>'New old title', 'body'=>'I love cebu sheyt']);
});

```


### Deleting Data
- Delete a particular data using detele() method by finding the id.

```code
Route::get('/delete', function(){
    $post = Post::find(3);

    $post->delete();
});
```


### Deleting a record pemanently
- Delete all files permanently.
```code
Route::get('/forcedelete',function(){
    Post::where('id',3)->forcedelete();
});
```




