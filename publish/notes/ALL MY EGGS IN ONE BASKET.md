https://github.com/Darnivo/Webprog/tree/main/TestProj

https://www.notion.so/RESPONSI-DOSEN-180b15279982805fa038d1352477a6be

https://docs.google.com/document/d/1ezx8xgj-UKL8ZGTZR3UW3_v_FCEqVlk9YTukyExYGkE/edit?tab=t.0

https://docs.google.com/document/d/121yJ4aoZzQbhY71NySookosSJiN3dGst1UMeBFIMK_I/edit?tab=t.0

https://docs.google.com/document/d/1PNngFm3_2Xx-fzt_wYawG0h6YRHjw6kV588GovEyxMQ/edit?tab=t.de446aaqjhhj


```
AccountController.php
<?php

  

namespace App\Http\Controllers;

  

use Illuminate\Http\Request;

use App\Models\User;

use Illuminate\Support\Facades\Auth;

  

class AccountController extends Controller

{

public function login(Request $request)

{

$credentials = $request->validate([

'username' => 'required',

'password' => 'required'

]);

  

if (Auth::attempt($credentials)) {

$request->session()->regenerate();

return redirect()->intended('home');

}

  

return back()->withErrors([

'error' => 'The provided credentials do not match our records.',

]);

}

  

public function showLoginForm()

{

return view('login');

}

  

public function logout(Request $request)

{

Auth::logout();

  

$request->session()->invalidate();

$request->session()->regenerateToken();

  

return redirect('/');

}

  

public function register(Request $request)

{

$credentials = $request->validate([

'username' => 'required|unique:users|min:3|max:255',

'password' => 'required|min:6|max:255'

]);

try{

User::create([

'username' => $credentials['username'],

'password' => bcrypt($credentials['password']),

]);

return redirect()->route('register_success');

} catch (\Exception $e) {

return back()->withErrors([

'error' => 'An error occurred while creating your account.'

]);

}

}

  

public function showRegistrationForm()

{

return view('register');

}

  
  
  

public function showTopUp(){

return view('topup');

}

  

public function topUp(Request $request){

$request->validate([

'amount' => 'required|numeric|min:1000|max:1000000'

]);

  

/** @var \App\Models\User $user */

$user = Auth::user();

$user->balance += $request->input('amount');

$user->save();

return redirect()->route('topup')->with('success', 'Topup successful');

}

  

public function showRedemptionForm()

{

return view('redemption');

}

  

public function redeemPoints()

{

/** @var \App\Models\User $user */

$user = Auth::user();

$user->points -= 10000;

$user->balance += 10000;

$user->save();

return redirect()->route('redeem')->with('success', 'Points redeemed! New balance: Rp' . number_format($user->balance, 0, ',', '.'));

}

  
  

}
```


```
Controller.php
<?php

  

namespace App\Http\Controllers;

  

use Illuminate\Foundation\Auth\Access\AuthorizesRequests;

use Illuminate\Foundation\Bus\DispatchesJobs;

use Illuminate\Foundation\Validation\ValidatesRequests;

use Illuminate\Routing\Controller as BaseController;

  

class Controller extends BaseController

{

use AuthorizesRequests, DispatchesJobs, ValidatesRequests;

}
```

