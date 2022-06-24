# Filter commits between two branches

You can use `git cherry` and you will see something like

```shell
git checkout devel
git cherry next
```

```
+ 492508acab7b454eee8b805f8ba906056eede0ff
- 5ceb5a9077ddb9e78b1e8f24bfc70e674c627949
+ b4459544c000f4d51d1ec23f279d9cdb19c1d32b
+ b6ce3b78e938644a293b2dd2a15b2fecb1b54cd9
```

The commits that begin with `+` will be the ones that you haven't yet cherry-picked into next.
In this case, I'd only cherry-picked one commit so far. You might want to add the -v parameter to the `git cherry` command, so that it also outputs the subject line of each commit.

Also, you can use

```shell
git log --left-right --graph --cherry-pick --oneline devel...next
```
to get a nice list of actual different commits not shared between the branches.

Reference:
  * [How to see which commits in one branch aren't in the other](https://stackoverflow.com/questions/7566416/how-to-see-which-commits-in-one-branch-arent-in-the-other)
  * [git cherry](https://git-scm.com/docs/git-cherry)
  * [git log](https://git-scm.com/docs/git-log)

