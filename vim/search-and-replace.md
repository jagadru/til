# Search and Replace in Vim

Syntax of the text substitution inside vim editor:

```vim
:[range]s[ubstitute]/{pattern}/{string}/[flags] [count]
```

There are three possible flags.

### Flags
* [c] Confirm each substitution.
* [g] Replace all occurrences in the line.
* [i] Ignore case for the pattern.

### Lines selector
 * %s – specifies all lines. Specifying the range as ‘%’ means do substitution in the entire file.
    ```
    :%s/old-text/new-text/g
    ```
 * Line selection. You select the line range
    ```
    :1,10s/helo/hello/g
    ```
 * Visual selection. Press `CTRL + V` in command mode, use navigation keys to select the part of the file you want to be substituted. Press ‘:’, you will see
    ```
    :'<,'>s/helo/hello/g
    ```

### Interactive Find and Replace in Vim Editor

```
:%s/awesome/wonderful/gc

replace with wonderful (y/n/a/q/l/^E/^Y)?
```
 * y – Will replace the current highlighted word. After replacing it will automatically highlight the next word that matched the search pattern
 * n – Will not replace the current highlighted word. But it will automatically highlight the next word that matched the search pattern
 * a – Will substitute all the highlighted words that matched the search criteria automatically.
 * l – This will replace only the current highlighted word and terminate the find and replace effort.
