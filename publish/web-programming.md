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
1. Create controller using `php artisan make:controller [Class_name]Controller`
2. Add function to go to query and pass to view


