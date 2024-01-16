# Database - Eloquent Polymorphic Many to Many

### Migration Setup

*Post Table*

```php
  public function up(): void
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }
```
<br>
<br>

*Videos Table*

```php
 public function up(): void
    {
        Schema::create('videos', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }
```

<br>
<br>

*Tags Table*

```php
   public function up(): void
    {
        Schema::create('tags', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }
```

<br>
<br>

*Taggables Table*
```php
 public function up(): void
    {
        Schema::create('taggables', function (Blueprint $table) {
            $table->id();
            $table->integer('tag_id');
            $table->integer('taggable_id');
            $table->integer('taggable_type');
            $table->timestamps();
        });
    }

```





### Model Setup


*Post Model*
```php
    protected $fillable = ['name'];
```
- This indicates that the this particular field is fillable.
<br>
<br>

*Tag Model*
```php
    protected $fillable = ['name'];
```
- This also indicates that the this particular field is fillable.

<br>
<br>


*Taggable Model*
```php
 public function tags()
    {
        return $this->morphMany(Tag::class,'taggable'); 
    }
```
- this block of code indicates that

### Inserting Data

```php
Route::get('/create', function(){

        $post = Post::create(['name'=>'My first post']);   
        $tag1 = Tag::find(1);
        $post->tags()->save($tag1);
        $video = Video::create(['name'=>'video.mov']);  
        $tag2 = Tag::find(2);
        $video->tags()->save($tag2);
});
```

- Inserting to 1 Post with a tag and 1 video also with it's tag.

### Read Data

```php
Route::get('/read',function(){
    $post = Post::findOrFail(1);

    foreach($post->tags as $tag){
        echo $tag;
    }
});
```
- Read all the tags in a particular post.

### Update Data
```php
Route::get('/update',function(){
    $post = Post::findOrFail(1);

    foreach($post->tags as $tag){
        $tag->where('name','PHP')->update(['name'=>'Updated PHP']);
    }
});

```
- Update the tag in a particular post.


### Delete Data

```php
Route::get('/delete',function(){

    $post = Post::findOrFail(1);

    
    foreach($post->tags as $tag){
        $tag->where('id',1)->delete();
    }
});
```

- Deleting tags from posts.
