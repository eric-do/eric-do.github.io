---
layout: post
title: Git Gud - Updating Files
comments: true
---
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