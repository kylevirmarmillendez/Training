# New Laravel 7 Application - Permissions & Roles CRUD

**Creating Role**
- Creating different roles for your application.
- It is very useful because you can create you own role with its own permissions.

```php
public function store(Request $request){
    $input_data = $request->all();
    Role::create($input_data);
}
```

<br>


**Display Role**
- Iterating all the roles inside a table.
```php
public function view(Request $request){
     $roles = Role::all();

     return view('admin.roles.index',['roles'=> $roles]);s
}
```
<br>


**Deleting a Specific Role**

```php
public function destroy(Role $role){
    $role->delete();
    return back()
}
```

<br>

**Updating a Specific Role**

```php
public function update(Request $request,$id){
    
    $role = Role::findOrFail($id);

    $role = new Role;
    $role->name = $request->name;
    $role->slug = $request->name;

    $role->save();

}
```