```
ProductController.php
<?php

  

namespace App\Http\Controllers;

  

use Illuminate\Http\Request;

use App\Models\Product;

use App\Models\ProductCategory;

  

class ProductController extends Controller

{

public function showProducts(){

$products = Product::paginate(6);

$numberOfProducts = Product::count();

  

return view('home')->with([

'products' => $products,

'numberOfProducts' => $numberOfProducts

]);

}

  

public function showProductsOfCategory($id){

$products = Product::where('category_id', $id)->get();

$numberOfProducts = $products->count();

  

return view('category')->with([

'products' => $products,

'numberOfProducts' => $numberOfProducts

]);

}

  

public function showProduct($id){

$product = Product::find($id);

  

return view('product')->with([

'product' => $product

]);

}

public function purchaseProduct(Request $request, $id){

$product = Product::find($id);

$user = $request->user();

$quantity = $request->quantity ?? 1;

$totalPrice = $product->price * $quantity;

  

if($user->balance < $totalPrice){

return back()->withErrors([

'error' => 'You do not have enough balance to purchase this product.'

]);

}

  

$user->balance -= $totalPrice;

$user->points += $totalPrice/100;

$user->save();

  

$product->stock -= $quantity;

$product->save();

  

// Create purchase without user_id

$user->purchases()->create([

'customer_id' => $user->id, // use customer_id, not user_id

'product_id' => $product->id,

'quantity' => $quantity

]);

  

return redirect()->route('product', $product->id)->with([

'success' => 'Product purchased., You gained ' . $totalPrice/100 . ' points.'

]);

}

  
  

public function showUploadForm(){

$categories = ProductCategory::all();

  

return view('uploadProduct')->with([

'categories' => $categories

]);

}

public function uploadProduct(Request $request){

$request->validate([

'name' => 'required|string| max:255',

'category_id' => 'required|numeric',

'price' => 'required|numeric|min:1000|max:200000',

'stock' => 'required|numeric',

'image' => 'required|image'

]);

  

$imagePath = 'storage/' . $request->file('image')->storeAs(

'img/products',

uniqid() . '.' . $request->file('image')->extension(),

'public'

);

Product::create([

'name' => $request->name,

'category_id' => $request->category_id,

'price' => $request->price,

'stock' => $request->stock,

'imageURL' => $imagePath

]);

  

return back()->with([

'success' => 'Product uploaded.'

]);

  

}

  
  
  

public function searchProduct(Request $request){

  
  

$keyword = $request->query('keyword');

$products = Product::where('name', 'like', '%' . $keyword . '%')->get();

$numberOfProducts = $products->count();

  

return view('search')->with([

'products' => $products,

'numberOfProducts' => $numberOfProducts,

'keyword' => $keyword

]);

}

  

}
```

```
AdminMiddleware.php
<?php

  

namespace App\Http\Middleware;

  

use Closure;

use Illuminate\Http\Request;

use Illuminate\Support\Facades\Auth;

  

class AdminMiddleware

{

/**

* Handle an incoming request.

*

* @param \Illuminate\Http\Request $request

* @param \Closure(\Illuminate\Http\Request): (\Illuminate\Http\Response|\Illuminate\Http\RedirectResponse) $next

* @return \Illuminate\Http\Response|\Illuminate\Http\RedirectResponse

*/

public function handle(Request $request, Closure $next)

{

if (!Auth::check() || Auth::user()->id !== 16) {

abort(403, 'Unauthorized access.');

}

  

return $next($request);

}

}
```

```
Product.php
<?php

  

namespace App\Models;

  

use Illuminate\Database\Eloquent\Factories\HasFactory;

use Illuminate\Database\Eloquent\Model;

  

class Product extends Model

{

use HasFactory;

  

protected $fillable = ['name', 'category_id', 'price', 'stock', 'imageURL'];

  

public function purchases()

{

return $this->belongsTo(Purchases::class);

}

  

public function productCategory()

{

return $this->belongsTo(ProductCategory::class, 'category_id');

}

}
```

```
ProductCategory.php
<?php

  

namespace App\Models;

  

use Illuminate\Database\Eloquent\Factories\HasFactory;

use Illuminate\Database\Eloquent\Model;

  

class ProductCategory extends Model

{

use HasFactory;

  

public function products()

{

return $this->hasMany(Product::class);

}

}
```

```
Purchases.php
<?php

  

namespace App\Models;

  

use Illuminate\Database\Eloquent\Factories\HasFactory;

use Illuminate\Database\Eloquent\Model;

  

class Purchases extends Model

{

use HasFactory;

  

protected $fillable = [

'customer_id',

'product_id',

'quantity',

];

  

public function customer()

{

return $this->belongsTo(User::class);

}

public function product()

{

return $this->belongsTo(Product::class);

}

}
```

```
create users table
<?php

  

use Illuminate\Database\Migrations\Migration;

use Illuminate\Database\Schema\Blueprint;

use Illuminate\Support\Facades\Schema;

  

return new class extends Migration

{

/**

* Run the migrations.

*

* @return void

*/

public function up()

{

Schema::create('users', function (Blueprint $table) {

$table->id();

$table->string('username')->unique();

$table->string('password');

$table->integer('balance')->default(10000);

$table->integer('points')->default(0);

$table->timestamps();

});

}

  

/**

* Reverse the migrations.

*

* @return void

*/

public function down()

{

Schema::dropIfExists('users');

}

};
```

