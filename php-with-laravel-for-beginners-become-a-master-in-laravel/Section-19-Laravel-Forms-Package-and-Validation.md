# Laravel Forms Package and Validation


**Install laravelcollective/html**

```cli
$ composer require laravelcollective/html
```

**Creating form using Laravelcollective/html**
```html
{!!Form::open(['method'=> 'POST', 'action'=>'App\Http\Controllers\PostsController@store'])!!}


<div class="form-group">
    {!!Form::label('title','Title:')!!}
    {!!Form::text('title',null,['class'=>'form-control', 'placeholder'=>'Enter title'])!!}
    {!!Form::text('content',null,['class'=>'form-control', 'placeholder'=>'Enter Content'])!!}
</div>

    {!!Form::submit('Submit')!!}
    {{-- <input type="text" name="title" placeholder="Enter title">
    <input type="text" name="content" placeholder="content"> --}}
    {{-- <input type="submit" name="submit"> --}}
{!!Form::close()!!}
```

**Simple Form Validation**

```php
    $validated = $request->validate([
        'title'=> 'required|unique:posts|max:255',
        'content'=>'required',
       ]);
```
- validates the form field.


**Error Handling**

```php
@if(count($errors)>0)
    @foreach($errors->all() as $error)

    <li>{{$error}}</li>
    @endforeach
@endif
```
- iterating the errors and display the errors.