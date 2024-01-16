# Application Comments Legacy Version 5.2 

I created 3 additional models with migrations:
- Post
- Comment
- Reply

 
<br>



**Post Model**
```php
     public function Post()
    {
        return $this->hasMany(Comment::class);
    }
```

**Comment Model**
```php
    public function comments()
    {
        return $this->belongsTo(Post::class);
    }

    public function replies()
    {
        return $this->hasMany(Reply::class);
    }
```

**Reply Model**
```php
    public function comment()
    {
        return $this->belongsTo(Comment::class);
    }
```


-  The Post has many Comment while the Comment belongs to a Post. The Comment has many reply while the Reply belongs to a Comment.
<br>
**Accessing the nested replationships**
```php
   public function index(){
        $posts =  Post::findOrfail(1);
        $comment = $posts->comments()->get()->first();
        $reply = $comment->replies[0];
        return dd($reply);
    }
```