```
create product categories table
<?php

  

use Illuminate\Database\Migrations\Migration;

use Illuminate\Database\Schema\Blueprint;

use Illuminate\Support\Facades\Schema;

  

return new class extends Migration

{

/**

* Run the migrations.

*

* @return void

*/

public function up()

{

Schema::create('product_categories', function (Blueprint $table) {

$table->id();

$table->string('category_name');

$table->timestamps();

});

}

  

/**

* Reverse the migrations.

*

* @return void

*/

public function down()

{

Schema::dropIfExists('product_categories');

}

};
```

```
create products table
<?php

  

use Illuminate\Database\Migrations\Migration;

use Illuminate\Database\Schema\Blueprint;

use Illuminate\Support\Facades\Schema;

  

return new class extends Migration

{

/**

* Run the migrations.

*

* @return void

*/

public function up()

{

Schema::create('products', function (Blueprint $table) {

$table->id();

$table->string('name');

$table->foreignId('category_id')->constrained('product_categories');

$table->integer('price');

$table->integer('stock');

$table->string('imageURL');

$table->timestamps();

});

}

  

/**

* Reverse the migrations.

*

* @return void

*/

public function down()

{

Schema::dropIfExists('products');

}

};
```

```
create purchases table
<?php

  

use Illuminate\Database\Migrations\Migration;

use Illuminate\Database\Schema\Blueprint;

use Illuminate\Support\Facades\Schema;

  

return new class extends Migration

{

/**

* Run the migrations.

*

* @return void

*/

public function up()

{

Schema::create('purchases', function (Blueprint $table) {

$table->id();

$table->foreignId('customer_id')->constrained('users');

$table->foreignId('product_id')->constrained('products');

$table->integer('quantity');

$table->timestamps();

});

}

  

/**

* Reverse the migrations.

*

* @return void

*/

public function down()

{

Schema::dropIfExists('purchases');

}

};
```

```
database seeder
<?php

  

namespace Database\Seeders;

  

// use Illuminate\Database\Console\Seeds\WithoutModelEvents;

use Illuminate\Database\Seeder;

  

class DatabaseSeeder extends Seeder

{

/**

* Seed the application's database.

*

* @return void

*/

public function run()

{

$this->call([

ProductCategorySeeder::class,

ProductSeeder::class,

UserSeeder::class,

]);

}

}
```

```
productcategory seeder
<?php

  

namespace Database\Seeders;

  

use Illuminate\Database\Console\Seeds\WithoutModelEvents;

use Illuminate\Database\Seeder;

use Illuminate\Support\Facades\DB;

  

class ProductCategorySeeder extends Seeder

{

/**

* Run the database seeds.

*

* @return void

*/

public function run()

{

//

DB::table('product_categories')->insert([

['category_name' => 'Snacks'],

['category_name' => 'Soft Drinks'],

['category_name' => 'Cookies']

]);

}

}
```

```
product seeder
<?php

  

namespace Database\Seeders;

  

use Illuminate\Database\Console\Seeds\WithoutModelEvents;

use Illuminate\Database\Seeder;

  

use Illuminate\Support\Facades\DB;

use Faker\Factory as Faker;

  

class ProductSeeder extends Seeder

{

/**

* Run the database seeds.

*

* @return void

*/

public function run()

{

$faker = Faker::create();

foreach (range(1, 20) as $index) {

$categoryId = rand(1, 3);

DB::table('products')->insert([

'name' => $faker->words(2, true),

'category_id' => $categoryId,

'price' => rand(10,40)*500,

'stock' => rand(0, 100),

'imageURL' => "img/products/product-" . $categoryId . ".jpg"

]);

}

}

}
```

```
purchases seeder.php
<?php

  

namespace Database\Seeders;

  

use Illuminate\Database\Console\Seeds\WithoutModelEvents;

use Illuminate\Database\Seeder;

  

class PurchasesSeeder extends Seeder

{

/**

* Run the database seeds.

*

* @return void

*/

public function run()

{

//

}

}
```

