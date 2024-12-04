# RouterBaseModel
Laravel v11 Custom Router per each Model perform CRUD and conditions

``` routes/modelName.php ```

``` 

routes/Users.php
routes/Posts.php

```

```

routes/Users.php

<?php

use App\Models\Post;
use Illuminate\Support\Facades\Route;


Route::prefix('posts')
    // ->middleware('auth')
    ->group(function () {
        Route::get('/', function () {

            return "Posts Model Route";

          });

        // Route::get('/create', [PostController::class, 'create'])->name('posts.create');
        // Route::post('/', [PostController::class, 'store'])->name('posts.store');
        // Route::get('/{post}', [PostController::class, 'show'])->name('posts.show');
        // Route::get('/{post}/edit', [PostController::class, 'edit'])->name('posts.edit');
        // Route::put('/{post}', [PostController::class, 'update'])->name('posts.update');
        // Route::delete('/{post}', [PostController::class, 'destroy'])->name('posts.destroy');
    });

```


```

routes/Posts.php

<?php

use App\Models\Post;
use Illuminate\Support\Facades\Route;


Route::prefix('posts')
    // ->middleware('auth')
    ->group(function () {
        Route::get('/', function () {

            return "Posts Model Route";

          });

        // Route::get('/create', [PostController::class, 'create'])->name('posts.create');
        // Route::post('/', [PostController::class, 'store'])->name('posts.store');
        // Route::get('/{post}', [PostController::class, 'show'])->name('posts.show');
        // Route::get('/{post}/edit', [PostController::class, 'edit'])->name('posts.edit');
        // Route::put('/{post}', [PostController::class, 'update'])->name('posts.update');
        // Route::delete('/{post}', [PostController::class, 'destroy'])->name('posts.destroy');
    });

```

``` App\Providers\AppServiceProvider.php ```

```

<?php

namespace App\Providers;

use Illuminate\Foundation\Support\Providers\RouteServiceProvider as ServiceProvider;
use Illuminate\Support\Facades\Route;

class AppServiceProvider extends ServiceProvider
{

     /**
     * The path to the "home" route for your application.
     *
     * @var string
     */
    public const HOME = '/home';

    /**
     * Register any application services.
     */
    public function register(): void
    {
        //
    }

    /**
     * Bootstrap any application services.
     */
    public function boot(): void
    {
        parent::boot();

        // Automatically load model-specific route files
        $this->loadModelRoutes();
    }

     /**
     * Register the model-specific route files.
     *
     * @return void
     */
    protected function loadModelRoutes()
    {
        // Load route files for models
        $models = ['Post', 'User']; // Add more model names here if needed

        foreach ($models as $model) {
            $routeFile = base_path("routes/{$model}.php");

            if (file_exists($routeFile)) {
                // Load the model-specific route file
                Route::middleware('web')
                    ->group($routeFile);
            }
        }
    }

        /**
     * Define the route model bindings for your application.
     *
     * @return void
     */
    public function map()
    {
        //
    }

}


```


<h5>OR</h5>

```

routes/
    posts.php
    product.php
    ...

```

```

// routes/posts.php
use App\Http\Controllers\PostController;

Route::get('/posts', [PostController::class, 'index'])->name('posts.index');
Route::get('/posts/{id}', [PostController::class, 'show'])->name('posts.show');
...


// routes/products.php
use App\Http\Controllers\ProductController;

Route::get('/products', [ProductController::class, 'index'])->name('products.index');
Route::get('/products/{id}', [ProductController::class, 'show'])->name('products.show');
...

```

```

// routes/web.php

// Define the directory where model-specific route files are stored
$routeFiles = glob(base_path('routes') . '/*.php');

// Loop through and include each route file
foreach ($routeFiles as $routeFile) {
    require $routeFile;
}


```

Filter Files (Optional)
If you want to be more specific about which route files to include (e.g., only model-related files), you could create a more specific pattern with glob(). For example, if your route files are grouped by name (e.g., model-posts.php, model-products.php), you could filter for these specific files.

Example:

``` $routeFiles = glob(base_path('routes/model-*.php')); ```

This will only load route files that start with model-.

Route File Naming Convention (Optional)
You may also want to adopt a naming convention for your route files, like model-{model_name}.php. For example:

```

routes/model-posts.php
routes/model-products.php

```

This ensures that only the correct files (those related to models) are included automatically.

Handling Namespaces and Middleware (Optional)
If you want to apply a specific namespace or middleware group to the routes in these model-specific files, you can use route groups within each route file.

For example, in routes/posts.php:

```

// routes/posts.php

use App\Http\Controllers\PostController;

Route::namespace('App\Http\Controllers')->middleware('auth')->group(function () {
    Route::get('/posts', [PostController::class, 'index'])->name('posts.index');
    Route::get('/posts/{id}', [PostController::class, 'show'])->name('posts.show');
});

```

This would apply the auth middleware and the App\Http\Controllers namespace to all the routes in the posts.php file.

Conclusion
By using this dynamic method to include model-specific route files, you can keep your routes clean, organized, and maintainable without manually listing each route file in web.php. The main steps are:

Create route files for each model.
Use glob() to dynamically load those route files.
Optionally, use route grouping to add middleware or namespaces.
This approach is scalable, and as your application grows, you won’t need to modify web.php unless you’re adding new global routes.


<i>Generated by AI</i> 


