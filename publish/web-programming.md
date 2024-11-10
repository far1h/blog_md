---
title: Web Programming (Laravel)
excerpt: Yes we study Laravel @BINUS
---
`//TODO` 
- [ ] Link to documentation for easy reference
##### Mid Exam Materials

![[uts-kisi.jpg]]

![[webutsnotes.jpg]]
# Initialization

```shell
composer create-project laravel/laravel newProject
```

> not necessary since no wifi and project might be already given
# Database
### Setup Database

1. Open `.env` file and look for `DB_..` and make sure its the same as this

```php
DB_CONNECTION=mysql // XAMPP runs mysql database engine
DB_HOST=127.0.0.1 
DB_PORT=3306 // port for database
DB_DATABASE=laravelproject // make a new database name 
DB_USERNAME=root // credentials for XAMPP
DB_PASSWORD= // empty by default by XAMPP
```

> Open XAMPP and turn on Apache Web Server and MySQL Database
### Create Tables

##### Migration

> migration files are used to design the database schema

1. Run the code below to generate migration files

```php
php artisan make:migration create_[class_name]_table --create=[class_name]
// php artisan make:migration create_products_table --create=products
// php artisan make:migration create_customer_product_table --create=customer_product
// use --create for old laravel
```

2. The file we will have to modify will look like this:

```php
public function up(){ 
	Schema::create('[class_names]', function (Blueprint $table) {
		$table->id();
		$table->string('[column_name]'); // custom column
		$table->integer('[column_name]'); // custom column
		$table->foreignId('[column_name]')->constrained(); // foreignID
		$table->timestamps();
	});
}

// example: 2024_10_13_021928_create_reviews_table.php
public function up(): void{
	Schema::create('reviews', function (Blueprint $table) {
		$table->id();
		$table->text('review');
		$table->unsignedTinyInteger('rating');
		$table->timestamps();
		$table->foreignId('book_id')->constrained()->cascadeOnDelete() ;
	});
}
```

> what is [[constrained()]] and [[cascadeOnDelete()]]?

3. After creating and modifying all migration files run `php artisan migrate` and your tables will be created
   ![[phpTables1.png]]
   
   ![[phpTables2.png]]

##### [[Seeder]]

> seeder files are used to populate the table

> can be populated using class seeder and database seeder or [[factory-and-dbseeder|factory and database seeder]]

4. Make seeder for each model using`php artisan make:seeder [Class_Name (UpperCase)]Seeder` 

5. Fill `run()` function for class seeder

Using [[Faker]]:

```php
// example class seeder: CustomerSeeder.php
public function run(){ 
	$faker = Faker::create('id_ID');
	for($i = 1;$i <= 10;$i++){
		DB::table('customers')->insert([
			'name' => $faker->name,
			'email' => $faker->email,
		]);
	}
}
```
![[afterSeeder1.png]]

Manually:

```php
// example class seeder: ProductSeeder.php
public function run(){
	DB::table(table: 'products')->insert([
		['productname' => 'Beng Beng',
		'price' => 2000,
		'image' => 'chocolate.jpg',
		'category_id' => 1],
		
		['productname' => 'Chitato 100gr',
		'price' => 12000,
		'image' => 'chocolate.jpg',
		'category_id' => 2],
		
		['productname' => 'Yakult',
		'price' => 2000,
		'image' => 'chocolate.jpg',
		'category_id' => 4],
	]);
}
```

6. Fill `run()` function for database seeder

```php
// DatabaseSeeder.php
public function run(): void{
	$this->call([
		ProductSeeder::class,
	]);
}
```

7. Execute the seeder using `php artisan db:seed`
##### Model

> model files are used to define the relationships between tables

1. Create models for each table using `php artisan make:model [Name (Uppercase)]` and it will be located at `app\Models`

2. Define relationships by adding the relationship class as a function to each models 

