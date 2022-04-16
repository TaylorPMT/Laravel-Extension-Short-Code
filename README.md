
![Logo](https://baqirfarooq.files.wordpress.com/2016/09/shortcodes.jpg)


# Laravel-Shortcodes




## Installation 

You can install the package via composer:

```composer
composer require taylorpmt/short-code
```
After updating composer, add the ServiceProvider to the providers array in config/app.php


**Required** 

---
1.  **illuminate/view 5.6+**
2.  **illuminate/support 5.6+**
3.  **illuminate/contracts 5.6+**
4.  **PHP 7.2+** 

## Usage
```php
Taylorpmt\ShortCode\Providers\ShortcodesServiceProvider::class
```
You can use the facade for shorter code. Add this to your aliases:
```php
'Shortcode' => Taylorpmt\ShortCode\Facades\Shortcode::class,
```
OR you can use the AppServiceProvider register for shorter code . 
```php
<?php

namespace App\Providers;

use Taylorpmt\ShortCode\Facades\Shortcode;
use Taylorpmt\ShortCode\Providers\ShortcodesServiceProvider;
use Illuminate\Foundation\AliasLoader;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Register any application services.
     *
     * @return void
     */
    public function register()
    {   
        $this->app->register(ShortcodesServiceProvider::class);
        $loader = AliasLoader::getInstance();
        $loader->alias('Shortcode', Shortcode::class);
    }

}

```
## Usage


*create File BlockSingleShortCode.php*
```php
<?php

namespace CMS\Page\Repository\Shortcode;


class BlockSingleShortCode
{
    const short_code_name = 'category-item';

    /*
        Shortcode register in providers 
    */
    public function register($shortcode, $content, $compiler, $name, $viewData)
    {
       // Logic code 
    }
}
```
Register ShortCode in providers
```php
<?php

namespace CMS\Page\Providers;

use Illuminate\Support\ServiceProvider;
use Shortcode;
use CMS\Page\Repository\Shortcode\BlockSingleShortCode;

class PageProviders extends ServiceProvider
{
    public function register()
    {
        Shortcode::register(BlockSingleShortCode::short_code_name, BlockSingleShortCode::class);
    }
}

```

## Shortcode compiling
**Defining An Accessor**
To define an accessor, create a getDataContentAttribute method on your model of the column you wish to access. 
In this example, we'll define an accessor for the data_content attribute. 
The accessor will automatically be called by Eloquent when attempting to retrieve the value of data_content:
```
public function getDataContentAttribute()
{
    return Shortcode::compile($data['data_content']);
}
```
## Reference source
[webwizo/laravel-shortcodes ](https://github.com/webwizo/laravel-shortcodes)
