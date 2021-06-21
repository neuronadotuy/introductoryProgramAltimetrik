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



## Bibliography

https://www.youtube.com/watch?v=2ReR1YJrNOM
https://www.perforce.com/blog/vcs/git-rebase-vs-merge-which-better
