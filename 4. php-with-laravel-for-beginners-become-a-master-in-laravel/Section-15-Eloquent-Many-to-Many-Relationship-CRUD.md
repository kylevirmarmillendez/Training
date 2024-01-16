# Database Eloquent Many to Many Relationship CRUD

### Inserting Data

```php
Route::get('/create',function(){
    $user = User::findOrFail(1);
    $role =  new Role(['name'=>'Author']);

    $user->roles()->save($role);
    });

```
- Setting a role to the user.

<br>
<br>

### Reading Data

```php
Route::get('/read',function(){

    $user =  User::findOrFail(1);

    // dd($user->roles->first()->name);

    foreach($user->roles as $role){
        return dd($role);
    }
});
```
- This block of code shows how to display roles under the users table.



<br>
<br>


### Updating Data
```php
Route::get('/update',function(){
    $user = User::findorFail(1);
    if($user->has('roles')){
        foreach($user->roles as $role){
            if($role->name == 'Administrator')
            {
                $role->name = 'administrator';
                $role->save();
            }
        }
    }
});
```
- Iterating the roles then there is conditional statement that if the role is equal to 'Administrator' it will change to 'administrator'.

<br>
<br>


### Deleting Data

```php
Route::get('/delete',function(){

    $user = User::findOrFail(1);

    foreach($user->roles as $role){
        $role->where('id',2)->delete();
    }

    // $user->roles()->delete();
});
```

- Iterate the roles where id = 2, then if id = 2 it will delete the role.