# Laravel Fundamentals Database Eloquent Relationships

### One to One ralationship
- it is a one way relationship, for example "A man has only one wife." that is one to one replationship


```code
  public function post(){
        return $this->hasOne('App\Models\Post');
    }

```
- this code indicate that this particular user has one post.

```code
Route::get('/user/{id}/post/',function($id){
      return  User::find($id)->post;
});
```
- this will be the route gets the id params to get the particular post.

### One to one replationship Inverse
- it is a relations that show and post that belongs to a user.

```code 
  public function user(): BelongsTo
    {
        return $this->belongsTo(User::class);
    }
```
- this block of code should be inserted to the Post model to show that this particular post belongs to the this user.


```code 
Route::get('/post/{id}/user',function($id){

    return Post::find($id)->user;
});

```
- this block of code is the route where you can access the user who owns the post.


### One is to Many Relationship

- One is to many realtionship when you have single model as a parent of more child models.

```code
 public function posts(): HasMany 
    {
        return $this->hasMany(Post::class);
    }
```
- this block of code should be inserted to the User model to show that this particular user has many posts.

```code
Route::get('/posts',function(){
     $user = User::find(1);
     $userPosts = $user->posts;
     foreach($userPosts as $post){
        echo $post->title.'<br>';
     }
});
```
- This route is iterates the found posts in a particular user.


### Many to Many Relationship

- One is to many realtionship when you have single model as a parent of more child models.

```code
Route::get('/user/{id}/role',function($id){
    
    $user = User::find($id);

    foreach($user->roles as $role){
        return $role->name;
    }
});

```

### Has many through relationship
- relationship provides a convenient way to access distant relations via an intermediate relation


```code
 public function posts(): HasManyThrough
    {
        return $this->hasManyThrough(Post::class, User::class,'country_id');
    }
```
- code in the post model that gets data from other models.


```code
Route::get('/user/country', function(){
   $country = Country::find(1);

   foreach($country->posts as $post){
    return $post->title;
   }
});
```
- this the route that gets the country id and iterate the post that belongs to that country.


### Polymorphic relationship
- allow a model to be loaned to more that one other made on asingle association.

```code
class Photo extends Model
{
    use HasFactory;

    public function imageable(): MorphTo
    {
        return $this->morphTo();
    }
}
```

```code
class Post extends Model
{
   
    use HasFactory;


   

    public function photos(): MorphMany
    {
        return $this->morphMany(Photo::class,'imageable');
    }

}
```

```code
public function photos(): MorphMany
{
    return $this->morphMany(Photo::class,'imageable');
}

```
 
### Polymorphic relationship the inverse
- shows how to pull the user owner of the image.
```code
Route::get('photo/{id}/post',function($id){
   $photo = Photo::findOrFail($id);

   return $photo->imageable;
});

```
### Polymorphic relation many to many 
- sharing a single list of unique records among the rest of the tables

```code
 public function posts()
    {
        return $this->morphedByMany(Post::class,'taggable');
    }

    public function videos()
    {
        return $this->morphedByMany(Video::class,'taggable');
    }
```

```code
public function photos(): MorphMany
{
    return $this->morphMany(Photo::class,'imageable');
}
```


### Polymorphic relation many to many retrieving
- To handle polymorphic many-to-many relationships in Laravel, you can use the Eloquent ORM. Define relationships in your models.


```code

class Post extends Model
{
    public function tags()
    {
        return $this->morphToMany(Tag::class, 'taggable');
    }
}


// Tag.php
class Tag extends Model
{
    public function posts()
    {
        return $this->morphedByMany(Post::class, 'taggable');
    }
}


// Taggable.php
class Taggable extends Model
{
    // This model is used as an intermediate table
    // Make sure to have tag_id, taggable_id, and taggable_type columns
}


$postId = 1; // Replace with the actual post ID

$post = Post::find($postId);
$tags = $post->tags;

// Now $tags contains the tags associated with the post


php artisan migrate




```


### Polymorphic relation many to many retrieving 

- polymorphic relationships enable a model to be associated with multiple types of another model in a many-to-many connection. To find the owner in a polymorphic many-to-many relationship, you can utilize the morphToMany relationship along with the wherePivot method to conveniently access the associated models and their types.

```code
// Post.php
class Post extends Model
{
    public function tags()
    {
        return $this->morphToMany(Tag::class, 'taggable')->withTimestamps();
    }
}

// Tag.php
class Tag extends Model
{
    public function posts()
    {
        return $this->morphedByMany(Post::class, 'taggable')->withTimestamps();
    }
}


$tag = Tag::find($tagId);

// Get all posts associated with the tag
$posts = $tag->posts;

// Get the type of the owner in the first post
$ownerType = $tag->posts()->first()->pivot->taggable_type;


```