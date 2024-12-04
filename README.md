# RuoterBaseModel
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


