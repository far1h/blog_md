---
date: 2024-11-09
excerpt: a shorthand in Laravel's migration schema builder that helps you quickly define a foreign key constraint for a column.
---
The `constrained()` method is a shorthand in Laravel's migration schema builder that helps you quickly define a foreign key constraint for a column.

`$table->foreignId('column_name')->constrained('table_name');`

- Automatically creates a foreign key constraint on the specified column.
- Infers the referenced table if not explicitly provided. For example, `user_id` would refer to the `users` table by default.
- Assumes the foreign key references the `id` column of the referenced table.

#### Example

```php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->foreignId('user_id')->constrained(); // References `users.id` by default
    $table->timestamps();
});
```

Equivalent to:

```php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->unsignedBigInteger('user_id');
    $table->foreign('user_id')->references('id')->on('users');
    $table->timestamps();
});
```

Status: #idea
Tags: [[web-programming]]

---
# References