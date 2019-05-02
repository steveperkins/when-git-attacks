# when-git-attacks
Merging and local problem resolution exercises for git

## Worksheets
### Exercise 1
#### Practice 1
1. Fork repo at https://github.com/steveperkins/when-git-attacks and clone your fork
1. To see what branches are available, use `git branch -v -a`
1. Check out the one-conflict branch. This branch has a conflict that prevents an automatic merge.
   * `git checkout one-conflict`
1. Merge the master branch into this branch
   * `git merge origin/master`
1. There are conflicts! Find out which files have conflicts.
   * `git status`
   
   ![git status shows conflicted files but not conflicted text](../../raw/screenshots/one-conflict%20branch%20-%20status%20shows%20conflicted%20files.PNG)

1. It’s a good start, but WHAT are the conflicts? Compare your version against the one in the `master` branch to find out.
   * `git diff`

   ![git diff shows conflicted text](../../raw/screenshots/one-conflict%20branch%20-%20diff%20shows%20conflicts.PNG)

1. That’s more helpful. `<<<<<< HEAD to =====` shows what your changes were and `==== to >>>>>> master` shows what the `master` branch’s changes are at the same line. Edit `pie.txt` so we keep "death metal" but remove "This'll be the day that I die".

   ![conflicted text](../../raw/screenshots/one-conflict%20branch%20-%20conflict%20text.PNG)

1. Stage your fix
   * `git add pie.txt`
1. Verify the file was added
   * `git status`
1. Notice we’re still in MERGING mode. We have to commit the changes (resolutions) to all conflicted files before the merge is considered complete. Commit the changes to complete the merge.
   * `git commit -m "Merged from master"`
   ![still in MERGING until a commit is made](../../raw/screenshots/one-conflict%20branch%20-%20still%20merging%20until%20commit.PNG)
1. (Optional) Merge the changes back to the master branch
   * `git checkout master`
   * `git merge one-conflict`


#### Practice 2
1. Check out the `competing-line-conflict` branch. This branch has conflicts that prevent an automatic merge.
   * `git checkout competing-line-conflict`
1. Merge the `master` branch into this branch
   * `git merge origin/master`
1. There are conflicts! Find out what the conflicts are.
   * `git diff`

   ![git diff shows actual conflict text](../../raw/screenshots/competing-line-conflict%20branch%20-%20diff%20shows%20conflicts.PNG)
   
1. Great, the master branch changed '**paper**' to '**newspaper**' at the same time we changed it to '**dead tree rectangle**'. Change it to '**dead tree newspaper**' so everyone's happy.
1. The `master` branch also changed '**fire**' to '**off-by-one errors**' at the same time we changed it to '**sharks with lasers**'. Change it back to '**off-by-one errors**'.
1. Stage your fixes and commit the changes (resolutions) to complete the merge.
   * `git add pie.txt`
   * `git commit -m "Merged from master"`
1. (Optional) Merge the changes back to the `master` branch
   * `git checkout master`
   * `git merge competing-line-conflict`

#### Practice 3
1. Check out the `competing-file-conflict` branch. This branch has a conflict that prevents an automatic merge.
   * `git checkout competing-file-conflict`
1. Merge the `master` branch into this branch
   * `git merge origin/master`
1. There are conflicts! Find out what the conflicts are.
   * `git diff`
   
   ![git diff just shows unmerged file paths](../../raw/screenshots/competing-file-conflict%20branch%20-%20diff%20just%20shows%20unmerged%20file%20path.PNG)
   
1. The diff is not terribly helpful here. Let's try getting status instead.
   * `git status`
   
   ![git diff just shows unmerged file paths](../../raw/screenshots/competing-file-conflict%20branch%20-%20status%20shows%20we%20deleted%20file.PNG)
   
1. That's much more helpful. It shows that the master branch made changes to **music.html** at the same time we deleted the entire file. Git doesn’t know how to merge that - should the file exist or not? We have to tell Git whether we want to keep the file as it exists in `master` or confirm that we intended to delete the file. It's a Choose-Your-Own Adventure.
   * To keep the file as it exists in master, use `git`**`add`**`music.html`
   * To confirm that the file should be deleted, use `git`**`rm`**`music.html`
1. Whatever your choice, complete the merge
   * `git commit -m "Merged from master"`
1. (Optional) Merge the changes back to the `master` branch
   * `git checkout master`
   * `git merge competing-file-conflict`


