# New Laravel 7 Application -  Admin Users


**All Users**
- Iterating or displaying all the users in the admin page.
- Only the admin can view users list.

```php

public function users(){
    $users = User::all();
    return view('admin.index.users', ['users'=> $users]);
}
```
<br>
<br>

**Deleting Users**
- Only the Admin has a permission delete user.


```php
public function destroy(User $user){
    $user->delete();
    return back();
}
```


<br>
<br>

**Components Nesting**
- Nesting component makes you code cleaner and easy to read.
- When you have na main page composes with different components and thoes components has their own components also.
- It is very useful because you can easily location or find you codes. 
