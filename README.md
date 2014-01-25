php_codesniffer_tests
=====================

Fork of [squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer), but *just* the `AbstractSniffUnitTest` class. Why?

- I didn't want to lose any git commit history for this particular file!
- Now in your `composer.json` you can just 

```
"require": {
    "squizlabs/php_codesniffer_tests": "1.0.0"
}
```

and automatically have access to `AbstractSniffUnitTest` in your unit tests when you `require(__DIR__.'/vendor/autoload.php');`
- allows you to use phpunit xml configuration files and test locally, right in your own standards repo
- hopefully encourages people to write tests for their PHP_CodeSniffer sniffs!

**Differences between this class and the one included with PHP_CodeSniffer:**

- The `runTests()` method is public and marked as a PHPUnit test (ie: `@test`). It also runs **per sniff** automatically, as in only one sniff will be tested with it's corresponding `.inc` file. Makes sense, right?
- `TEST_PATH` (**required**)
    - Because this package is installable via `composer` it's conceptually better to define somewhere, somehow, where your tests are located. Also, it's a bit less nebulous.
- `STANDARD_PATH` (optional)
    - This is specifically for standards that you have not yet officially installed in your instance of `phpcs`. If this const is not defined, the class will use the original method - parse the test class name & assume that everything is in the `phpcs` home dir
- `TEST_EXT` (optional)
    - The original suite **required** all your tests to be `{$SNIFF_NAME}UnitTest.php`. Setting this constant allows you to override the `UnitTest` portion completely, giving you *some* flexibility when organizing your tests.

All of these constants can just be defined in a bootstrap script that requires the composer bootstrap.
eg:
```
<?php
require_once( __DIR__ . '/../vendor/autoload.php' );
define( 'TEST_PATH', __DIR__ . '/Awesomeness' );
define( 'STANDARD_PATH', __DIR__ . '/../Awesomeness' );
define( 'TEST_EXT', 'SniffTest.php' );
```

And, depending on how you run your tests, require this bootstrap script in either your Suite script or `phpunit.xml.dist`
