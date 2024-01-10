# Database Eloquent One to One Relationship CRUD


```php
Route::get('/insert',function(){
    $user = User::findOrFail(1);

    $address = new Address(['name'=>'12345 San Antonio Ave Secret 12234']);

    $user->address()->save($address);
});
```
- Insert address to the database using eloquent but if you don't have any user that will be asssigned with this address, the data will not be inserted.


### Find and update.

```php 
Route::get('/update', function(){

    $address = Address::where('user_id', 1)->first();

    $address->name = "Updated ave 123434423, Alaskaa";

    $address->save();
});
```

- finding the user_id that is equals to 1 then update the address on the particular user.


### Reading the Data.


```php
Route::get('/read',function(){
    $user = User::findOrFail(1);

    echo $user->address->name;
});
```
- Display the user's address specifically.

### Update
```php
Route::get('/update', function(){

    $address = Address::where('user_id', 1)->first();

    $address->name = "Updated ave 123434423, Alaskaa";

    $address->save();
});
```

- Update the the address of the user by finding the user first override the new data to replace the old data in the database.


### Delete
```php
Route::get('/delete',function(){
    $user = User::findOrFail(2);

    $user-> address -> delete();

    return 'done';
});
```
- find the a user by its id and delete the address.