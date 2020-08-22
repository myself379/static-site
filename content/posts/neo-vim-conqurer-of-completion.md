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
