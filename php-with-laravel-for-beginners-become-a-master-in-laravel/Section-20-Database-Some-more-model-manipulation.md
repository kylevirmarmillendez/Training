# Database Some More Model Manipulation

**Dates**

```php
Route::get('/dates',function(){

        $date = new DateTime('+1 week');

        echo $date->format('m-d-Y');

        echo '<br>';

        echo Carbon::now()->addMonths(10)->diffForHumans();

        echo '<br>';

        echo Carbon::now()->subDays(5)->diffForHumans();

        echo '<br>';

        echo Carbon::now()->yesterday()->diffForHumans();

        echo '<br>';


    });
```
<br>
<br>

 **Accessors**

```php
public function getNameAttribute($value){
    return ucfirst($value);
}
```



 - it pulls data out from the database and manipulate the data


**Mutator**

 ```php
 public function setNameAttribute($value){
    $this->attributes['name']=strtoupper($value);
}
 ```

 - Mutates the data before sending it to the database.


 **Query Scope**
 ```php
   public function index()
    {
        $posts = Post::latest()->get();
        return view('posts.index',compact('posts'));
    }
 ```
 
 ```php
  public static function scopeLatest($query){
        return $query->orderBy('id','asc')->get();
    }
 ```