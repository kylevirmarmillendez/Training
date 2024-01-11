# Forms Uploading Files

**Upload Form**
```html
<form action="/uploadfile" method="post" enctype="multipart/form-data">
    @csrf
    <div class="form-group">
        <input type="file" class="form-control-file" name="fileToUpload" id="exampleInputFile">
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

```php
public function store(CreatePostRequest $request)
    {
$input = $request->all();
        $file = $request->file('file');
        if($file){
            $name = $file->getClientOriginalName();
            $file->move('images', $name);

            $input['path'] = $name;
        }

        Post::create($input);
    }
```
- This function gets all the data along with the file from the form and upload the title, content and the path of the file.


**Iterating posts with image**
```php
<ul>
    @foreach($posts as $post)
    

    <div class="image-container">

      <img height="100" src="{{$post->path}}" alt="Image">

    </div>

    <li>{{$post->title}} - {{$post->content}} <a href="{{route('posts.show', $post->id)}}">view</a></li>


    @endforeach
 </ul>

```

**Accessor**
```php

    public $directory = "/images/";


  public function getPathAttribute($value){
        return $this->directory.$value;
    }
```
- this code will the directory become dynamic.



