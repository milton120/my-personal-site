---
title: Git for beginner++
date: 2018-11-18
published: true
tags: ['git','Software Engineering']
canonical_url: https://medium.com/datadriveninvestor/git-for-beginner-f438adfc3599
description: "You know the basic of git workflow and familiar with some basic commands like add, commit, push, pull then maybe this post is for you. This post is mainly focused on daily git use improvement, fixing some common mistakes and a step towards advance git learner."
---


You know the basic of git workflow and familiar with some basic commands like add, commit, push, pull then maybe this post is for you. This post is mainly focused on daily git use improvement, fixing some common mistakes and a step towards advance git learner.

### **# Scenario with add**

You just want to add files with specific extension in your staging area. Of course you can add all the files one by one. But you can use *.<extension_name> to include all files with that extension. Following command will add all python files.

    git add *.py

You want to add files with specific extension and also want to specify directory name then you can run the following command. The following command will add all python files from sub directories of models/ directory.

    git add models/\*.py

### # Scenario with clean

You created some new files or folders in your branch. After some time you realized that you don’t want those files or folders. You need your working tree clean. These are untracked files in git.

*Untracked files are those which you didn’t add already using git add*

To make your working tree clean you can run the following command. This command will delete all files and directories that are not tracked by git.

    git clean -df

If you want to see which untracked files will be removed before removing then you can run this command.

    git clean -dn

### # Scenario with rm

Now you want to delete your tracked files. You can delete your tracked file using this command.

    git rm <file-path>

If your file is in staging area then you have to give additional **force flag.**

    git rm <file-path> -f

You want to delete files from git repository but not from your file system then you can run this command.

    git rm --cached <file-path>

### **# Scenario with branch**

You have made a typo in your branch name or you want to change your branch name, then the following command will change your branch name.

    git branch -m <old-branch-name> <new-branch-name>

You want to change the current branch name, then you can just run the following command.

    git branch -m <new-branch-name> 

If you’ve already pushed the branch with old name, then there are a couple of extra steps required. You need to delete the old branch from the remote and push up the new one.

    git push <remote-name> --delete <old-branch-name>
    git push <remote-name> <new-branch-name> 

You want to push your local branch code but your local branch name doesn’t match with the name of remote repository branch name. Then you can run the following command.

    git push <remote-name> <local-branch-name>:<remote-branch-name> 

### # Scenario with log

You want to see your commit history so you just ran a git log command. This shows a lot of information but you just need to see commit id and message. Then you can run the following command.

    git log --oneline

git log --oneline will show the following kind of output.

