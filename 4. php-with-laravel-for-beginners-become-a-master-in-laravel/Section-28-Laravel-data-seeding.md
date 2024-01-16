# Laravel Data Seeding

**Data seeding** inserting dummy data into the application.

```php

factory(App\User::class, 10)->create();

DB::table('users')->insert([
    'name'=> str_random(10),
    'role_id'=> 1, //administrator
    'email'=> str_radom(10).'@gmail.com',
    'password' => bcrypt('secret')
]);
```

**Factories**

```php
$factory(App\User::class,10)->create()->each(function($user){

$user->posts()->save(factory(App\Post::class)->make());
});

```