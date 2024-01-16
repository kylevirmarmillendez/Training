# Database Eloquent One to Many Relationship CRUD



```php
    public function up(): void
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->integer('user_id')->unsigned()->nullable()->index();
            $table->string('title');
            $table->text('body');
            $table->timestamps();
        });
    }

```

- Configuration of the posts migration ot the posts table in the database.

<br>
<br>


```php
 public function post(): HasMany
    {
        return $this->hasMany(Post::class);
    }
```
- This code is inside the user model. This means that this particular user can make many posts.

<br>
<br>

```php
   protected $fillable = [

        'title',
        'body'
    ];
```

- This code is located inside the Post Model. This code will inform laravel that title and body are available to be filled with datas.


<br>
<br>

### Create
```php
Route::get('/create', function(){
        $user = User::findOrFail(1);

        $post = new Post(['title'=>'My Post by kyle Millendez','body'=>'Kang Kong chips by Josh Mojica']);

        $user->post()->save($post);

    });
```

- To create a post under a user is to find the user and create an instance that stores the data to be inserted.laslty, save the post.


### Read

```php
Route::get('/read', function(){
        $user = User::findOrFail(1);

    
       $posts = $user->posts;

       foreach($posts as $post){
        echo $post->title;
        echo '<br>';
       }
});
```
- To read the post by a user, you need to get the find the user and get posts and since it is HasMany so it will be stored inside an array. For you to display all the data inside the array you need use foreach to iterate the data.


### Update
```php
Route::get('/update',function(){
    $user = User::findOrFail(1);
    $user->posts()->where('id',1)->update(['title'=>'I Love Laravel','body'=>"this is Awesome"]);
});
```

- To update, you also to find the a user and get navigate the posts inside the users table where id = 1 then update the content.


### Delete

```php 
    Route::get('/delete',function(){
        $user = User::find(1);
        $user->posts()->where('id', 1)->delete();
});
```

- To delete to find the user then navigate to the post inside the user where id = 1 the delete the data.
 