```
UserSeeder.php
<?php

  

namespace Database\Seeders;

  

use Illuminate\Database\Console\Seeds\WithoutModelEvents;

use Illuminate\Database\Seeder;

use App\Models\User;

use Illuminate\Support\Facades\Hash;

  

class UserSeeder extends Seeder

{

/**

* Run the database seeds.

*

* @return void

*/

public function run()

{

for ($i = 1; $i <= 5; $i++) {

User::create([

'username' => 'customer #' . $i,

'password' => Hash::make('password__#' . $i * 100)

]);

}

  

$RandomNames = ['John', 'Doe', 'Jane', 'Smith', 'Michael', 'Jordan', 'Lebron', 'James', 'Kobe', 'Bryant'];

  

for ($i = 1; $i <= 10; $i++) {

User::create([

'username' => $RandomNames[rand(0, 9)] . '_' . $RandomNames[rand(0, 9)] . rand(1, 100),

'password' => Hash::make('password__#' . $i * 100)

]);

}

}

}
```

```
<?php

  

return [

  

/*

|--------------------------------------------------------------------------

| Authentication Language Lines

|--------------------------------------------------------------------------

|

| The following language lines are used during authentication for various

| messages that we need to display to the user. You are free to modify

| these language lines according to your application's requirements.

|

*/

  

'failed' => 'These credentials do not match our records.',

'password' => 'The provided password is incorrect.',

'throttle' => 'Too many login attempts. Please try again in :seconds seconds.',

  

];
```

```
category.blade.php
@extends('main')

  

@section('content')

<!-- skibidi home content <br> -->

  

<div class="container">

<div class="row">

<div class="col-12 mb-3 h3 ">

Category = {{$products->first()->productCategory->category_name}} <br>

Total number of products = {{ $numberOfProducts }}

</div>

</div>

<div class="row">

@foreach ($products as $product)

<div class="col-md-3 mb-4 d-flex justify-content-center">

<div class="card w-100">

<img src="{{url($product->imageURL)}}" class="card-img-top" style="height: 200px; width: 100%; object-fit: cover;" alt="...">

<div class="card-body">

<h5 class="card-title">{{$product->name}} {{$product->id}}</h5>

<p class="card-text">

Price = {{$product->price}} <br>

Stock = {{$product->stock}}

</p>

<a href="{{ url('product/' . $product->id) }}" class="btn btn-primary">Product detail</a>

</div>

</div>

</div>

@endforeach

</div>

</div>

  

@endsection
```


```
home.blade.php
@extends('main')

  

@section('content')

<!-- skibidi home content <br> -->

  

<div class="container">

<div class="row">

<div class="col-12 mb-3 h3 ">

Total number of products = {{ $numberOfProducts }}

</div>

</div>

<div class="row">

@foreach ($products as $product)

<div class="col-md-3 mb-4 d-flex justify-content-center">

<div class="card w-100">

<img src="{{ url($product->imageURL) }}" class="card-img-top" style="height: 200px; width: 100%; object-fit: cover;" alt="...">

<div class="card-body">

<h5 class="card-title">{{$product->name}} {{$product->id}}</h5>

<p class="card-text">

{{$product->productCategory->category_name}}<br>

Price = {{$product->price}} <br>

Stock = {{$product->stock}}

</p>

<a href="{{route('product', $product->id)}}" class="btn btn-primary">Product detail</a>

</div>

</div>

</div>

@endforeach

</div>

</div>

  

<nav aria-label="Page navigation" class="mt-3 ms-auto d-flex justify-content-end">

{{ $products->links('pagination::bootstrap-5') }}

</nav>

  
  

@endsection
```

```
login.blade.php
@extends('main')

  

@section('content')

<div class="container w-50">

<h2 class="text-center">Log in to your account</h1>

  

<form method="POST" action="{{ route('login') }}">

@csrf

<!-- Username Input -->

<div class="">

<label for="username" class="form-label fs-5">Username:</label>

<input type="text" id="username" name="username" class="form-control" required value="{{ old('username') }}">

@error('username')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

  

<!-- Password Input -->

<div class="mt-3">

<label for="password" class="form-label fs-5">Password:</label>

<input type="password" id="password" name="password" class="form-control" required>

@error('password')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

  

<!-- General error message -->

@if($errors->has('error'))

<div class="text-danger mt-2">{{ $errors->first('error') }}</div>

@endif

  

<!-- Submit Button -->

<div class="text-center mt-2">

<button type="submit" class="btn btn-primary fw-bold px-4 fs-5 mt-4">Login</button>

</div>

  

</form>

  
  

</div>

@endsection
```

