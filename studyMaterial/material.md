## What is Git?

Git is the most popular version control system, its free, open source, fast and scalable.

A version control system record the changes made to our code over time in a special database called repository, we can look at our project history and see who and why and if we screw something up we can easily reverse our project to an earlier state.

With Git or any other version control system we can track history and work together.

VCS fall into 2 categories, Centralized and Distributed.

Centralized system, all team members connect to a central server to get the later copy of the code and to share their changes with others. The problem with centralized architecture is the single point of failure. If the server goes offline we cannot collaborate or save snapshots of our project so we have to wait until the server comes back online.

In Distributed systems we don’t have this problem, every team member has a copy of the project with his history in their machine so we can save snapshots of our project locally on our machine. If the central server is offline we can synchronize our work directly with others.

Git is an example of a distributed version control systems.

## Git rebase and squash | merge vs rebase

### What is git merge?

Git merge is a command that allows you to merge branches from Git.

### What Is Git Rebase?

Git rebase is a command that allows developers to integrate changes from one branch to another.

### Git Rebase vs. Merge: Similarities and Differences

[Git rebase](https://www.perforce.com/blog/vcs/git-rebase-vs-merge-which-better#Git Rebase) and merge both integrate changes from one branch into another. Where they differ is how it's done. Git rebase moves a feature branch into a master. [Git merge](https://www.perforce.com/blog/vcs/git-rebase-vs-merge-which-better#Git Merge) adds a new commit, preserving the history.

### Git Rebase vs. Merge: Which to Use

Some developers believe you should always rebase. And others think that you should always merge. Each side has benefits.

### Benefits

Here are the top three benefits for Git rebase and for Git merge.

#### Git Rebase

- Streamlines a potentially complex history.
- Avoids merge commit “noise” in busy repos with busy branches.
- Cleans intermediate commits by making them a single commit, which can be helpful for DevOps teams.

#### Git Merge

- Simple and familiar.
- Preserves complete history and chronological order.
- Maintains the context of the branch.

Using git for version control allows for powerful collaboration in tech teams. Like any tool, if misused, it can also cause some serious headaches. After working with a wide variety of team sizes and dynamics, I’ve found that the `squash and rebase workflow` helps make the collaboration process more efficient and a hell of a lot less painful.

## What is the squash rebase workflow?

It’s simple – before you merge a feature branch back into your main branch (often `master` or `develop`), your feature branch should be squashed down to a single buildable commit, and then rebased from the up-to-date main branch. Here’s a breakdown.

Pull master branch

```
git pull origin master
```

Create bug/feature branch

```
git checkout -b branchName
```

Make changes as needed with as many commits that you need to. Make sure the final commit is buildable and all tests pass.

Get the number of commits from the start of your branch. There are a couple of ways to get this. You can simply `git log` and count your commits, or

```
git log --graph --decorate --pretty=oneline --abbrev-commit
```

which will show a graph of your commit log history and may be easier to visualize your commits. Sometimes you will have large enough number of commits that counting can become troublesome. In that case grab the SHA from the last commit that your branch branches from.

Squash to 1 commit.

```
git rebase -i HEAD~[NUMBER OF COMMITS]
```

OR

```
git rebase -i [SHA]
```

If you have previously pushed your code to a remote branch, you will need to force push.

```
git push origin branchName --force
```

Checkout master branch

```
git checkout master
```

Pull master branch

```
git pull origin master
```

Checkout bug/feature branch

```
git checkout branchName
```

Rebase from master

```
git rebase master
```

Handle any conflicts and make sure your code builds and all tests pass. Force push branch to remote.

```
git push origin branchName --force
```

Checkout, merge, and push into master

```
git checkout master
git merge branchName
git push origin master
```

## Why should you adopt this workflow?

If you follow this process it guarantees that ALL commits in master build and pass tests. This simple fact makes debugging an issue much easier. You can use **git** bisect when trying to find the source of a bug. Git bisect becomes almost completely ineffective  if there are broken commits on the master branch; if you jump to a commit that isn’t clean, it’s difficult or impossible to tell if it introduced the bug.

The process also cleans up your git log. Have you ever seen a git log graph that looks like this?

![img](https://blog.carbonfive.com/wp-content/uploads/2017/08/Screen-Shot-2017-07-10-at-3.28.16-PM-1-470x428.png)

This is incredibly hard to discern what is going on, especially when you compare it to what my process makes the history look like:

![img](https://blog.carbonfive.com/wp-content/uploads/2017/08/Screen-Shot-2017-07-10-at-3.39.18-PM-1-470x396.png)

Because each commit contains all the code for a feature or bug fix, you can easily see the whole unit of work in a commit, and you don’t have to  worry about checking out the correct commit from a branch.

My favorite outcome of this workflow is that it makes handling conflicts from rebasing simple. Since you’ve squashed down to one commit, you only have to deal with those conflicts once, rather than having to work against half-baked code. It reduces the risk of losing code when dealing with the conflicts.

## So what are the drawbacks?

Since we’re squashing commits and rebasing, we are literally changing the history for the repository. Some people feel that history should reflect your true history, the good the bad and the ugly. I propose a clean history is more valuable than one that is hard to understand. Not all history is lost; diehards can still see the original history in the ref log. Another small drawback is that we lose some granularity when we squash our commits. If you really want to have multiple commits for a feature, at least squash down so that each commit builds and passes tests. While this workflow can be dangerous if you don’t have an understanding of what you are doing, after minimal education on the matter, this process is extremely safe.

## TLDR

When it comes to squashing and rebasing your commits, the pros significantly outweigh the cons. It speeds up your debugging process, cleans up your history, reduces the pain from merge conflicts and makes collaboration in your team much better.

## Bibliography

https://www.youtube.com/watch?v=2ReR1YJrNOM
https://www.perforce.com/blog/vcs/git-rebase-vs-merge-which-better
https://blog.carbonfive.com/always-squash-and-rebase-your-git-commits/
