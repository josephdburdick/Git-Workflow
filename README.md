#A collaborative process for Git. 
From the official Github Flow guide:
> Branching is a core concept in Git, and the entire GitHub Flow is based upon it. 
> There's only one rule: anything in the master branch is always deployable.

All changes should always be made in a branch created from master. Working in and merging changes within the master branch will inevitably lead to conflicts while working with others. For best results, prepend your branch name with something consistent and something unique (like your name/username, e.g.: josephdburdick/featureName]) .

Following the process improves everybody's workflow both independently and collectively. It enforces good documentation, backups, and prevents common merge conflicts while working with others. It is also inline with the official [Github Flow guide](https://guides.github.com/introduction/flow/), _"a lightweight, branch-based workflow that supports teams and projects where deployments are made regularly."_ 

:metal:
***

## Pre-Pull Request

Use rebase to do whatever you please to make the history most understandable and clear [[guide](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)]:

* Update with contents of master
* Squash commits together
* Separate single commits into multiple ones
* Reorder commits
* Remove commits
* Alter commit messages
* Force push changes to your <u>branch</u> (the only time force push is okay; *never* force push to master)

## Post-Pull Request

* Commit and push to your branch to address feedback from code review/visual testing

## Pre-Merge

* Do one large rebase to bring your branch up-to-date with master
* Do not push rebased version — keeps commentary history
* Do explicitly merge with master using `—no-ff` [What is the difference between `git merge` and `git merge --no-ff`?](http://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff)
* This merge commit does have value, indicates a feature has landed

## Workflow

1. Get assigned issue on Github / Atlassian / Issue Tracker. 
	* `git checkout master`
	* `git pull origin master`
	* `git checkout -b [your-name]/[feature]` (Create feature branch)
2. Work on feature; commit/push to this unique branch often. 
3. Prep for master update by fetching the latest master from origin and placing your code on top of it within your own branch.
	* `git fetch`
	* `git rebase origin/master -i` 
	* `git push origin [your-name]/[feature] -f`
4. If submitting Pull Request for code review
	* Open a Pull Request
	* Respond to PR feedback (commit and push only)
5. Merge
	* `git checkout master`
	* `git merge [your-name]/[feature]`
6. If Pull Request submitted
	* Close PR and link merge commit SHA in comment
7. Close relevant issue and link merge commit SHA in comment
8. Delete branches
	* From local: `git branch -D [your-name]/[feature]` 
	* From remote: `git push origin --delete [your-name]/[feature]`
	* Or include a script in your .bashrc / .zshrc file that does both simultaneously: ```deleteBranch(){ git branch -D $1; git push origin --delete $1 }```
	-	`$ deleteBranch [your-name]/[feature]`


## Merging
* `git fetch`
* `git checkout [your-name]/[feature]`
* `git rebase origin/master`
* …resolve any conflict…
* `git checkout master`
* `git reset --hard origin/master`
* `git merge --no-ff [your-name]/[feature]`
* …there should be no conflicts at this point since they were resolved already…
* …make sure you can build, no warnings, etc…
* `git push origin master`

## Escape Hatches
* `git rebase -abort` while rebasing
* `git reset --hard ORIG-HEAD` after rebasing
* `git reflog` if you accidentally delete something you don’t mean to