```php
// relationship_class() in a Model
public function [relationship_class](){ // inside a model
	return $this->belongsToMany([Relationship_class]::class); // 1:N
	return $this->hasMany([Relationship_class]::class); // 1:N
}

// Category.php
class Category extends Model{
    use HasFactory;
    public function products(){
        return $this->hasMany(Product::class); // 1:N
    }
}

// Product.php
class Product extends Model{
    use HasFactory;
    public function category(){
        return $this->belongsTo(Category::class); // 1:1
    }
    public function customers(){
        return $this->belongsToMany(Customer::class); // 1:N
    }
}

// Customer.php
class Customer extends Model{
    use HasFactory;
    public function products(){
        return $this->belongsToMany(Product::class); // 1:N
    }
    public function idcard(){
        return $this->hasOne(Idcard::class); // 1:1
    }
}
```

Available relationship functions:
- `hasMany()`
- `belongsTo()`
- `belongsToMany()`
- `hasOne()`
- `...`

### Cheats

##### Model WITH Migration Seeder Controller

> MIGRATION SEEDER AND CONTROLLER CAN BE MADE WITH ONE LINE USING [[-M -S -C]]

```
php artisan make:model [ClassName] -m -s -c
php artisan make:model Clothes -m -s -c
```

Running this command would create the following files:
- **`app/Models/Clothes.php`**: The model file.
- **`database/migrations/xxxx_xx_xx_xxxxxx_create_clothes_table.php`**: The migration file to define the schema of the `clothes` table.
- **`database/seeders/ClothesSeeder.php`**: The seeder file for populating the `clothes` table.
- **`app/Http/Controllers/ClothesController.php`**: The controller file to manage CRUD operations for the `Clothes` model.

##### Migrate and Seed at Once

`php artisan migrate:fresh --seed` basically resets everything and populates it 
# Frontend

##### [[Controller]]

> Basically does the logic and connects view with the model

1. Create controller using `php artisan make:controller [Class_name]Controller` and it will be located at `app\Http\Controllers`
2. Add function in the controller to query and pass into view

```php
class TransactionController extends Controller{
    public function category(){
        $categories = Category::all(); // query all
        return view('category',compact('categories'));
        // return view("home", ["categories"=> $categories]); 
        // the same used if variable names are diff or duplicate names exist
    }
}
```

##### Router

> Used to set up endpoints which execute the function of the controller

3. Add controller function to `web.php` (Router) in `\routes`

```php
Route:get('\endpoint', [Controller::class, 'function']); // template
Route::get('oneToMany',[TransactionController::class,'category']);
Route::get('manyToMany',[TransactionController::class,'customerTransaction']);
```

##### Views

> Front end html css. What the users interact with. UI elements.

4. **Recommended: Make a layout template** inside `\resources\views\` add a `\layouts` folder filled with `app.blade.php`

```php
// example layouts\app.blade.php
<!DOCTYPE html>
	<html lang="en">
	
	<head>
	  <meta charset="UTF-8">
	  <title>Example</title> 
	</head>
	
	<body>
	  <h1>@yield('title')</h1> // section for the title
	  @yield('content') // section for the content
	</body>
</html>
```

> `@yield()` used to create a section

```php
// example of blade.php file that extends layouts\app.blade.php
@extends('layouts.app') // EXTENDS 

@section('title', 'The list of tasks') // one line use of section

@section('content')
    <nav>
        <a href="{{ route('tasks.create') }}">Add Task</a>
    </nav>
    @forelse ($tasks as $task)
        <div>
            <a href="{{ route('tasks.show', ['task' => $task->id]) }}" @class(['line-through' => $task->completed])>{{ $task->title }}</a>
        </div>
    @empty
        <div>There are no tasks!</div>
    @endforelse
    @if ($tasks->count())
        <nav>
            {{ $tasks->links() }}
        </nav>
    @endif
@endsection // use end section if not one line

```

> Use `!` to generate HTML template

##### Bootstrap

> CSS Framework

5. Locate Bootstrap Folder
6. Pick the folder with the version according to the requirement
7. Find `\css` folder and copy
8. Paste `\css` folder to `\public` folder
9. Inside `<head></head>` tag add link to tailwind using `asset()` and `rel="stylesheet"`

```php
<head>
	<title>
		Table Relation
	</title>
	<link href="{{asset('css/bootstrap.min.css')}}" rel="stylesheet" >
