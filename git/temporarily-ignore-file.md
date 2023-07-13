# Temporarily "ignore" a file

You can temporarily "ignore" a file that's under version control. This is useful for stopping you accidentally committing/pushing changes like settings that you are experimenting with locally. eg.

```
git update-index --assume-unchanged src/settings.php
```

You can reverse it easily:

```
git update-index --no-assume-unchanged src/settings.php
```

Remembering that you have done this of course, is an exercise left to the reader.

I learned this from this Stack Overflow question: <https://stackoverflow.com/a/49370034/966703>
