# Git commands to help you tell your story

## Before a change is committed

### `git add -p`

The `-p` means "patch" and let's you stage your diff in chunks. 

### `git reset -p`

`reset` is a powerful command that is used to undo local changes, both staged and/or committed depending on how it's invoked. It can seem scary to undo changes, but with practice it's a realy handy command.

`git reset -p` is the inverse of `git add -p`. If you accidentally did a `git add .` and want to unstage just some of it, you can reset in chunks

### `git checkout -p`

If you want to get rid of some changes completely, you can also checkout your changes using the `-p` flag. 

### `git stash save 'msg'`

To put everything you currently have in your stash, you really only need `git stash` but I find it helpful to include a message so that you have some description of what you stashed.

`git stash` will stash everything regardless of staged/unstaged (unless the file is also untracked) and then when you `git stash pop` or `git stash apply`, it does not keep the staging.

### `git stash save -k`

To only stash your unstaged items, i.e. the things you haven't `git add`, then you want to use the `-k` flag which stands for `--keep-index`

### `git stash save -u`

To stash untracked files as well, you use the `-u` flag, which stands for `--include-untracked` 

To stash only your untracked files, you can combine the `-k` and `-u` flags

## What about after you've already committed your change?

### `git commit --amend`

This allows you to add files to your previous commit or edit the commit message.

### `git reset HEAD~1`

If you committed too much and you want to back out a file, you can soft reset the last commit (locally) and change what's staged and then re-commit. If you want to reset more than 1 commit, you can change that number to how many you want to undo. 

This will only undo the commit not the changes, so you'll have all of your changes in your staging area.

### `git cherry-pick <SHA>`

If you made a commit in the wrong branch, you can cherry-pick it into your correct branch before you reset/revert/undo it in some way in the wrong branch.

### `git checkout branch-name -- <filename>`

If you don't need the full commit and just want one file change, you can checkout just that file from another branch into your current branch.

_This is an aside, but does anyone else get confused by what "checkout" means b/c it means checkout like a library book or undo 🤷‍♀️_

### `git rebase -i HEAD~4`

Interactive rebase is incredibly powerful for editing your commit history but you should def only do this locally (before you push anything!)

You can change the order of commits, add files to a commit made multiple commits ago, combine commits, and remove commits. As well as probably a whole host of other things that I haven't tried yet.

### `git push --force-with-lease`

If you interactive rebase on a shared project (one where you aren't the only contributor), using `--force-with-lease` makes sure that you don't hose someone else's local repo. Your force push won't succeed if someone else has pushed up changes that your force push would overwrite.

### When might it be acceptable to force push?
To amend to a commit with something very small immediately after your previous push in a branch that you're soloing in.