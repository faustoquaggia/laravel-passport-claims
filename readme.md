# laravel-passport-claims

[![Latest Version on Packagist][ico-version]][link-packagist]
[![Total Downloads][ico-downloads]][link-downloads]

This package allows you to add claims to Laravel Passport JWT Tokens. If you have questions or comments, please open an issue. 

## Installation

Via Composer

``` bash
$ composer require corbosman/laravel-passport-claims
```

To collect all the claims, this package sends the access token through a pipeline of classes. Each class adds a claim to the token. For each claim that you want to add, you need to create a class like the example below. Because the AccessToken is sent through the pipeline, you have access to methods on the AccessToken class. This is useful if you want to derive information from the token. For instance, look up user data based on the token user identifier.  

```php
<?php

namespace App\Claims;

class CustomClaim
{
    public function handle($token, $next)
    {
        $token->addClaim('my-claim', 'my custom claim data');

        return $next($token);
    }
}
```

To tell this package which claims you want to add, you need to publish the config file and add a list of all your classes. To publish the config file, run the following command after installing this package. 

```shell
php artisan vendor:publish --provider="CorBosman\Passport\ServiceProvider"
```

The config file will look like this.

```php
<?php

return [
    /*
    |--------------------------------------------------------------------------
    | JWT Claim Classes
    |--------------------------------------------------------------------------
    |
    | Here you can add an array of classes that will each be called to add
    | claims to the passport JWT token. See the readme for the interface that
    | these classes should adhere to.
    |
    */
    'claims' => [
        App\Claims\MyCustomClaim::class,
        App\Claims\MyOtherCustomClaim::class
    ]
];
```

## Change log

Please see the [changelog](changelog.md) for more information on what has changed recently.

## Contributing

Please see [contributing.md](contributing.md) for details.

## Security

If you discover any security related issues, please email author email instead of using the issue tracker.

## Credits

- [Cor Bosman][link-author]

## License

Please see the [license file](license.md) for more information.

[ico-version]: https://img.shields.io/packagist/v/corbosman/laravel-passport-claims.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/corbosman/laravel-passport-claims.svg?style=flat-square
[ico-styleci]: https://styleci.io/repos/12345678/shield

[link-packagist]: https://packagist.org/packages/corbosman/laravel-passport-claims
[link-downloads]: https://packagist.org/packages/corbosman/laravel-passport-claims
[link-styleci]: https://styleci.io/repos/12345678
[link-author]: https://github.com/corbosman