```
main.blade.php
<!DOCTYPE html>

<html lang="en" class="h-100">

  

<head>

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link rel="stylesheet" href="/bootstrap/bootstrap.min.css">

<script src="/bootstrap/bootstrap.bundle.min.js"></script>

  

</head>

  

<body class="d-flex flex-column h-100" data-bs-theme="dark">

<header>

<nav class="navbar navbar-expand-lg bg-body-tertiary">

<div class="container-fluid">

<a class="navbar-brand" href="#">Navbar</a>

<button class="navbar-toggler" type="button" data-bs-toggle="collapse"

data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"

aria-expanded="false" aria-label="Toggle navigation">

<span class="navbar-toggler-icon"></span>

</button>

<div class="collapse navbar-collapse" id="navbarSupportedContent">

<ul class="navbar-nav me-auto mb-2 mb-lg-0">

<li class="nav-item">

<a class="nav-link" href="/home">Home</a>

</li>

<li class="nav-item">

<a class="nav-link" href="/category/1">Snacks</a>

</li>

<li class="nav-item">

<a class="nav-link" href="/category/2">Soft Drinks</a>

</li>

<li class="nav-item">

<a class="nav-link" href="/category/3">Cookies</a>

</li>

</ul>

  

<form class="d-flex" role="search" method="GET" action="{{ route('search') }}">

<input class="form-control me-2 w-100" type="search" placeholder="Search" aria-label="Search" name="keyword">

<button class="btn btn-outline-success" type="submit">Search</button>

</form>

  

<ul class="d-flex navbar-nav ms-auto mb-2 mb-lg-0">

<!-- placeholder section for buttons -->

@auth

<span class="navbar-text text-white me-2">

You're logged in,

Your name is {{ Auth::user()->username }}

</span>

<li class="nav-item">

<a class="nav-link" href="/topup">Top up</a>

</li>

<li class="nav-item">

<a class="nav-link" target="_blank" href="/redeem">Redeem points</a>

</li>

@if (Auth::user()->id == 16)

<li class="nav-item">

<span class="nav-link fw-bold">You are admin</span>

</li>

<li class="nav-item">

<a class="nav-link" href="/upload">Upload</a>

</li>

@endif

  

<li class="nav-item">

<form method="POST" action="{{ route('logout') }}">

@csrf

<button type="submit" class="btn btn-danger"> Logout</button>

</form>

</li>

@endauth

  

@guest

<span class="navbar-text text-white me-2">

Go log in fool

</span>

<li class="nav-item">

<a class="nav-link" href="/login">Login</a>

</li>

<li class="nav-item">

<a class="nav-link" href="/register">Register</a>

</li>

@endguest

</ul>

</div>

</div>

</nav>

</header>

  

<main class="flex-grow-1">

<div class="container py-3 bg-body-secondary h-100">

@yield('content')

<!-- example text -->

<!-- put content here -->

</div>

</main>

  

<footer class="footer mt-auto py-3 bg-body-tertiary">

<div class="text-center">

2042 &copy; Footer here

  

</div>

</footer>

</body>

  

</html>
```

```
product.blade.php
@extends('main')

  

@section('content')

<!-- skibidi home content <br> -->

  

<div class="container">

<div class="h1">{{$product->name}} <br></div>

<div class="h5 mb-4">Part of {{$product->productCategory->category_name}}</div>

<img src="{{url($product->imageURL)}}" class="img-fluid" style="height: 200px; width: 50%; object-fit: cover;" alt="..."><br>

  

Available stock = {{$product->stock}}<br>

Price per unit = Rp {{number_format($product->price,0,'.',',')}}<br>

  

Purchase product

@if($product->stock == 0)

<div class="alert alert-danger mt-3" role="alert">

Product is out of stock.

</div>

@else

@auth

Your current balance = Rp {{number_format(Auth::user()->balance,0,'.',',')}}<br>

@if(session('success'))

<div class="alert alert-success mt-3">

{{ session('success') }}

</div>

@endif

@error('error')

<div class="alert alert-danger mt-3">

{{ $message }}

</div>

@enderror

<form action="{{ route('product.purchase', ['id' => $product->id]) }}" method="post">

@csrf

<input type="number" name="quantity" id="quantity" min="1" max="{{$product->stock}}" value="1">

<button type="submit" class="btn btn-primary">Purchase</button>

</form>

@endauth

@endif

  

@guest

<div class="alert alert-danger mt-3" role="alert">

You need to log in to purchase items.

</div>

@endguest

</div>

  

@endsection
```

