# Laravel Sessions

**Session Setup**
```php
Route::get('/session',function(Request  $request) {
  $request->session()->put(['name'=>'Kyle Millendez']);
```
**Read Session**
```php
 return session()->all();
```

**Update session**
```php
   session(['kyle'=>'virmar']);
     return session('sadasdd');
```

**Delete a single Session**
```php
$request->session()->forget('name2');
```

**Delete all the session**
```php
$request->session()->flush();
```

**Flashing data**
```php
    $request->session()->flash('message', 'Post has been created');

    return $request->session()->get('message');
```

