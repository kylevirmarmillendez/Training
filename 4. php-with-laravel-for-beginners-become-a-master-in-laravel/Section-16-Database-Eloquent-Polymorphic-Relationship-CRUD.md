# Database Eloquent Polymorphic Relationship CRUD


### Migration Setup

*Staff Migration Table*
```code 
   
    public function up(): void
    {
        Schema::create('staff', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }
```
-  The staff table has added a fillable string name.

<br>
<br>

*Products Migration Table*

```code
    public function up(): void
    {
        Schema::create('products', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->timestamps();
        });
    }
 ```
-  The products table has added a fillable string name.

<br>
<br>

*Photos Migration Table*

```code 
 public function up(): void
    {
        Schema::create('photos', function (Blueprint $table) {
            $table->id();
            $table->string('path');
            $table->integer('imageable_id');
            $table->string('imageable_type');
            $table->timestamps();
        });
    }
```
- The Photos table has a fillable string named path;


### Models Setup

*Staff model*
```code
 public function photos(){
        return $this->morphMany(Photo::class,'imageable');
    }
```

<br>
<br>

*Product Model*

```code 
 public function photos(){
        return $this->morphMany(Photo::class,'imageable');
    }
```

*Photo Model*
```code
  public function imageable(){
        return $this->morphTo();
    }
```

<br>



### Insert Data
```code
Route::get('/create', function(){
    $staff =  Staff::find(1);
    $staff->photos()->create(['path'=>'example.jpg']);
}); 
```
- inserting image path to the staff that has an id = 1.


<br>
<br>

### Reading Data

```php
Route::get('/read', function(){

    $staff = Staff::findOrFail(1);

    foreach($staff->photos as $photo){
        return $photo->path;
    }
});
```
- Reading all the photos inside a particular staff

<br>
<br>

### Updating Data
```php 
    Route::get('/update', function(){
    $staff = Staff::findOrFail(1);
    $photo = $staff->photos->where('id',1)->first();
    
    $photo->path = 'Update example.jpg';
    $photo->save();
});
```
- Updating the path where id = 1;

<br>
<br>

### Deleting Data

```php
Route::get('/delete', function(){
    $staff =Staff::findOrFail(1);
    $staff->photos()->where('id',1)->delete();

});
```

- Deleting 1 particular data that belongs to a staff.

