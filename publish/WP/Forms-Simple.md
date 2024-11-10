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

3. Edit migration file

```php
// 2024_11_10_094235_create_food_table.php
public function up(): void{
	Schema::create('food', function (Blueprint $table) {
		$table->id();
		$table->string('name');
		$table->integer('price');
		$table->string('description');
		$table->timestamps();
	});
}
```

4. Edit seeder

```php
// FoodSeeder.php
public function run(): void{
	Food::insert([
		'name' => 'Food 1',
		'price' => 15000,
		'description' => 'Yummy'
	]);
}
```

