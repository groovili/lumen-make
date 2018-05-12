# Lumen make
[![Latest Stable Version](https://poser.pugx.org/groovili/lumen-make/v/stable)](https://packagist.org/packages/groovili/lumen-make)
[![Total Downloads](https://poser.pugx.org/groovili/lumen-make/downloads)](https://packagist.org/packages/groovili/lumen-make)
[![License](https://poser.pugx.org/groovili/lumen-make/license)](https://packagist.org/packages/groovili/lumen-make)

A package built for **Lumen** that ports most of the **make commands** from Laravel and adds **Form Request Validation** functionality.

***At the moment package compatible only with Lumen >= 5.6.***

## Installation

Just run the following command
```shell
> composer require groovili/lumen-make
```
or this to enable package only for development needs
```shell
> composer require groovili/lumen-make --dev
```

Uncomment or add this line in ```bootstrap/app.php```
```php
$app->register(App\Providers\EventServiceProvider::class);
```

And add this to ```bootstrap/app.php``` to enable generators
```php
// To enable generator permanently
$app->register(Groovili\LumenMake\LumenMakeServiceProvider::class);

// To enable generator in development mode
if (env('APP_ENV') !== 'production' || env('APP_ENV') === 'local') {
    $app->register(Groovili\LumenMake\LumenMakeServiceProvider::class);
}
```

## Form Request Validation

Add line to ```bootstrap/app.php``` to enable form requests
```php
$app->register(Groovili\LumenMake\Providers\FormRequestServiceProvider::class);
```

Then run 

```shell
> php artisan make:request {name}
```

Below is example of generated request with validation rules:

```php
<?php

declare(strict_types=1);

namespace App\Http\Requests;

use Groovili\LumenMake\Requests\FormRequest;

/**
 * Class FooBarRequest
 * @package App\Http\Requests
 */
class FooBarRequest extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     *
     * @return bool
     */
    public function authorize(): bool
    {
        return true;
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules(): array
    {
        return [
            'foo' => 'bail|required|max:255|min:3',
            'bar' => 'bail|required|max:255|min:3',
        ];
    }
}
```


#### Migrate to Laravel
In generated requests ```Groovili\LumenMake\Requests``` is used. 

If you want migrate to Laravel - change use line in all generated requests:
```php
use Groovili\LumenMake\Requests\FormRequest; 
// change to
use Illuminate\Foundation\Http\FormRequest;
```


### Available commands
* `make:job {name}` - Job class in ```Jobs/```
* `make:console {name}` - Console command in ```Console/Commands/```
* `make:controller {name}` - Restful controller in ```Http/Controllers/```
* `make:model {name}` - Model in ```/```
* `make:middleware {name}` - Middleware class in ```Http/Middleware/```
* `make:exception {name}` - Exception class in ```Exceptions/```
* `make:event {name}` - Event class in ```Events/```
* `make:request {name}` - Request class in ```Http/Requests/```
