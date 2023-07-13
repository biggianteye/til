# Exporting repository directories

Way back in the mists of time, CVS and later SVN had the ability to `export` a project. This downloaded the project without any of the version control information.

This was useful when you needed the code on things like build servers where you didn't want to make any changes. This mechanism also allowed you to download a subfolder of the project.

Pulling down a directory from github is surprisingly hard!

- You can allegedly use `svn export` but it gets fiddly with private repos.
- You can't use `git archive` because github explicitly doesn't support it.
- With some contortions you could use the zip download but that is also fiddly with private repos.

After faffing about for a few hours on this, I ended up just going down the path of cloning the repo like this:

```shell
git clone git@github.com:username/my-repo.git && \
    mv my-repo/some/directory . && \
    rm -rf my-repo
```

It's gross, but it does the job. #pragmatism

## Links
* Stack Overflow: [Download a single folder or directory from a GitHub repo
](https://stackoverflow.com/questions/7106012/download-a-single-folder-or-directory-from-a-github-repo)
* <https://twitter.com/GitHubHelp/status/322818593748303873>
