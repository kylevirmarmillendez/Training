# Laravel Fundamentals Database Tinker

- Tinker will us interact with databases a lot better using eloquent. 

```php 
> $post = App\Models\Post::create(['title'=>'post from tinker','body'=
>'PHP content from tinker']);
= App\Models\Post {#7032
    title: "post from tinker",
    body: "PHP content from tinker",
    updated_at: "2024-01-08 02:00:49",
    created_at: "2024-01-08 02:00:49",
    id: 3,
  }
```
- This is how to insert data in tinker.


### Reading Information or Finding record using Tinker

```php
$post = App\Models\Post::find(6);

= App\Models\Post {#7267
    id: 6,
    title: "Yeah Baby",
    body: "Hello Baby",
    created_at: "2024-01-08 02:16:38",
    updated_at: "2024-01-08 02:16:38",
    is_Admin: 0,
    deleted_at: null,
  }
```

### Update and Delete data using tinker.


```php
 $post->delete();
```
- this method will delete the data but it will just move to trashed that is called soft delete.


```php
$post = App\Models\Post::onlyTrashed();
$post->forceDelete();
```
- enable for us to delete the data permanently, you need to consider the data inside the trashed before you delete those data by using forceDelete() Method.