```
redemption.blade.php
@extends('main')

  

@section('content')

<!-- skibidi home content <br> -->

  

<div class="container">

<span class="h3"> Top up balance</span>

  

@auth

<br>

<span> Your current balance: Rp {{ number_format(Auth::user()->balance, 0, ',', '.') }}</span> <br>

<div class="mb-4"><span> You currently have {{Auth::user()->points}} Points</span></div>

<span> You can redeem points 10000 points for Rp 10.000 </span> <br>

  

@if(session('success'))

<div class="alert alert-success mt-3" role="alert">

{{ session('success') }}

</div>

@endif

  

<form method="POST" action="{{ route('redeem') }}">

@csrf

@if(Auth::user()->points >= 10000)

You have enough points to redeem something <br>

<button type="submit" class="btn btn-primary">Redeem Points</button>

@else

<div class="alert alert-dark mt-4">You do not have enough points.</div>

@endif

</form>

@endauth

  

@guest

<div class="alert alert-danger mt-3" role="alert">

You need to log in to redeem points.

</div>

@endguest

  

</div>

  
  

@endsection
```

```
regitser_successs.blade.php
@extends('main')

  

@section('content')

<div class="m-4 jumbotron text-center">

<h1>Account Registration Successful!</h1>

<p>Your account has been successfully created. You can now <a href="{{ route('login') }}">log in</a>.</p>

</div>

@endsection
```


```
regoister.blade.php
@extends('main')

  

@section('content')

<div class="container w-50">

<h2 class="text-center">Make an account</h1>

  

<form method="POST" action="{{ route('register') }}">

@csrf

<!-- username -->

<div class="">

<label for="username" class="form-label fs-4">Username:</label>

<input type="text" id="username" name="username" class="form-control" required value="{{ old('username') }}">

@error('username')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

  

<!-- pw -->

<div class="">

<label for="password" class="form-label fs-4">Password:</label>

<div class="input-group">

<input type="password" id="password" name="password" class="form-control" required>

</div>

@error('password')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

  

<!-- button -->

<div class="text-center mt-2">

<button type="submit" class="btn btn-primary fw-bold px-4 fs-5 mt-4">Register</button>

</div>

<!-- error msgs -->

@if($errors->has('error'))

<div class="text-danger mt-3">{{ $errors->first('error') }}</div>

@endif

  

</form>

  
  

</div>

@endsection
```

```
search.blade.php
@extends('main')

  

@section('content')

<!-- skibidi home content <br> -->

  

<div class="container">

<div class="row">

<div class="col-12 mb-3 h3 ">

Found {{ $numberOfProducts }} Products with title containing "{{$keyword}}".

</div>

</div>

<div class="row">

@if($numberOfProducts == 0)

<div class="col-12 mb-3 h3 ">

No products found matching search term.

@else

@foreach ($products as $product)

<div class="col-md-3 mb-4 d-flex justify-content-center">

<div class="card w-100">

<img src="{{url($product->imageURL)}}" class="card-img-top" style="height: 200px; width: 100%; object-fit: cover;" alt="...">

<div class="card-body">

<h5 class="card-title">{{$product->name}} {{$product->id}}</h5>

<p class="card-text">

Price = {{$product->price}} <br>

Stock = {{$product->stock}}

</p>

<a href="{{ url('product/' . $product->id) }}" class="btn btn-primary">Product detail</a>

</div>

</div>

</div>

@endforeach

@endif

</div>

</div>

  

@endsection
```

```
topup.blade.php
@extends('main')

  

@section('content')

<!-- skibidi home content <br> -->

  

<div class="container">

<span class="h3"> Top up balance</span>

  

@auth

<span> Your current balance: Rp {{ number_format(Auth::user()->balance, 0, ',', '.') }}</span>

  

@if(session('success'))

<div class="alert alert-success mt-3" role="alert">

{{ session('success') }}

</div>

@endif

  

<form method="POST" action="{{ route('topup') }}">

@csrf

<div class="mb-3">

<label for="amount" class="form-label">Amount to top up (1k to 1Mill):</label>

<input type="number" class="form-control" id="amount" name="amount" required>

@error('amount')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

<button type="submit" class="btn btn-primary">Top up</button>

</form>

@endauth

  

@guest

<div class="alert alert-danger mt-3" role="alert">

You need to log in to top up your balance.

</div>

@endguest

  

</div>

  
  

@endsection
```


