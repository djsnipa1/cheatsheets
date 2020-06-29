# Git

## `git status` shows modified files because of CRLF and LF 

I had an issue where hundreds of line endings were modified by some program and git diff listed all source files as changed. After fixing the line endings, git status still listed the files as modified.

I was able to fix this problem by adding all files to index and then resetting the index.

```
git add -A

git reset
```

`core.filemode` was set to false.

Git features a ‘remove’ command, `git rm`. You can use it to remove files from git’s tracking cache, like so:

PowerShell

git rm \-\-cached <filename>

|

1

 |

git rm  \-\-cached  < filename\>

 |

The above command is for a specific file. It will take effect with your next commit. It’s a good idea for you to commit any pending changes you have before you start this process. If you have many files and/or folders (for instance, your /bin and /obj folders in a .NET project) that you need to clean up from your repository, you can use the following commands to remove them from the index (cache):

PowerShell

git rm \-r \-\-cached .

|

1

 |

git rm  \-r  \-\-cached .

 |

The `-r` switch makes the command recursive from the current path. Next, add back all of the files you do want to track, using:

PowerShell

git add .

|

1

 |

git add  .

 |

Then, commit your changes and your files that would have been ignored if you’d had the right `.gitignore` in place from the start should no longer be tracked. Yay! If you’re interested, or if this approach doesn’t work for you, there are a few variations on how you might achieve the same result listed in [this StackOverflow thread](http://stackoverflow.com/questions/1274057/how-to-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitignore).


## Cloning and Using Pull Requests

```
git fetch origin pull/34/head:pull_34
git checkout pull_34
```

What that does is creates the **branch 34** named **pull_34**. Now you can merge it:

```
git checkout master
git merge pull_34
git branch -d pull_34
```


