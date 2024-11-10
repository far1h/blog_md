# Seeder

```php
class DatabaseSeeder extends Seeder {
    public function run(): void {
        [ModelName]::factory(10)->create(); 
        // it will the factory template 10 times
    }
}
```

# Model

prepare the model to be used by the factory by adding fillable properties

```php
protected $fillable = ['title','description','long_description'];
```

# Factory

create a factory and link to the model using this code:

```
php artisan make:factory TaskFactory --model=Task
```

modify the `definition()` method with [[Faker]] in the factory file:

```php 
// example: TaskFactory.php
public function definition(): array {
	return [
		'title' => $this->faker->sentence,
		'description' => $this->faker->paragraph,
		'long_description' => $this->faker->paragraph(7, true),
		'completed' => $this->faker->boolean,
	];
}
```

```php
// example: BookFactory.php
public function definition(): array
    {
        return [
            'title' => fake()->sentence(3),
            'author' => fake()->name,
            'created_at' => fake()->dateTimeBetween('-2 years'),
            'updated_at' => fake()->dateTimeBetween('created_at','now')
        ];
    }
```

