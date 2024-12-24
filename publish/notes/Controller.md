---
title: Controllers
date: 2024-11-10
excerpt: Basically does the logic and connects view with the model
---
Basically does the logic and connects view with the model

https://laravel.com/docs/11.x/controllers

## Default

`php artisan help make:controller [ClassName]Controller` will not include any methods in the controller file 

## Resource `--resource`

`php artisan make:controller PhotoController --resource` will a method for each of the available resource operations in the container file

```php
// these methods will be generated in the controller
    public function index() //Display a listing of the resource
    public function create() //Show the form for creating a new resource
    public function store(Request $request) // Store a newly created resource in storage
    public function show(string $id) // Display the specified resource
    public function edit(string $id) // Show the form for editing the specified resource
    public function update(Request $request, string $id) // Update the specified resource in storage
    public function destroy(string $id) // Remove the specified resource from storage
```
### Routing a resource controller

Registering a resource route that points to the controller can be done using this:

```php
use App\Http\Controllers\PhotoController;

Route::resource('\endpoint', [ClassName]Controller::class);
Route::resource('photos', PhotoController::class);
```

Status: #idea  
Tags: [[web-programming#web-prog-mid-exam-materials Mid Exam Materials]], [[web-prog-mid-exam-materials]]

---
# References