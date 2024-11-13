---
title: I UNDERSTAND IT NOW (WP)
date: 2025-11-12
excerpt: T-minus 4 hours exam notes
---
![[ah-ok.gif]]

> CTRL P to search for files in vsc

run `artisan make:model Post -m -s -f`
run `artisan make:model Category -m -s -f`
run `artisan make:model Writer -m -s -f`
run `php artisan make:controller PostController --resource`
run `php artisan make:controller CategoryController --resource`
run `php artisan make:controller WriterController --resource`

# Route

edit `web.php`

```php
// web.php
Route::resource('/category', CategoryController::class);
Route::resource('/post', PostController::class);
Route::resource('/writer', WriterController::class);
```
# View and Blade

make `layouts.app`

add bootstrap `<link rel="stylesheet" href="{{ asset('css/bootstrap.min.css') }}">`

```php
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <title>@yield('title')</title>
        <link rel="stylesheet" href="{{ asset('css/bootstrap.min.css') }}">
    </head>
    <body class="antialiased">
        <header>
            @include('layouts.header')
        </header>
        <div class="container-fluid text-center">
            @yield('content')
        </div>
        @include('layouts.footer')
    </body>
</html>
```

make `layouts.header`

```php
<nav class="navbar navbar-light bg-white shadow-sm sticky-top">
    <div class="container d-flex justify-content-between align-items-center">
        <!-- Logo -->
        <a class="navbar-brand" href="{{ url('/') }}">LOGO</a>

        <!-- Navbar Links -->
        <ul class="navbar-nav d-flex flex-row">
            @if (isset($categories))
                <a class="px-2" 
                href="{{ route('category.index')}}">Categories</a>
            @endif
            @if (isset($post))
            <a class="px-2" href="{{ route('category.index')}}">Writers</a>
            @endif
        </ul>
    </div>
</nav>
```

make `layouts.footer`

```php
<footer class="py-3 my-4 border-top">
    <div class="container d-flex flex-column align-items-center">
        <span class="text-body-secondary text-center mb-3">
            &copy; {{ date("Y") }} Web Programming | 
            Farih Muhammad | 2602165650
        </span>
    </div>
</footer>
```

make `home`

```php
@extends('layouts.app')

@section('title', 'Home')

@section('content')
    <!-- Main Image -->
    <img src="{{ asset('img.jpg') }}" alt="Main Banner"
     class="img-fluid mb-4 w-100">


    <div class="container">
        <h2 class="mb-4">Latest Articles</h2>
        <div class="row g-4">
            @forelse ($posts as $post)
                <div class="col-md-4">
                    <div class="card h-100">
                        <img src="{{ asset('img.jpg') }}" 
                        class="card-img-top" alt="Article Image">
                        <div class="card-body d-flex flex-column">
                            <h5 class="card-title">{{ $post->title }}</h5>
                            <p class="card-text">
                            {{ \Illuminate\Support\Str::
                            limit($post->material, 100, '...') }}</p>
                            <a href="{{ route('post.show', $post) }}" 
                            class="btn btn-primary mt-auto">Read More</a>
                        </div>
                    </div>
                </div>
            @empty
                <div class="col-12">
                    <p class="text-center">
                    No articles available at the moment.</p>
                </div>
            @endforelse
        </div>
    </div>
@endsection

```

make `category`

```php
@extends('layouts.app')

@section('content')
    @forelse ($categories as $category)
        <a href="{{ route('category.show',$category) }}">
        <h1>{{$category->category}}</h1></a>
    @empty

    @endforelse

@endsection
```

make `detail`

```php
@extends('layouts.app')

@section('content')
    <h1>{{ $post->title }}</h1>
    <img src="{{ asset('img.jpg') }}" alt="" class='img-fluid mb-4 w-50'>
    <p>{{ $post->date }}</p>
    <p>{{ $post->author }}</p>
    <p>{{ $post->material }}</p>

@endsection
```

make `show`

