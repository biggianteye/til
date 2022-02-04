# Underscore imports

In git you can use an underscore (`_`) for variables or function return values that you want to ignore. The same syntax can be applied to import statements. eg.

```git
import (
	"database/sql"
	_ "github.com/go-sql-driver/mysql"
)
```

What's the point of importing something and ignoring it? Because you want access to side effects via the `init()` function in the package.

> [Why we import SQL drivers as the blank identifier ( _ ) in Go](https://www.calhoun.io/why-we-import-sql-drivers-with-the-blank-identifier/)

The above article explains the situation well, but the basic gist in this example is that the `database/sql` package contains general code but no implementation for any specific database engine. The `init()` function in the mysql package registers itself as a concrete implementation of the database code.

Following on from that, this question explains where `init()` fits into the sequence of execution.

> [When is the init() function run?](https://stackoverflow.com/questions/24790175/when-is-the-init-function-run)

This image from one of the answers shows with great clarity the sequence of things that get executed before the `main()` function.

![image showing the execution order in golang](init.png)

I mentioned databases above, but this pattern can be used in many other circumstances eg. image processing libraries.