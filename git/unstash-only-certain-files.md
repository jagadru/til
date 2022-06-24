# Unstash only centain files with git

You can apply it by using `git checkout` to restore a specific file.

```shell
git checkout stash@{0} -- <filename>
```

With Git 2.23+ (August 2019), use `git restore`, which replaces the confusing `git checkout` command:

```shell
git restore --source=stash@{0} -- <filename>
```

That does __overwrite__ filename: make sure you didn't have local modifications, or you might want to merge the stashed file instead.

Reference: https://stackoverflow.com/a/15264717/19404207
