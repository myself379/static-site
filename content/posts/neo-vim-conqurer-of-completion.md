---
title: "neo-vim Conquerer of Completion"
date: 2020-08-22T10:56:26+08:00
draft: true
---

Toyed around with Conquerer of Completion ( [coc.nvim](https://github.com/neoclide/coc.nvim) ) language server. This one of the best language server plug ins created for vim/neo-vim. It is a joy to bring IDE-like suggestions.


```json
{
    "languageserver": {
        "intelephense": {
            "enable": true,
            "command": "intelephense",
            "args": ["--stdio"],
            "filetypes": ["php"],
            "initializationOptions": {
                "storagePath": "/tmp/intelephense"
            }
        },
        "settings": {
            "intelephense": {
                "files": {
                    "maxSize": 1000000,
                    "associations": ["*.php", "*.phtml"]
                },
                "completion": {
                    "insertUseDeclaration": true,
                    "fullyQualifyGlobalConstantsAndFunctions": false,
                    "triggerParameterHints": true,
                    "maxItems": 15
                },
                "format": {
                    "enable": true
                }
            }
        }
    }
}
```

For Laravel projects. An IDE-helper is needed to installed. You can get it by using

This is because Laravel hides its implementation behind a Facade. That is why you can use things like `Route::get()` in `route.php` and `Eloquent` syntaxes in your `Controllers` such as the following examples

```php
<?php
public function index() {
User::get();
}
?>
```

Each facade implementation are called via the `__callStatic()` and Laravel simply pulled out the existing Singleton from the bags of Inversion of Control (IoC) container. Simply put, IoC is the implementation of Dependency Injection.

With this Facades, we developers simply use the functionality provides by Laravel applications, which makes us easily write fluent codes.

Due to this implementation, IDE unable to map the underlying facade. Hence to solve that issue, we need a way to build the "bridge" that allow the IDE to connect the dots and make its way into `vendor/laravel/illuminate`.

Lucky for us, Barryvdh has thought of one solution for us, by generate an IDE helper class that allow IDE to reads the contents and maps into the underlying Laravel implementation.

Simply install `barryvdh/laravel-ide-helper` and configure it.

```bash
composer require --dev barryvdh/laravel-ide-helper
```

You can prevent Laravel auto-discovery mechanism to detect laravel-ide-helper. This is useful when you're pushing to production.


In your `composer.json`. Add the following
```json
{
    "extra": {
        "laravel": {
            "dont-discover": [
                "barryvdh/laravel-ide-helper"
            ]
        }
    }
}
```

Then, for the `laravel-ide-helper` to work, it is needed to be loaded into providers. Add the following class into `config/app.php`

```php
<?php
Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,
?>
```

Alternatively, if you're using Lumen. Add into the following service provider

```php
<?php
public function register() {
    if ($this->app->environment() !== 'production') {
        $this->app->register(\Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class)
    }
}
?>
```

That is it! Now every IDE would not be squawking for error messages in your `routes.php` and `route/web.php` or `User::get()` in your controllers
