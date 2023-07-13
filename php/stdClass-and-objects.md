# `stdClass` and objects

`stdClass` is not the base class of all PHP classes.

Unlike other languages that have classes and objects, all PHP classes are
independent of each other apart from classes they extend.

This means that you can't used `stdClass` as a type hint for a function
that takes any class.

Example that will not work:

```php
function foo(stdClass $bar) {
    // ...
}
```

PHP 7.2 introduced the `object` type hint which *can* be used for this
purpose.

<https://stackoverflow.com/questions/7839059/type-hinting-for-any-object>
