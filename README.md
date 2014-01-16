php_codesniffer_tests
=====================

Fork of [squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer), but *just* the `AbstractSniffUnitTest` class. Why?
- Now in your `composer.json` you can just 
```
"require": {
    "squizlabs/php_codesniffer_tests": "*"
}
```
and automatically have access to `AbstractSniffUnitTest` in your unit tests when you `require(__DIR__.'/vendor/autoload.php');`
- hopefully encourages people to write tests for their PHP_CodeSniffer sniffs!