</head>
```

10. Add code in view file linked to controller to show queried results

```php
@extends('layouts.app')

@section('title', 'Product Category') // one line use of section

@section('content')
	<ul>
		@forelse ($categories as $category) // for each category
		   <li>{{$category->category}}</li>  // show category name
		   <ul>
				@forelse ($category->products as $product) 
				// for each products in the category
				<li>
					{{$product->productname}} 
					// show product name
					<img src="{{asset($product->image)}}">
					// show product image
				</li>
				@empty
					<h4>No product found..</h4> // if category has no products
				@endforelse
		   </ul>
		@empty
			<h2>No category..</h2> // there are no categories
		@endforelse
	</ul>
@endsection 
```

11. Previously we tried simulate the one to many relationship and below is the example for many to many relationship

##### Paginate

> use `simplePaginate()` instead of `all()` and add `links()` at the bottom

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

Check out my Github repo for example implementation: https://github.com/far1h/utsProject

> Check commits for step by step process
### Forms (in case necessary)

> too complicated. bottom example uses tailwind.

```php
// web.php
<?php

use App\Http\Controllers\TaskController;
use App\Models\Task;
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return redirect()->route('tasks.index');
});

Route::resource('tasks', TaskController::class);

Route::put('tasks/{task}/toggle-complete', function (Task $task) {
    $task->toggleComplete();
    return redirect()->back()->with('success', 'Task updated successfully!');
})->name('tasks.toggle-complete');

Route::fallback(function () {
    return "Still got somewhere";
});


```

```php
// TaskController.php
<?php
namespace App\Http\Controllers;

use App\Models\Task;
use Illuminate\Http\Request;

class TaskController extends Controller
{
    /**
     * Display a listing of the resource.
     */
    public function index()
    {
        $tasks = Task::latest()->paginate(10);
        return view('index', compact('tasks'));
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
        $task = Task::create($request->all());
        return redirect()->route("tasks.show", ['task' => $task->id])->with("success", "Task created successfully!");
    }

    /**
     * Display the specified resource.
     */
    public function show(string $id)
    {
        $task = Task::findOrFail($id);
        return view('show', compact('task'));
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(string $id)
    {
        $task = Task::findOrFail($id);
        return view('edit', compact('task'));
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, string $id)
    {
        $task = Task::findOrFail($id);
        $task->update($request->all());

        return redirect()->route("tasks.show", ['task' => $task->id])->with("success", "Task updated successfully!");
    }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(string $id)
    {
        $task = Task::findOrFail($id);
        $task->delete();

        return redirect()->route('tasks.index')->with('success', 'Task deleted successfully!');
    }
}

```

```php
// edit.blade.php
@extends('layouts.app')

@section('content')
    @include('form', ['task' => $task])
@endsection

```

```php
// create.blade.php
@extends('layouts.app')

@section('content')
    @include('form')
@endsection

```

```php
// form.blade.php
@extends('layouts.app')

@section('title', isset($task) ? 'Edit Task' : 'Add Task')

@section('content')
    <form action="{{ isset($task) ? route('tasks.update', ['task' => $task->id]) : route('tasks.store') }}" method="POST">
        @csrf
        @isset($task)
            @method('PUT')
        @endisset
        <div class="mb-4">
            <label for="title">
                Title
            </label>
            <input type="text" name="title" id="title" @class(['border-red-500' => $errors->has('title')]) {{-- class="border @error('title') border-red-500 @enderror" --}}
                value="{{ $task->title ?? old('title') }}">
            @error('title')
                <p class="error">{{ $message }}</p>
            @enderror
        </div>
        <div class="mb-4">
            <label for="description">Description</label>
            <textarea name="description" id="description" @class(['border-red-500' => $errors->has('description')]) rows="5">
                {{ $task->description ?? old('description') }}
            </textarea>
            @error('description')
                <p class="error">{{ $message }}</p>
            @enderror
        </div>
        <div class="mb-4">
            <label for="long_description">Long Description</label>
            <textarea name="long_description" id="long_description" @class(['border-red-500' => $errors->has('long_description')]) rows="10">
                {{ $task->long_description ?? old('long_description') }}
            </textarea>
            @error('long_description')
                <p class="error">{{ $message }}</p>
            @enderror
        </div>
        <div class="flex gap-2 items-center">
            <button type="submit" class="btn">
                @isset($task)
                    Update Task
                @else
                    Add Task
                @endisset
            </button>
            <a href="{{ route('tasks.index') }}" class="link">Cancel</a>
        </div>
    </form>
@endsection

```

```php
// show.blade.php
@extends('layouts.app')

@section('title', $task->title)

@section('content')
    <div class="mb-4">
        <a href="{{ route('tasks.index')}}"
    class="link">← Go back to the task list!</a>
    </div>

