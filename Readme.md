Q: Would you lose any work if your a local clone of a git repository were lost?
A: Run this script to find out.

The script is useful to check the state of your project and what needs to be cleaned up.

Checks for:
 ∙ whether this is a git repository at all
 ∙ untracked files
 ∙ diffs not yet checked in
 ∙ stashes
 ∙ detached HEAD
 ∙ branches not pushed to `origin`
 ∙ all of the above for any submodules

The script itself had detailed notes, including about setting up and using the `-a`
flag to take the appropriate step for any of the above issues.
