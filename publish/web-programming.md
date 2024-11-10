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

> CAN BE MADE WITH ONE LINE USING MODEL [[-M -S -C]]

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

In case necessary: [[Forms]]