```
uploadprodyctblade.php
@extends('main')

  

<!-- (name) Name of product > text box

(category_id) Category of product > dropdown menu

(price) Price > number

(stock) Stock > number

(imageURL) Image > image upload, rename and then store in -->

  

@section('content')

<div class="container w-50">

<h2 class="text-center">Insert new product</h1>

  

@if(session('success'))

<div class="alert alert-success mt-3">

{{ session('success') }}

</div>

@endif

  

<form method="POST" action="{{ route('upload.submit') }}" enctype="multipart/form-data">

@csrf

<!-- Name of product -->

<div class="">

<label for="name" class="form-label fs-5">Name of product:</label>

<input type="text" id="name" name="name" class="form-control" required value="{{ old('name') }}">

@error('name')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

<!-- Category of product -->

<div class="mt-3">

<label for="category_id" class="form-label fs-5">Category of product:</label>

<select id="category_id" name="category_id" class="form-select" required>

<option value="">Select category</option>

@foreach ($categories as $category)

<option value="{{ $category->id }}" {{ old('category_id') == $category->id ? 'selected' : '' }}>

{{ $category->category_name }}

</option>

@endforeach

</select>

@error('category_id')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

  

<!-- Price & stock -->

<div class="mt-3">

<div class="row">

<div class="col">

<label for="price" class="form-label fs-5">Price:</label>

<input type="number" id="price" name="price" class="form-control" required value="{{ old('price') }}">

@error('price')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

<div class="col">

<label for="stock" class="form-label fs-5">Stock:</label>

<input type="number" id="stock" name="stock" class="form-control" required value="{{ old('stock') }}">

@error('stock')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

</div>

</div>

  

<!-- Image -->

<div class="mt-3">

<label for="image" class="form-label fs-5">Image:</label>

<input type="file" id="image" name="image" class="form-control" required accept="image/*">

@error('image')

<div class="text-danger mt-2">{{ $message }}</div>

@enderror

</div>

  

<!-- Submit button -->

<div class="text-center mt-2">

<button type="submit" class="btn btn-primary fw-bold px-4 fs-5 mt-4">Insert</button>

</div>

  
  
  

</form>

  
  

</div>

@endsection
```

```
web.php
<?php

  

use Illuminate\Support\Facades\Route;

use App\Http\Controllers\AccountController;

use App\Http\Controllers\ProductController;

/*

|--------------------------------------------------------------------------

| Web Routes

|--------------------------------------------------------------------------

|

| Here is where you can register web routes for your application. These

| routes are loaded by the RouteServiceProvider within a group which

| contains the "web" middleware group. Now create something great!

|

*/

  

Route::get('/', [ProductController::class, 'showProducts']);

  
  

Route::get('/home', [ProductController::class, 'showProducts']);

  
  

Route::get('/main', function () {

return view('main');

});

  
  

Route::get('/login', [AccountController::class, 'showLoginForm'])->name('login');

Route::post('/login', [AccountController::class, 'login']);

  

Route::post('/logout', [AccountController::class, 'logout'])->name('logout');

  
  

Route::get('/register', [AccountController::class, 'showRegistrationForm'])->name('register');

Route::post('/register', [AccountController::class, 'register']);

  

Route::get('/register_success', function () {

return view('register_success');

})->name('register_success');

  

Route::get('/topup', [AccountController::class, 'showTopUp'])->name('topup');

Route::post('/topup', [AccountController::class, 'topUp']);

  

Route::get('/category/{id}', [ProductController::class, 'showProductsOfCategory']);

  
  

Route::get('/redeem', [AccountController::class, 'showRedemptionForm'])->name('redeem');

Route::post('/redeem', [AccountController::class, 'redeemPoints']);

  
  

Route::get('/product/{id}', [ProductController::class, 'showProduct'])->name('product');

Route::post('/product/{id}/purchase', [ProductController::class, 'purchaseProduct'])->name('product.purchase');

  

Route::middleware(['admin'])->group(function () {

Route::get('/upload', [ProductController::class, 'showUploadForm'])->name('upload.form');

Route::post('/upload', [ProductController::class, 'uploadProduct'])->name('upload.submit');

});

  

Route::get('/search', [ProductController::class, 'searchProduct'])->name('search');
```