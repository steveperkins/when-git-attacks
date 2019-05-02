# when-git-attacks
Merging and local problem resolution exercises for git

## Table of Contents
1. [Worksheets](#worksheets)
   1. [Exercise 1: Merging](#exercise-1-merging)
      1. [Practice 1: Merging a line conflict](#practice-1-merging-a-line-conflict)
      1. [Practice 2: Merging multiple conflicts](#practice-2-merging-multiple-conflicts)
      1. [Practice 3: Merging a file conflict](#practice-3-merging-a-file-conflict)

   1. [Exercise 2: Undoing](#exercise-2-undoing)
      1. [Practice 1: Undoing local (private), uncommitted changes](#practice-1-undoing-local-private-uncommitted-changes)
      1. [Practice 2: Undoing local (private), committed changes](#practice-2-undoing-local-private-committed-changes)
      1. [Practice 3: Undoing remote (public) changes](#practice-3-undoing-remote-public-changes) 

## Worksheets
### Exercise 1: Merging
#### Practice 1: Merging a line conflict
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


#### Practice 2: Merging multiple conflicts
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

#### Practice 3: Merging a file conflict
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



### Exercise 2:  Undoing
#### Practice 1: Undoing local (private), uncommitted changes
1. Check out the `reverting` branch
1. Let's edit JailhouseRock.txt. Make any changes you’d like.
1. **Stage** your changes
   * `git add JailhouseRock.txt`
1. Verify Git knows the file is ready to be committed
   * `git status`
1. On second thought, Jailhouse Rock is awesome already. Let’s revert the **staged**-but-not-committed changes.
   * `git reset HEAD JailhouseRock.txt`
1. Check the status
   * `git status`
   
   ![git diff just shows unmerged file paths](../../raw/screenshots/E2-2%20-%20revert%20keeps%20changes%20local.PNG)
   
1. Wait, what happened? Git **unstaged** the file, but didn’t discard the actual changes. That's good if you accidentally **staged** a change you wanted to keep but didn't want in the next commit. But we really wanted to do is completely throw away the changes to JailhouseRock.txt. To finish the job we have to use `git checkout` to discard local **unstaged changes**.
   * `git checkout JailhouseRock.txt`
   * `git status`

   ![git checkout destroys unstaged file changes](../../raw/screenshots/E2-1%20-%20checkout%20destroys%20unstaged%20changes.png)
   
1. Much better. Now our working directory has no changes! Note that `git checkout` only throws away **unstaged** changes - it has no effect on **staged** files.


#### Practice 2: Undoing local (private), committed changes
1. Let’s edit LifeIsAHighway.txt now. Change Line 3 to "We all live in a yellow submarine".
1. Stage the changes
   * `git add LifeIsAHighway.txt`
1. Commit the changes and confirm with `git status`
   * `git commit -m "Added the missing submarine"`
   * `git status`
1. Oh no, we edited the wrong file! We can’t use `git checkout` to fix this because the changes have already been committed. Let’s try `git reset` instead. The ~1 means "roll back to the commit 1 before HEAD". You could use another number instead.
   * `git reset HEAD~1`
   
   ![git reset un-commits local commits](../../raw/screenshots/E2-1%20-%20reset%20HEAD%20kills%20local%20commits.PNG)
   
1. We're closer, but not there yet. Just like with JailhouseRock.txt, `git reset` removed the local (**private**) commit but didn't discard the changes. Let's try it a different way.
   * `git add LifeIsAHighway.txt`
   * `git commit -m "Added missing submarine"`
   * `git reset --hard HEAD~1`
   * `git status`
1. Much better. Now our changes are nowhere to be found. It’s important to note that `--hard` ONLY works at the commit level, not the file level. When run at the commit level, `git reset` **will locally revert ALL changes in the commit**, not just changes in a specific file.


#### Practice 3: Undoing remote (public) changes
1. Let’s edit TenThousandFists.txt. Change Line 1 to "Ten Thousand Fists Clutching Straws In The Wind".
1. Stage your changes, commit, and push
1. Crap! That was a terrible joke and shouldn't have been pushed to the remote repository! Let's fix it with `git revert`. First though, we have to find out what that bad commit's hash (ID) was.
   * Use `git log -1` to see the last commit's details, which includes the hash. 1 is just how many commits we want to see.
   
   ![git log shows commit hashes](../../raw/screenshots/E2-3%20-%20commit%20hash%20in%20git%20log.png)
   * Copy the first 5 or 6 characters of the hash
1. Run `git revert your-hash--here` to revert the commit identified by the hash
1. Since the commit you want to revert is already in the remote repo (**public**), to reverse it `git revert` creates a second commit that nullifies the original commit’s changes. A text editor will open up for you to change the second commit’s commit message. The default message is fine, so just close the text editor.
1. `git status` now shows that the second commit is waiting to be made **public** (pushed to the remote repo). Go ahead and `push`.
   * `git push`
1. The commit log now shows both the original accidental commit and the reverse commit that corrected it.
   ![git log shows reverse commit](../../raw/screenshots/E2-3%20-%20git%20log%20shows%20reverse%20commit.png)
