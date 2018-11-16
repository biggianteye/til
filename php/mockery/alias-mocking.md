# alias mocking

The Mockery library and dependency injection allow you to mock external dependencies such as databases and filesystems. This is great, but doesn't work if that dependency is being called statically within the code you want to test.

Imagine this scenario:

```php
class Foo {
    public function __construct(Database $db = null) {

        // ...

        Database::someDatabaseStuff(...);
    }
}
```

and

```php
function testFoo() {
    $foo = new Foo(Mockery::mock(Database::class));
    // ...
}
```

Even though you did the right thing and mocked the `Database` class, any `Foo` tests will fail if there is no database available (and there shouldn't be in unit tests) because of the explicit static call in the constructor.

Alias mocking to the rescue.

```php
function testFoo() {
    $db = Mockery::mock('alias:Database');
    $db->shouldReceive('someDatabaseStuff');

    $foo = new Foo($db);
    // ...
}
```

This will route *all* calls to `Database` through the mock. This will work as it if run standalone, but if you want to run it alongside other tests you have to add these annotations to each test:

```
@runInSeparateProcess
@preserveGlobalState disabled
```

More details here: https://blog.gougousis.net/mocking-static-methods-with-mockery/

The Mockery [documentation](http://docs.mockery.io/en/latest/reference/creating_test_doubles.html#aliasing) does not recommend using aliasing, but it was a neat solution to the problem I had.
