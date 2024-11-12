---
title: Simple Form Implementation
date: 2024-11-10
excerpt: Simple implementation of forms in laravel for creating data
---

1. Edit `.env`

```php
DB_CONNECTION=sqlite
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=FoodDB
DB_USERNAME=root
DB_PASSWORD=
```


2. Run `php artisan make:model Food -m -s` 
3. Run `php artisan make:model FoodCategory -m -s`

> i want a resource controller so without -c

3. Edit migration file and run `php artisan migrate`

```php
// 2024_11_10_094235_create_food_table.php
public function up(): void {
	Schema::create('food', function (Blueprint $table) {
		$table->id();
		$table->string('name');
		$table->integer('price');
		$table->string('description');
		$table->timestamps();
	});
}
```

4. Edit ClassSeeder

```php
// FoodSeeder.php
public function run(): void {
	Food::insert([
		'name' => 'Food 1',
		'price' => 15000,
		'description' => 'Yummy'
	]);
}
```

5. Edit DatabaseSeeder the run `php artisan db:seed`

```php
// DatabaseSeeder.php
class DatabaseSeeder extends Seeder {
    public function run(): void {
        $this->call(FoodSeeder::class);
    }
}
```

6. Create and edit ClassController 
   `php artisan make:controller FoodController --resource`

Without resource controller:

```php
// FoodController.php
class FoodController extends Controller
{
    public function index(){
        // $foods = Food::all();
        $foods = Food::simplePaginate(2);
        return view('home',compact('foods'));
    }

    public function insert() {
        return view('insert');
    }

    public function store(Request $request)
    {
        // $task = Food::create($request->all());
        Food::insert([
            'name'=> $request->name,
            'price'=> $request->price,
            'description'=> $request->description,
        ]);
        return redirect()->route('food.index');
    }
}
```

With resource controller:

```php
<?php
// FoodController.php
namespace App\Http\Controllers;

use App\Models\Food;
use Illuminate\Http\Request;

class FoodController extends Controller
{
    /**
     * Display a listing of the resource.
     */
    public function index()
    {
        // $foods = Food::all();
        $foods = Food::simplePaginate(2);
        return view('home',compact('foods'));
    }

    /**
     * Show the form for creating a new resource.
     */
    public function create()
    {
        return view('create');
    }

    /**
     * Store a newly created resource in storage.
     */
    public function store(Request $request)
    {
        Food::insert([
            'name'=> $request->name,
            'price'=> $request->price,
            'description'=> $request->description,
        ]);
        return redirect()->route('food.index');
    }

    /**
     * Display the specified resource.
     */
    public function show(string $id)
    {
        //
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(string $id)
    {
        //
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, string $id)
    {
        //
    }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(string $id)
    {
        //
    }
}

```

7. Edit Routes

```php
// without resource controller
// Route::get('/', [FoodController::class, 'index'])->name('food.index');
// Route::get('/insert', [FoodController::class, 'create'])->name('food.create');
// Route::post('/store', [FoodController::class, 'store'])->name('food.store');

// with resource controller
Route::resource('/food', controller: FoodController::class);
```

8. Link Bootstrap and create views

```php
// layouts\app.blade.php
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>@yield('title')</title>
    <link rel="stylesheet" href="{{asset('css/bootstrap.min.css')}}">
    // bootstrap
    <style>
        .container {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            justify-content: space-around;
            align-items: center;
        }

        .box {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background-color: gainsboro;
            border-radius: 8px;
            padding: 10px;
            margin: 10px;
            min-width: 150px;
        }
    </style>
    // custom styles
</head>

<body>
    <h1>
        @yield('body_title')
    </h1>
    @yield('content')
</body>

</html>
```

```php
// create.blade.php
@extends('layouts.app')

@section('title', 'Insert')
@section('body_title', 'Insert')

@section('content')
<form action="{{route('food.store')}}" method="POST">
    @csrf
    <label for="name">Name:</label>
    <input type="text" name="name" id="name"><br><br>
    <label for="price">Price:</label>
    <input type="text" name="price" id="price"><br><br>
    <label for="description">Description:</label>
    <input type="text" name="description" id="description"><br><br>
    <input type="submit">
</form>
@endsection
```

```php
// home.blade.php
@extends('layouts.app')

@section('title', 'Home')
@section('body_title', 'Home')

@section('content')
    <a href="{{ route('food.create') }}">Insert Food</a>
    <div class="container">
        @foreach ($foods as $food)
            <div class="box">
                <h3>{{ $food->name }}</h3>
                <h3>{{ $food->price }}</h3>
                <h3>{{ $food->description }}</h3>
            </div>
        @endforeach
    </div>
    {{ $foods->links() }}
@endsection
```

