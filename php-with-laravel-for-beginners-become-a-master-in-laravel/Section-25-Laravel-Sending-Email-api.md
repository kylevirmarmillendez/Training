# Laravel Sending Email API

 - Since the mailgun requested for payment, I use [mailpit](https://mailpit.axllent.org/docs/install/) instead.


```php
Route::get('/', function () {
    // return view('welcome');

    $data = [
        'title'=> 'Hi student I hope you like the course',
        'content'=> 'This laravel course was created with a lot of love and dedication for you'
    ];

    Mail::send('emails.test', $data, function($message){
        $message->to('kylevirmar.millendez@nabepero.co.jp','Kyle')->subject('Hello students how are you?');
    });
});

```