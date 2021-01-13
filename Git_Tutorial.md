### Learning Git/Github

This is a short introduction to using git/GitHub for version control. 


Git is a version control tool. Git can be confusing, yet it is also a very useful tool. The simplest way to work with git is through the command line. Since you have to explicitly type each command, working with git through the command line will help you understand what is actually happening. While IDE integration with git is useful, I would not recommend using it until you understand the basics. 

#### Installation
See the Installation section on the main github wiki page


#### Git Basics
This [git book](https://git-scm.com/book/en/v2) provides a great overview of git and how to work with a remote git repo like GitHub. This book is a well written, easy to read book, that provides the foundation from which you can gain After installing git, I recommend reading chapter 1 of the book. If you are short on time, or not interested in the history of version control, then you can skip to chapter 2 and read through chapter 3. 

The most important commands from that section are 

```bash 
git add 
git commit 
git clone 
git branch 
git checkout
git status 
```
 
#### Exercise

Now it is time to do a simple tutorial. Go to github and clone this repo https://github.com/DexterAntonio/github-tutorial.

```bash 
git clone https://github.com/DexterAntonio/github-tutorial.git
```

Navigate to the cloned repo github-tutorial

cd github-tutorial

Perform the following actions 
1.	Run git status
2.	Create a new branch and check it out using the git checkout -b branch-name command 
3.	Edit the README.md file and add your name to the list
4.	Check the status of the repo again
5.	Look at the differences using git diff 

```bash
➜  github-tutorial git:(main) git status
On branch main
Your branch is up to date with 'origin/main'.
 
nothing to commit, working tree clean
➜  github-tutorial git:(main) git checkout -b adding-my-name
Switched to a new branch 'adding-my-name'
➜  github-tutorial git:(adding-my-name) vim README.md 
➜  github-tutorial git:(adding-my-name) ✗ git status
On branch adding-my-name
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md
 
no changes added to commit (use "git add" and/or "git commit -a")
```

now stage your changes and commit them 
```bash
➜  github-tutorial git:(adding-my-name) ✗ git add -u
➜  github-tutorial git:(adding-my-name) ✗ git commit -m "added my name"
[adding-my-name f51eaf3] added my name
 1 file changed, 4 insertions(+)
```
Now it is time to push your branch the remote repo 
```bash
➜  github-tutorial git:(adding-my-name) git push origin adding-my-name  
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 317 bytes | 158.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: 
remote: Create a pull request for 'adding-my-name' on GitHub by visiting:
remote:      https://github.com/DexterAntonio/github-tutorial/pull/new/adding-my-name
remote: 
To https://github.com/DexterAntonio/github-tutorial.git
 * [new branch]      adding-my-name -> adding-my-name
 
 ```

 Go to github and create a pull request by clicking on the green bar titled `Compare & pull request'. 

 Add a comment if you want, then and click the `Create pull request` bar. 

 If you were working on a large software project, you would review the PR with your team. You are not, so just go ahead and click the `Merge pull request` button.

Now click the `Delete branch` button. 


The next steps are updating your local repo 

First checkout main/master

```bash
➜  github-tutorial git:(adding-my-name) git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
➜  github-tutorial git:(main) git pull 
```
Pull down the changes. If you have multiple branches that have additional changes, you can rebase them with main/master after the merge. 

```bash
➜  github-tutorial git:(main) git pull origin main  
remote: Enumerating objects: 11, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 5 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (5/5), done.
From https://github.com/DexterAntonio/github-tutorial
 * branch            main       -> FETCH_HEAD
   bc7c3ce..394a9db  main       -> origin/main
Updating bc7c3ce..394a9db
Fast-forward
 README.md | 4 ++++
 1 file changed, 4 insertions(+)
```
Check if your local branches are merged successfully 
```bash
➜  github-tutorial git:(main) git branch --merged
  adding-my-name
* main
```
Check if your local branches are merged successfully 
Delete the merged branch 
```
➜  github-tutorial git:(main) git branch -d adding-my-name
Deleted branch adding-my-name (was f51eaf3).
```

Now you can create a new branch and add to your addition of the project!

### Summary of workflow 

When doing a new experiment 
1.	Create a new local branch off of master branch
```git checkout –b new-branch-name```
2. Commit changes locally throughout progress (every time a change is made) 
```bash
git add –u # add tracked files
git add commit –m “what you did”
```

3. After experiment is complete push changes to remote 
```git push origin branch-name```
4. Create pull request on github 
5. Merge pull request with comments 
6. Delete branch on remote 
7. Switch back to local main/master branch
```git checkout main``` 
8. Pull down origin master/main 
```git pull origin main``` 
9. Delete local merged branch
```git branch –-merged # list merged branches
Git branch –d new-branch-name ```

People who have completed this tutorial: 
1. Dexter Antonio
