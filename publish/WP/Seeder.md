There are 3 ways to insert data:

```php
<?php

namespace Database\Seeders;

use Carbon\Carbon;
use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;

class ClothesSeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        //
        // 3 methods:
        // 1. DB::raw
        // 2. DB::table
        // 3. Model::

        // 1. -> DB RAW -> Manual Query
        // DB::raw("INSERT INTO USER BLABLABLA)
        // DB::raw("SELECT * FROM USERS)

        // 2. -> Query Builder -> Built in laravel
        // DB::table("users)->insert(['name'=> blabal])
        // DB::table('users')->get();

        // 3. -> Eloquent - ORM (Object Relational mapping)
        // User::insert([]);
        // User:all();

        Clothes::insert([
            'name' => 'Uniqlo Airism Oversized',
            'price'=> '200000',
            'created_at'=> Carbon::now(),
            'updated_at'=> Carbon::now()
            ]);
    }
}
```