---
layout: default
title: File Storage
parent: Laravel
nav_order: 3
---

# File Storage

PHP
{: .label .label-blue }

Reference Manual
{: .label .label-yellow }

@see [Laravel File Storage docs](https://laravel.com/docs/master/filesystem)

## How to store and access files

The `public` disk included in your application's `filesystems` configuration file is intended for files that are going to be publicly accessible. By default, the `public` disk uses the `local` driver and stores its files in `storage/app/public`.

To make these files accessible from the web, you should create a symbolic link from `public/storage` to `storage/app/public`. Symbolic links are configured in `/config/filesystems.php`, to create the symlinks run the command `php artisan storage:link`, note that if you are running the application inside a container the command must be run from inside the container otherwise the link will be broken.

### Code example on how to store an image

#### File System configuration file

```php
<?php

return [
    ...

    'links' => [
        public_path('storage') => storage_path('app/public'),
    ],
];
```

#### Route

```php
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\ImageController;

Route::group([
    "prefix" => "image",
    "controller" => ImageController::class],
    function() {
        Route::post(
            '',
            'create'
        )->name('createImage');

        Route::delete(
            '{id}',
            'delete'
        )->name('deleteImage');
    }
);
```

#### Controller

```php
<?php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Http\Response;
use Illuminate\Http\JsonResponse;

use App\Models\Image;

class ImageController extends Controller
{
    public function create(Request $request): JsonResponse
    {
        // Stores the image in storage/app/public/images/
        // $path will be equal to "images/<image-name>"
        $path = $request->file('image')->store('images', 'public');
        // Get the url at which the image can be publicly accessed
        // (in the public/storage directory where the symlink to
        // storage/app/public was created)
        $url = asset('storage/'.$imagePath);

        // Insert an image record in the DB.
        $image = Image::create([
            'path' => $path,
            'url' => $url
        ]);

        return response()->json($image, Response::HTTP_CREATED);
    }

    public function delete(Image $image): JsonResponse
    {
        $path = storage_path('app/public/').$image->path;

        $image->delete(); // Delete the image record from the DB.

        if (file_exists($path))
            unlink($path); // Delete the file.

        return response()->json(null, Response::HTTP_NO_CONTENT);
    }
}
```
