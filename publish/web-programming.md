---
title: Web Programming (Laravel)
excerpt: Yes we study Laravel @BINUS
---
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

### Create Tables

1. Run the code below to generate migration files

> migration files are used to design the database schema

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

// example:
public function up(): void{
	Schema::create('reviews', function (Blueprint $table) {
		$table->id();
		$table->text('review');
		$table->unsignedTinyInteger('rating');
		$table->timestamps();
		$table->foreignId('book_id')->constrained()->cascadeOnDelete();
	});
}
```

> what is `constrained()`? and `cascadeOnDelete()`?

3. After creating and modifying all migration files run `php artisan migrate` and your tables will be created
   ![[phpTables1.png]]
   ![[phpTables2.png]]

4. Make seeder for each model using`php artisan make:seeder [Class_Name (UpperCase)]Seeder` 

> seeder files are used to populate the table

5. Fill `run()` function for class seeder

Using Faker:
```php
public function run(){ // custom seeder
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
> I still get an error here

6. Fill `run()` function for database seeder

```php
public function run(): void{
	$this->call([
		ProductSeeder::class,
	]);
}
```

7. Create models for each table using `php artisan make:model [Name (Uppercase)]` and it will be located at `app\Models`

> model files are used to define the relationships between tables

8. Define relationships by adding the relationship class as a function to each models 

```php
public function [relationship_class](){ // inside a model
	return $this->belongsToMany([Relationship_class]::class); // 1:N
	return $this->hasMany([Relationship_class]::class); // 1:N
}

class Category extends Model{
    use HasFactory;
    public function products(){
        return $this->hasMany(Product::class); // 1:N
    }
}

class Product extends Model{
    use HasFactory;
    public function category(){
        return $this->belongsTo(Category::class); // 1:1
    }
    public function customers(){
        return $this->belongsToMany(Customer::class); // 1:N
    }
}

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

# Frontend
### Setup Routes
1. Create controller using `php artisan make:controller [Class_name]Controller` and it will be located at `app\Http\Controllers`
2. Add function in the controller to query and pass into view
```php
class TransactionController extends Controller{
    public function category(){
        $categories = Category::all(); // query all
        return view('category',compact('categories'));
    }
}
```
3. Add controller function to `web.php` (Router) in `\routes`
```php
Route:get('\endpoint', [Controller::class, 'function']);
Route::get('oneToMany',[TransactionController::class,'category']);
Route::get('manyToMany',[TransactionController::class,'customerTransaction']);
```
4. **Recommended: Make a layout template** inside `\resources\views\` add a `\layouts` folder filled with `app.blade.php`
```php
// example layouts\app.blade.php
<!DOCTYPE html>
	<html lang="en">
	
	<head>
	  <meta charset="UTF-8">
	  <title>Example</title> // create a section for the title
	</head>
	
	<body>
	  <h1>@yield('title')</h1>
	  @yield('content') // create a section for the content
	</body>
</html>
```

```php
// example of blade.php file that extends layouts\app.blade.php
@extends('layouts.app')

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

5. Locate Bootstrap Folder
6. Pick the folder with the version according to the requirement
7. Find `\css` folder and copy
8. Paste `\css` folder to `\public` forlder
9. Inside `<head></head>` tag add link to tailwind ‼️ using `asset()`
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

> Pagination: use `simplePaginate()` instead of `all()` and in the `links()` at the bottom

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