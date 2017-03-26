# Install Laravel Ide Helper for [PHPStorm](https://www.jetbrains.com/phpstorm/)

## Where is Laravel Ide Helper?
Github: [barryvdh/laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper)

## Setup
- Install it with composer:

`composer require barryvdh/laravel-ide-helper`
- After updating composer, add the service provider to the providers array in `config/app.php`
```
Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
```
- Publish it:

`php artisan vendor:publish --provider="Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider" --tag=config`
- Regenerate the helper:

`php artisan ide-helper:generate`
- Update the file `config\ide-helper.php`
```
'include_fluent' => true,
```
Now PHPStorm can see the methods in your migrations ;)