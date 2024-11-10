1. Edit `.env`

```php
DB_CONNECTION=sqlite
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=FoodDB
DB_USERNAME=root
DB_PASSWORD=
```


2. Run `php artisan make:model Food -m -s -c`

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

6. Modify ClassController

```php
// FoodController.php
class FoodController extends Controller
{
    public function index(){
        $foods = Food::all();
        return view('home',compact('foods'));
    }

    public function insert() {
        return view('insert');
    }
}
```

7. Edit Routes
9. Link Bootstrap and create views

```php
// layouts\app.blade.php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>@yield('title')</title>
</head>
<body>
    <h1>
        @yield('body_title')
    </h1>
    <a href="{{route()}}">Insert Food</a>
    @yield('content')
</body>
</html>
```

```php
// home.blade.php

```

