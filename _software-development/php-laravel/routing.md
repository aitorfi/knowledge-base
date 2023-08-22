---
layout: default
title: Routing
parent: Laravel
nav_order: 2
---

# Routing

@see [Laravel Routing Docs](https://laravel.com/docs/9.x/routing#parameters-optional-parameters)

In Laravel routes are defined in either the `/routes/api.php` file if you are building an API or in the `/routes/web.php` file if you are building a web app.

Routes defined in the `/routes/api.php` file are accessed at `your-domain/api/route-uri` whereas routes defined in the `/routes/web.php` file are accessed at `your-domain/route-uri`.

## Basic Syntax

To define a route you must call the appropriate static method from the class `Route` according to the HTTP method you want to handle, the available methods are `get`, `post`, `put`, `patch`, `delete` and `options`.

```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::delete($uri, $callback);
```

You can also use methods `match` to register a route that responds to multiple HTTP verbs or `any` to respond to all the HTTP verbs.

```php
Route::match(['get', 'post'], $uri, $callback);
Route::any($uri, $callback);
```

Route methods receive as parameters the URI at which the route can be accessed and a callback or a reference to the method that will be executed when the route is accessed. 

### URI Parameters

Parameters are defined in the URI with the following syntax `/{param-name}` or `/{param-name?}` if it is optional. The parameter values are injected in the callback with the same name.

```php
Route::get('/customer/{id}', function($id) {
    // Do something
});
```

### Route Names

Routes can be assigned names by calling the method `name`.

```php
Route::get($uri, $callback)->name('route-name');
```

The name of a route can be used to generate a URL to that route or to make redirects.

```php
$url = route('route-name'); // Generate URL to route-name

return redirect()->route('route-name'); // Redirect to route-name

return to_route('route-name'); // Redirect to route-name
```

## API Routing Example

```php
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\CustomerController; // Custom Controller class
use App\Models\Customer; // Custom Model class

Route::get(
    'customer/{id}',
    'App\Http\Controllers\CustomerController@getById'
)->name('getCustomerById');

Route::post(
    'customer',
    [CustomerController::class, 'create']
)->name('createCustomer');

Route::put(
    'customer/{customer}',
    [CustomerController::class, 'update']
)->name('updateCustomer');

Route::delete(
    'customer/{customer}',
    function(Customer $customer) {
        new CustomerController()->deleteCustomer();
    }
)->name('deleteCustomer');
```

## Web App Routing Example

```php
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\ViewController; // Custom Controller class

Route::get(
    '/',
    [ViewController::class, 'getHomeView']
)->name('home-view');

Route::get(
    '/products',
    'App\Http\Controllers\ViewController@getProductsView'
)->name('products-view');

Route::get(
    '/order',
    function() {
        return view('order');
    }
)->name('order-view');

Route::view('/customer', 'customer')->name('customer-view');
```
