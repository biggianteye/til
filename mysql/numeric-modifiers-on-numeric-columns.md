# Numeric modifiers on numeric columns

When you specify a value for a numeric column (eg. `int(3)`) it **does not affect storage**. It only affects display when used in conjunction with the `zerofill` property.

The reason this comes as a revelation to me is that in Oracle it *does* restrict storage. So trying to insert `1000` into a `number(3)` would result in this error:

>  `ORA-01438: value larger than specified precision allowed for this column`

Here is an answer to a Stack Overflow question that asks "What is the size of column of int(11) in mysql in bytes?": <https://stackoverflow.com/a/27519793/966703>

The important part from that answer:

> if the value has less digit than 'somenumber', ZEROFILL will prepend zeros.
>
> INT(5) ZEROFILL with the stored value of 32 will show 00032
> INT(5) with the stored value of 32 will show 32
> INT with the stored value of 32 will show 32
>
> if the value has more digit than 'somenumber', the stored value will be shown.
>
> INT(3) ZEROFILL with the stored value of 250000 will show 250000
> INT(3) with the stored value of 250000 will show 250000
> INT with the stored value of 250000 will show 250000

Here is a quick demonstration:

```mysql
mysql> create table mind_blown(what int(1));
mysql> create table mind_blown(what int(1));
mysql>
mysql> insert into mind_blown values (1);
mysql> insert into mind_blown values (10);
mysql> insert into mind_blown values (100);
mysql> insert into mind_blown values (1000);
mysql>
mysql> select * from mind_blown;
+------+
| what |
+------+
|    1 |
|   10 |
|  100 |
| 1000 |
+------+
4 rows in set (0.00 sec)
```

In conclusion, unless you are using `zerofill`, don't waste your time trying to work out what is the optimal number to use.
