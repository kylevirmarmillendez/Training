# Laravel Forms and Validations

### Routing

```php
Route::resource('/posts',PostsController::class);
```

### CRUD Sequence

**Create**

```php
 public function create()
    {
        return view('posts.create');
    }
```

- This code will display a form to create a post.

```html
@extends('layouts.app') @section('content')

<form
  method="POST"
  action="/posts">
  {{csrf_field()}}
  <input
    type="text"
    name="title"
    placeholder="Enter title" />
  <input
    type="text"
    name="content"
    placeholder="content" />
  <input
    type="submit"
    name="submit" />
</form>
@endsection
```

- This is the HTML code for the post create form.

**Store**

```php
 public function store(Request $request)
    {
    //    $title  = $request->title;

        // Post::create($request->all());

        $post = new Post;

        $post->title = $request->title;
        $post->content = $request->content;
        $post->save();

        return redirect('/posts');
    }
```

- If the user will hit the submit button the function will be triggered the it will store the inputed data to the database.

**Read**

```php
  public function index()
    {
        $posts = Post::all();
        return view('posts.index',compact('posts'));
    }
```

- This block of code will get all the Posts from the database to display on the index view.

<br>

```html
@extends('layouts.app') @section('content')
<ul>
  @foreach($posts as $post)

  <li>
    {{$post->title}} - {{$post->content}}
    <a href="{{route('posts.show', $post->id)}}">view</a>
  </li>

  @endforeach
</ul>
@endsection
```

- In this html code, all the posts will iterated.

**Show**

```php
  public function show(string $id)
    {
        $post = Post::findOrFail($id);
        return view('posts.show',compact('post'));
    }
```

- It gets a one post by id and send it to the show view and display.

```php
<ul>

    <li>{{$post->title}}-{{$post->content}}   ----- <a href="/posts/{{$post->id}}/edit">Edit</a></li>

</ul>
```

- It displays the individual Posts.

**Update**

```php
  public function update(Request $request, string $id)
    {

    $post = Post::findOrFail($id);
    $post->update(["title"=>$request->title,"content"=>$request->content]);
    return redirect('/posts');


    }
```
- if the update button is clicked the this function will trigger and this will send the new data to the database.



**Delete**
```php
  public function destroy(string $id)
    {

        $post = Post::findOFail($id);
        $post->delete();
        return redirect('/posts')
    }
```
- with this code, this will delete a posts by its ID.
