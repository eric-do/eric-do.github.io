---
layout: post
title: Git Gud, Newb
comments: true
---

This post is meant to be a rough guide to Git and spells out some things that weren't clear to me as I was figuring it out. It assumes the user can install git on their own.

## Aliases
Common git commands can be shorted via aliases. I put this near the top because if I'm ever on a different machine and need a reference for setting up the aliases I'm used to, I'll find them here.

Aliases are updated in your .gitconfig file, which is stored in your $HOME directory. To find your home directory:

```
Erics-MacBook:_posts ericdo$ echo $HOME
```

Then add to the file:
```
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  type = cat-file -t
  dump = cat-file -p
```
  
## Updating files
The general flow for updating files (not including pulling/merging right now) is:
1. Update file(s) locally, save
2. Add file(s) to be commited. <br />Note: it's common you'll update multiple files but only want to commit a subset, so it's best to get in the habit of manually adding each file to be committed.
3. Commit changes
4. Push changes to your repo

So normally after you make a local update to the file and do a **git status**, the terminal will show something like:
```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   2020-04-02-Git-good.md
```
You'll want to then run steps 2-4 above:

```
Erics-MacBook:_posts ericdo$ git add 2020-04-02-Git-good.md
Erics-MacBook:_posts ericdo$ git commit -m "Added instructions on how to update files"
[master 0f7ec66] Added instructions on how to update files
 1 file changed, 53 insertions(+)
 create mode 100755 _posts/2020-04-02-Git-good.md
Erics-MacBook:_posts ericdo$ git push origin master
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 333 bytes | 333.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
```