![](https://cdn-images-1.medium.com/max/2720/1*p1NZBtY_zieo9YV_P9Is7w.png#screen-shot)

The first seven character in above output is the **shorthand commit id** and then we have our commit message. The commit id is shorthand because the full commit id is forty hexadecimal characters that specify a 160-bit SHA-1 hash. Notice Head -> master . This means we are now in master branch.

If you want to see the commit message of a specific author, then you can run the following command. I am assuming the author name is John Doe.

    git log --author="John Doe"

### # Scenario with stash

You are working in a branch and made some changes. Now, you want to just see the output or code of that branch before you made those changes. Then you can run stash command. It will make your working tree clean.

    git stash

If you want your changes back then you have to run the following command.

    git stash pop

If you don’t want those changes back then you have to run the following command.

    git stash drop

You changed some files in wrong branch. Then you can stash your changes and** checkout **to your desired branch and run git stash pop there. You will get your changes in your desired branch.

### # Scenario with checkout

You want to switch to a branch. Then you can just run the following command.

    git checkout <branch-name>

*If you already changed some file in your current branch, then be sure to stash your changes or commit the changes. . If you don’t stash or commit those changes, it will also reflect in your switched branch which you may not want or need.*

You have a branch name development and you want to make a branch from development and switch to your new branch directly. Then you can run the following command.

    (development)$ git checkout -b <your-new-branch-name>

You can also checkout using commit id. You can use shorthand commit id safely if your project isn’t very large.

    git checkout <commit-id>

*This will fall in **detached head **state in git. **Head** is simply a reference to the current commit (latest) on the current branch*.* Generally, **Head **in git can point to a branch or a commit. When Head points to a branch, git doesn’t complain. But when head points to a commit, but not a branch then it goes to a **detached head** state.*

You want to develop a feature from this **detached head** state then you have to make a branch from this state and develop your feature there.

    git checkout -b <your-new-branch-name>

### # Scenario with commit

You just added a commit message and realized that there is a typo in your commit or you just want to make your commit message more expressive and understandable. Then you can use the following git command.

    git commit --amend -m "your-new-commit-message"

If you just added some files or fixed a bug but don’t want to add another commit message then you can use following git command with --no-edit flag.

    git commit --amend --no-edit

*Here one thing is very important to remember that amending the last commit rewrites the commit history. It means your **commit id** will change when you amend a commit.*

If you already pushed your code in the remote repository and then you realized that you have to amend your commit message then after amending, you have to make a **force push. **Assuming your remote name as origin you can run the following command.

    git push origin <branch-name> -f

### # Scenario with reset

You want to discard your last some commits. Then you can use git reset to discard those commits. There are three flag for git reset that you should know.

* --soft

* --mixed

* --hard

![](https://cdn-images-1.medium.com/max/2720/1*Gv06pFgMVOT5x4yJvcGRrQ.png#screen-shot)

Let’s assume you want to discard the changes until **added two.txt **which has commit id** 96b037c**

Now, let’s run git reset command with --soft flag.

    git reset --soft 96b037c

git reset --soft will make **orphan **all the commits after that commit id (e.g. 96b037c) but the files will not be deleted. The files will be in the staging area.

**Orphaned** commit means there is no direct path from a ref to access them. These orphaned commits can usually be found and restored using git reflog Git will permanently delete any orphaned commits after it runs the internal garbage collector. By default, git is configured to run the garbage collector every 30 days.

So, if you run git status you will see the following output.

![](https://cdn-images-1.medium.com/max/2720/1*sAD1jfH8Xx5a6spnFLWGxA.png#screen-shot)

If you run git log --oneline you will see that previous commits are deleted.

![](https://cdn-images-1.medium.com/max/2720/1*E8sZRcyP4kky7RsqGG2qCw.png#screen-shot)

If you run reset command with --mixed flag then your commits will be **orphaned** and the files will not be in staging area but the files will be found in the file system. If you don’t specify any flag in reset then git will use --mixed flag as default.

If you run git status then you will see the following output.

![](https://cdn-images-1.medium.com/max/2740/1*BnhPheN0MvBqdalJDarGoQ.png#screen-shot)

If you want to permanently delete the files then you can run reset command with --hard flag.

*A good practice you can follow that you first run reset command with --soft flag and see the affected files. If you are sure that you don’t want those changes then you can run the reset command with --hard flag.*

You should never use git reset <commit-id> when any snapshots after <commit-id> have been pushed to a public repository. Removing a commit that other team members have continued developing poses serious problems for collaboration.

### # Scenario with revert

You are working in a public repository and you want to undo a commit. Then you can run the following command.

    git revert <commit-id> --no-commit

After running the above command, you can check the affected files using git status . Then you have to make a commit using git commit -m "commit-message" .

*git revert will not** orphan **a commit. It will just undo the changes of your reverted commit id.*

![](https://cdn-images-1.medium.com/max/3684/1*gwJgqYECujtC3__mDX68zw.png#screen-shot)

Let’s assume you want to revert the last commit. Then after reverting your status will look like following image.

![](https://cdn-images-1.medium.com/max/2720/1*egKJ4OeiGOItiDEJZPyBrQ.png#screen-shot)

Before the last commit **six.txt **file was not added, so it is deleted and** five.txt **is changed back to it’s previous state. Now, after committing your commit history will look like this.

![](https://cdn-images-1.medium.com/max/3684/1*XiWmXUWG5LLk3Q5QMMJprA.png#screen-shot)

You want to revert multiple commits within a range then you can run the following command.

    git revert <oldest-commit-id>..<recent-commit-id> --no-commit

If you want to revert multiple commits that are not within a range then you have to provide every commit id that you want to revert.

    git revert <commit-id-1> <commit-id-2> --no-commit

### # Scenario with cherry-pick

You are working in a branch and you need a commit(e.g. a bug fix commit) from another branch to work in your current branch. Then you can use cherry-pick command to get that commit in your current branch. It is also helpful if you committed in the wrong branch and want the commit in another branch.

First, you have to switch to the branch that has the commit. Copy the commit id of that commit and switch back to your own working branch. Then run the following command to get the commit in your working branch.

*git cherry-pick is like copying something from a folder and pasting it in another folder. So, it will not delete the commit from where you cherry picked and in destination branch commit id will also be different.*

    git cherry-pick <commit-id>

*I am also learning git almost everyday and don’t consider myself as an advance git user. So, if I made any mistake please feel free to correct me and put your suggestions in the comment section.*