    <p class="mb-4 text-slate-700">{{ $task->description }}</p>
    @if ($task->long_description)
        <p class="mb-4 text-slate-700">{{ $task->long_description }}</p>
    @endif

    <p class="mb-4 text-sm text-slate-500">Created {{ $task->created_at->diffForHumans() }} · Updated {{ $task->updated_at->diffForHumans() }}</p>

    <p class="mb-4">
        @if ($task->completed)
            <span class="font-medium text-green-500">
                Completed
            </span>
        @else
            <span class="font-medium text-red-500">
                Not completed
            </span>
        @endif
    </p>

    <div class="flex gap-2">
        <a href="{{ route('tasks.edit', ['task' => $task]) }}"
            class="btn">Edit</a>
        <form method="POST" action="{{ route('tasks.toggle-complete', ['task' => $task]) }}">
            @csrf
            @method('PUT')
            <button type="submit" class="btn">
                Mark as {{ $task->completed ? 'not completed' : 'completed ' }}
            </button>
        </form>
        <form action="{{ route('tasks.destroy', ['task' => $task]) }}" method="post">
            @csrf
            @method('DELETE')
            <button type="submit" class="btn">Delete</button>
        </form>
    </div>
@endsection

```

```php
// show.blade.php
@extends('layouts.app')

@section('title', 'The list of tasks')

@section('content')
    <nav class="mb-4">
        <a href="{{ route('tasks.create') }}" class="link">Add Task</a>
    </nav>
    @forelse ($tasks as $task)
        <div>
            <a href="{{ route('tasks.show', ['task' => $task->id]) }}" @class(['line-through' => $task->completed])>{{ $task->title }}</a>
        </div>
    @empty
        <div>There are no tasks!</div>
    @endforelse
    @if ($tasks->count())
        <nav class="mt-4">
            {{ $tasks->links() }}
        </nav>
    @endif
@endsection

```

```php
// layouts\app.blade.php
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Laravel 10 Task List App</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="//unpkg.com/alpinejs" defer></script>

    <style type="text/tailwindcss">
        .btn {
            @apply rounded-md px-2 py-1 text-center font-medium shadow-sm ring-1 ring-slate-700/10 hover:bg-slate-50 text-slate-700
        }

        .link {
            @apply font-medium text-gray-700 underline decoration-pink-500
        }

        label {
            @apply block uppercase text-slate-700 mb-2
        }

        input,
        textarea {
            @apply shadow-sm appearance-none border w-full py-2 px-3 text-slate-700 leading-tight focus:outline-none
        }

        .error {
            @apply text-red-500 text-sm
        }
    </style>
    @yield('styles')
</head>

<body class="container mx-auto mt-10 mb-10 max-w-lg">
    <h1 class="text-2xl mb-4">@yield('title')</h1>
    <di x-data="{ flash: true }">
        @if (session()->has('success'))
        <div x-show="flash"
        class="relative mb-10 rounded border border-green-400 bg-green-100 px-4 py-3 text-lg text-green-700"
            role="alert">
            <strong class="font-bold">Success!</strong>
            <div>{{ session('success') }}</div>
            <span class="absolute top-0 bottom-0 right-0 px-4 py-3">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    @click="flash = false" stroke="currentColor" class="h-6 w-6 cursor-pointer">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                </svg>
            </span>
        </div>
        @endif
        @yield('content')
        </div>
</body>

</html>


```