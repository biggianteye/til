# NOT NULL without a DEFAULT

It turns out that you can add a `NOT NULL` column to a MySQL table with
existing data without specifying a default value. MySQL will silently fill
in the column with what (I'm guessing) is the default value for the data
type.

```sql
create table a (foo int, bar into);
insert into a values (1,1), (2,2), (3,3);
alter table a add column i_null int;
alter table a add column i_not_null int not null;
alter table a add column s_null varchar(10);
alter table a add column s_not_null varchar(10) not null;
```

```
mysql> select * from a;
+------+------+--------+------------+--------+------------+
| foo  | bar  | i_null | i_not_null | s_null | s_not_null |
+------+------+--------+------------+--------+------------+
|    1 |    1 |   NULL |          0 | NULL   |            |
|    2 |    2 |   NULL |          0 | NULL   |            |
|    3 |    3 |   NULL |          0 | NULL   |            |
+------+------+--------+------------+--------+------------+
```

The `int` column has been filled in with a `0` and the `varchar` column has
been filled in with an empty string.

This is not the behaviour I would expect and is potentially unsafe. For
example, that zero might not be a correct/safe/valid value to have. I don't
like the fact that it silently does this. I guess it is trying to be
"helpful"?

I have more experience with Oracle than MySQL and Oracle would not allow
this. The moment you try to add such a column, you would get this error:

> ORA-01758: table must be empty to add mandatory (NOT NULL) column

That makes more sense to me as the database engine should not make guesses
as to what the value in a `NOT NULL` column should be.
