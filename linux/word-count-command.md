# wc command - word count

Print newline, word, and byte counts for each file

## Parameters
```
-c, --bytes: print the byte counts
-m, --chars print the character counts
-l, --lines: print the newline counts
-L, --max-line-length: print the length of the longest line
-w, --words: print the word counts
```

## Example

```
cat distribution_service-20201124.log | grep GetFacebookPageInfoError | wc -l
12
```

## For more info
 - [Man wc](https://linux.die.net/man/1/wc)
