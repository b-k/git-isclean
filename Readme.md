Q: Would you lose any work if your local clone of a git repository were lost?  
A: Run this script to find out.

The script is useful to check the state of your project and what needs to be cleaned up.
It checks for

 * whether this is a git repository at all  
 * untracked files  
 * diffs not yet checked in  
 * stashes  
 * detached HEAD  
 * branches not pushed to `origin`  
 * tags not pushed to `origin`
 * all of the above for any submodules

It returns 0 if the repository passes all checks (no untracked files, no diffs, ...), and 1 otherwise.

With the -a flag, take the first relevant automatic action. In every case that is not purely
informational, ask permission
before doing anything. If an action feels unsafe or inappropriate, just say no or hit <ctrl>-C to leave.

 * If this is not even a git repository, run `git init`.
 * If there are untracked files, run `git status -s`.
 * If there are diffs, run `git diff`.
 * If there is one stash, run `git stash show -p` [i.e., print the stash diff].
 * If there are multiple stashes, run `git stash list`.
 * If there are tags not pushed to origin, push them.
 * If in a detached HEAD state, merge to master.
 * If a branch (incl. master) needs to be `git push origin`-ed, do so.
 * If there are submodules, recurse into them and run all of the above; else print nothing.
 * If everything is clean, remove the directory!

The last step is intended for people who have the work habit of not leaving copies of
repositories in their home directory if they aren't needed—effectively putting them
back on the shelf to take down later. If that isn't your habit, it is safe to remove the
last block of this script that takes that action. If you do delete the directory entirely,
you will still need to `cd` to another directory yourself (a subshell can't change
its parent shell's working directory.)

Setup:
Add this to your `~/.gitconfig`:

```
[alias]
    isclean = !/path/to/git-isclean
```

Now you can run
`git isclean`
or 
`git isclean -a`
from any repository.

Limitations:
 * Misses empty subdirectories---including those with only dot files!
 * Assumes your only remote is origin.

License: CC BY SA [creative commons, attribution, share-alike]
By Ben Klemens. See http://modelingwithdata.org/arch/00000194.htm for discussion.
