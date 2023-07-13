# `utf8` character set

MySQL allows you to specify the character set for text data. It has a
character set called `utf8` which looks like what you should choose if you
want to support Unicode content. Well that's slightly misleading.

At work we are using MySQL 5.6. According to the [documentation](https://dev.mysql.com/doc/refman/5.6/en/charset-unicode-utf8.html),
`utf8` is actually an alias for `utf8mb3`! This explains why emojis from
customer-generated data were not being saved, despite our database tables
in theory supporting Unicode. 🤦🏽‍♂️

Note that the MySQL 8.0 [documentation](https://dev.mysql.com/doc/refman/8.0/en/charset-unicode-utf8.html)
actually says that `utf8mb3` is deprecated:

> The `utf8mb3` character set is deprecated and will be removed in a future
> MySQL release. Please use `utf8mb4` instead. Although `utf8` is currently
> an alias for `utf8mb3`, at some point `utf8` will become a reference to
> `utf8mb4`. To avoid ambiguity about the meaning of `utf8`, consider
> specifying `utf8mb4` explicitly for character set references instead of
> `utf8`.

In conclusion, avoid ambiguity by explicitly using `utf8mb4`.
