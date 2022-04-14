# Git

## `git status` shows modified files because of CRLF and LF 

I had an issue where hundreds of line endings were modified by some program and git diff listed all source files as changed. After fixing the line endings, git status still listed the files as modified.

I was able to fix this problem by adding all files to index and then resetting the index.

```shell
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

The above command is for a specific file. It will take effect with your next commit. It’s a good idea for you to commit
any pending changes you have before you start this process. If you have many files and/or folders (for instance, your
/bin and /obj folders in a .NET project) that you need to clean up from your repository, you can use the following commands 
to remove them from the index (cache):

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

Then, commit your changes and your files that would have been ignored if you’d had the right `.gitignore` in place from 
the start should no longer be tracked. Yay! If you’re interested, or if this approach doesn’t work for you, there are a
few variations on how you might achieve the same result listed in 
[this StackOverflow thread](http://stackoverflow.com/questions/1274057/how-to-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitignore).


## Cloning and Using Pull Requests

It's not immediately obvious how to pull down the code for a PR and test it locally. But it's [pretty easy](https://help.github.com/articles/checking-out-pull-requests-locally/). (This assumes you have a remote for the main repo named `upstream`.)

**Getting the PR code**

1. Make note of the PR number. For example, Rod's latest is PR #37: https://github.com/Psiphon-Labs/psiphon-tunnel-core/pull/37

2. Fetch the PR's pseudo-branch (or bookmark or rev pointer whatever the word is), and give it a local branch name. Here we'll name it `pr37`:
  ```
  $ git fetch upstream pull/37/head:pr37
  ```

3. Switch to that branch:
  ```
  $ git checkout pr37
  ```

4. Compile and test.

If the PR code changes and you want to update:

```
# Do this while in the pr37 branch
$ git pull upstream pull/37/head
```

(I try to avoid `pull` and instead use `fetch`+`merge`, but... I don't know how to do it for this.)

**Merging the PR**

You can use the Github web interface, but there's a [TOCTOU](https://en.wikipedia.org/wiki/Time_of_check_to_time_of_use) problem: If the pull-requester changes their master (or whatever they're PRing from) between the time you test and the time you merge, then you'll be merging code that you haven't reviewed/tested. So let's do it on the command line.

First, checkout the upstream master code:

You'll only do this the first time -- it creates the local `upstream_master` branch, tracks it to `upstream_master`, and switches to the branch:
```
$ git checkout -t -b upstream_master upstream/master
```

After the first time you'll just do:
```
$ git checkout upstream_master
```

Now merge the PR:
```
$ git merge pr37
```

NOTE: You should edit the merge commit message to reference the PR (using, say `#37` in it).

Now push:
```
$ git push upstream HEAD:master
```

(You can't just `git push` because your local branch name is different than the remote.)

Done! Refresh the Github PR page and you'll see that the PR is now merged+closed.
## Diff master and a branch

```bash
git diff master branch_number
```

## Commit another change without editing the commit message

For when you forget to make an additional change and you've already committed 

```console
git commit --amend --no-edit
```

```html
<p class="chad">This is a sample test</p>
```

```bash
foo@bar:~$ whoami
foo
```
