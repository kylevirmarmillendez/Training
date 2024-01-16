# New Application Laravel 7


- **Create New laravel Application** for the new-cms-system.

- **Installing the laravel/ui** enable to use the bootstrap built in authentication.

- import all the all the templates in the different blade files.

- Change the default login and registration route in RouteServiceProvide to the newly added route '/' that displays the home page with  bootstrap template.


### Creating Seeds


```php
 public function definition(): array
    {
        return [
            'user_id'=> User::factory(),
            'title'=> fake()->sentence(),
            'post_image'=> fake()->imageUrl('900','400'),
            'body' => fake()->paragraph(),
        ];
    }
```
**Creating Seeds** -  Inside the factory directory, I've created a factory named  PostFactory the provide fake credentials of the posts.


<br>
<br>

```php
 public function run(): void
    {
        User::factory()->count(10)->create()->each(function($user){
            $user->posts()->save(Post::factory()->create());
        });
    }
```

- Since the User has its own UserFactory, in the DatabaseSeeder.php you need logic that if you create a user using faker library it will automatically create a posts in each user.



**Creating Views**
- Setting all the views with it's routes and get the all data that are needed in a particular view.
- Using Bootstrap for styling and downloaded prebuild template each view.

**Display all the posts**
- Display all the posts that are generated using factory.

**Creating middlewares**
- Since authentication has been added to the project, middlewares are need to have a admin authorization so there are some routes that can be access when your are authorized.