```php
@extends('layouts.app')

@section('content')
<div class="container">
    <h2 class="mb-4">Articles</h2>
    <div class="row g-4">
        @forelse ($category->posts as $post)
            <div class="col-md-4">
                <div class="card h-100">
                    <img src="{{ asset('img.jpg') }}" 
                    class="card-img-top" alt="Article Image">
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title">{{ $post->title }}</h5>
                        <p class="card-text">
                        {{ \Illuminate\Support\Str::limit
                        ($post->material, 100, '...') }}</p>
                        <a href="{{ route('post.show', $post) }}" 
                        class="btn btn-primary mt-auto">Read More</a>
                    </div>
                </div>
            </div>
        @empty
            <div class="col-12">
                <p class="text-center">No articles available at the moment.</p>
            </div>
        @endforelse
    </div>
</div>

@endsection
```

# Controller

for each model

```php
public function index()
    {
        $categories = Category::all();
        return view('category',compact('categories'));
    }
```

```php
public function show(string $id)
    {
        $category = Category::findOrFail($id);
        return view('show', compact('category'));
    }
```

edit `.env`

```php
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=utspractice
DB_USERNAME=root
DB_PASSWORD=
```
# Model

update models

```php
class Category extends Model
{
    public function posts(){
        return $this->hasMany(Post::class);
    }
}
```

```php
class Post extends Model
{
    public function categories(){
        return $this->belongsTo(Category::class);
    }
}
```
# Migration

edit migration for each

```php
    public function up(): void
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->string('title');
            $table->text('material');
            $table->date('date');
            $table->string('author');
            $table->foreignId('category_id')->constrained()->cascadeOnDelete();
            $table->timestamps();
        });
    }
```

```php
    public function up(): void
    {
        Schema::create('categories', function (Blueprint $table) {
            $table->id();
            $table->string('category');
            $table->timestamps();
        });
    }
```

reorder by editing file names
# Factory

edit factory

```php
    public function definition(): array
    {
        $categories = ['Health','Sports','Politics'];
        return [
            'category' => fake()->unique()->randomElement($categories)
        ];
    }
```

```php
    public function definition(): array
    {

        return [
            'title'=>fake()->word,
            'material'=>fake()->paragraph(),
            'date'=>fake()->date,
            'author'=>fake()->name,
            'category_id'=>fake()->numberBetween(1,3)
        ];
    }
```
# Seeder and Faker

edit seeder

```php
public function run(): void
    {
        Category::factory()->count(3)->create();
    }
```

```php
    public function run(): void
    {
        Post::factory()->count(10)->create();
    }
```

```php
        $this->call([
            CategorySeeder::class,
            PostSeeder::class
        ]);
```

`php artisan db:seed CategorySeeder`
`php artisan db:seed PostSeeder`    

`php artisan migrate`
`php artisan migrate:fresh -seed`

##### [[Paginate]]

```php
class TransactionController extends Controller{
    public function customerTransaction(){
        $customers = Customer::simplePaginate(5); 
        return view('customer',compact('customers'));
    }
}
```

```php
@extends('layouts.app')

@section('title', 'Customer Transaction') // one line use of section

@section('content')
	<ul>
        @forelse ($customers as $customer)
            <li>{{ $customer->name }} {{ $customer->email }}</li>
        @empty
            <h2>No customers..</h2>
        @endforelse
    </ul>
    <h2>Transacation</h2>
    <ul>
        @forelse ($customers as $customer)
            <li>{{ $customer->name }}</li>
            <ul>
                @forelse ($customer->products as $product)
                    <li>{{ $product->productname }} {{ $product->price }}</li>
                @empty
                    <h4>No transaction..</h4>
                @endforelse
            </ul>
        @empty
            <h2>No customers..</h2>
        @endforelse
    </ul>
    {{ $customers->links() }} // for pagination links
@endsection 
```

Status: #idea  
Tags: [[web-programming]]  

---
# References
