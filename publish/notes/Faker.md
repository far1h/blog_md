---
title: Faker
excerpt: whats the difference of different kinds of fake instead of fake and real
date: 2024-11-10
---
### 1. **`faker`** (lowercase)
- In Laravel, `faker` is often used as a property in factories or test cases, and it provides access to an instance of the `Faker` class.
- Laravel automatically resolves `faker` for you in many cases, such as in factory definitions or PHPUnit tests.
- Example in a factory:
  ```php
  'name' => $this->faker->name,
  ```
- It is a shorthand for using the Faker library in Laravel.

---

### 2. **`Faker`** (uppercase)
- `Faker` is the actual **class** provided by the [Faker library](https://fakerphp.github.io/).
- It's a PHP library used to generate fake data, such as names, emails, and addresses.
- If you want to manually create an instance of the `Faker` class, you can do this:
  ```php
  use Faker\Factory;

  $faker = Factory::create();
  echo $faker->name;
  ```
- In this case, `Faker` refers to the main library that Laravel integrates with for generating fake data.

---

### 3. **`fake()`**
- `fake()` is a **new helper function** introduced in Laravel 9, designed to provide an easier way to access a Faker instance directly.
- You can call it globally without needing to explicitly set up or inject `Faker` or `faker`.
- Example usage:
  ```php
  $name = fake()->name;
  $email = fake()->email;
  ```
- It simplifies usage, especially in testing and small scripts, and is particularly useful in Laravel projects starting with version 9.

---

### Key Differences
| **Term**  | **Context**  | **Purpose**  |
|-----------|--------------|--------------|
| `faker`   | Laravel property | A shorthand instance of the `Faker` library, often pre-configured in factories and tests. |
| `Faker`   | PHP class     | The main library for generating fake data, requiring manual instantiation. |
| `fake()`  | Laravel helper | A Laravel-provided helper function to quickly get a `Faker` instance without manual setup. |

---

### Summary
- **In Laravel 9+**, `fake()` is the easiest and most recommended way to use Faker.
- `faker` is the Laravel-integrated shorthand for an instance of `Faker`.
- `Faker` is the original library and is still accessible manually if needed.

Status: #idea
Tags: [[web-programming]]

---
# References