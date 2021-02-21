# Calculator
GIT practice

### Task:
> * Clone the following repo: https://github.com/SergiiPiatakov/calculator.git .
> * Using `rebase -i` swap the following commits: "fix truncation error" and "formatting: use tabs instead of spaces".
> * Then sign them and create two patches using `git format-patch`.
> * Then combine "improve calculation accuracy" and "fix truncation error" into one commit using `rebase -i`. Sign it.
> * Then remove the top commit "formatting: use tabs instead of spaces" using `git rebase -i` - I really don't like tabs ;) .
> * Rename the current remote on the "github". Add another remote: https://gitlab.com/SergiiPiatakov/calculator.git and call it "gitlab".
> * Get code from the "gitlab" remote by `git fetch`, and explore it by `git log gitlab/master`.
> * Then grab the commit: "add a multiplication operation" by `git cherry-pick`.
> * Create your own patch about 5-15 lines (any changes).
> * Push the result into your own repo.

### Solution:
Clone the following repo:
```
$ git clone  https://github.com/SergiiPiatakov/calculator.git calculator
$ cd calculator
```

View all existing commits:
```
$ git log
```

From the list of commits we need to swap the last 2 commits - *“fix truncation error”* and *“formatting: use tabs instead of spaces”*:
```
$ git rebase -i HEAD^^
```

Then we get the following message:
  > - error: could not apply 4ad40a3... fix truncation error
  > - When you have resolved this problem, run "git rebase --continue".
  > - If you prefer to skip this patch, run "git rebase --skip" instead.
  > - To check out the original branch and stop rebasing, run "git rebase --abort".
  > - Could not apply 4ad40a3b4572deee4efc716e7bd6e6e4fda46dcf... fix truncation error
  
 Now we need to resolve git conflict by hands. After conflict has been resolved:
  ```
$ git add calculator.cpp
$ git rebase --continue
```

Next command:
```
$ git show -n2
$ git rebase -i HEAD^^ 
```

Now put `edit` next to the commits names.

Then we need sign commits and perform next action twice, cause we have two commits:
```
$ git commit --amend -v -s
$ git rebase --continue
```

Run `$ git log` to check that last two commits are signed by you.

Create two patches using `git format-patch`:
```
$ git format-patch HEAD -2
```

Combine two commits into one:
```
$ git rebase -i HEAD^^^
```
Then use `squash` command. 

Now sign our new commit and continue:
```
$ git commit -s --amend
$ git rebase --continue
```

Rename the current remote on the "github". Add another remote and call it "gitlab":
```
$ git remote
$ git remote rename origin github
$ git remote add gitlab https://gitlab.com/SergiiPiatakov/calculator.git
$ git remote show
```

Get code from the "gitlab" remote by `git fetch`, and explore it by `git log gitlab/master`:
```
$ git fetch gitlab
$ git log gitlab/master
$ git branch -av
```

Then grab the commit: "add a multiplication operation" by `git cherry-pick`:
```
$ git log --oneline gitlab/master
$ git cherry-pick e0ea21b
```
Now we have error *"could not apply e0ea21b... add a multiplication operation"* and we need to fix git conflict (`$ git status` and `$ vim <file_with_conflict>`). After that:
```
$ git cherry-pick --continue
```

Then we create our own patch (check code above) and push the result into repo.
