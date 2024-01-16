# Laravel Form Login


**Laravel Login Setup**
```$
$ composer require laravel/ui

$ php artisan ui vue --auth

$ npm install && npm run dev

$ php artisan migrate
```

<br>
<br>

```php
 public function index()
    {
       $user = Auth::user();
       return view('home',compact('user')); 
    }
```
- Retrieving the data who is logged in.


**Checking Auth**
```php
  if(Auth::check()){
        return "the user is logged in!!";
    }
    return redirect('/login');
```

- if the user is logged it it will return "the user is logged in!!" otherwise it will redirect to login page.


```php
    $username = "adadadas";
    $password = "asdadasd";

    if(Auth::attempt(['username'=>$username, 'password'=>$password])){
        return redirect()->intended();
    }
```


