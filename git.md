# Git

## `git status` shows modified files because of CRLF and LF 

I had an issue where hundreds of line endings were modified by some program and git diff listed all source files as changed. After fixing the line endings, git status still listed the files as modified.

I was able to fix this problem by adding all files to index and then resetting the index.

```
git add -A

git reset
```

`core.filemode` was set to false.


