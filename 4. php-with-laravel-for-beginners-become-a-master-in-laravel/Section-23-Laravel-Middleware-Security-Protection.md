# Laravel Middleware Security Protection

**Middlewares** 
-  is like a filtering mechanisn for HTTP request that are coming in th application.
- one the most important keys in protecting certain aspects of your application.

**To create a middleware:**

```php

$ php artisan make:middleware RoleMiddleware
```



**Route**
```php
Route::get('/admin',[AdminController::class,'index']);

```
- creating route for admin page with controller named index.

**Calling middleware inside the controller**
```php
public function __construct(){
    $this->middleware("IsAdmin");
 }
```


**The IsAdmin Middleware**
```php
class IsAdmin
{
    
     * @param  \Closure(\Illuminate\Http\Request): (\Symfony\Component\HttpFoundation\Response)  $next
     */
    public function handle(Request $request, Closure $next): Response
    {

        $user = Auth::user();

        if(!$user){
            return redirect('/login');
        }

        if(!$user->isAdmin()){
            return redirect('/');
        }
    
        

        return $next($request);
    }
}

```
- this middle check if the user is loggged in and calls the method isAdmin from the User Model.

**Method inside the User Model**

```php
 public function isAdmin(){
        if($this->role->id === 1){

            echo true;
            return true;
        }
        echo false;
       return false;
    }
```
- this method check if the user is admin.



