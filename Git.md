# Git

## Git Branch

Git的分支只是简单地指向某个提交记录。

如果你想创建一个新的分支同时切换到新创建的分支的话，可以通过 `git checkout -b ` 来实现。

Rebase 实际上就是取出一系列的提交记录，“复制”它们，然后在另外一个地方逐个的放下去。

## HEAD

我们首先看一下 “HEAD”。 HEAD 是一个对当前检出记录的符号引用 —— 也就是指向你正在其基础上进行工作的提交记录。

HEAD 总是指向当前分支上最近一次提交记录。大多数修改提交树的 Git 命令都是从改变 HEAD 的指向开始的。

HEAD 通常情况下是指向分支名的（如 bugFix）。在你提交时，改变了 bugFix 的状态，这一变化通过 HEAD 变得可见。

想完成此关，从 `bugFix` 分支中分离出 HEAD 并让其指向一个提交记录。

通过哈希值指定提交记录。每个提交记录的哈希值显示在代表提交记录的圆圈中。

## 相对引用

- 使用 `^` 向上移动 1 个提交记录
- 使用 `~` 向上移动多个提交记录，如 `~3`

要完成此关，切换到 `bugFix` 的父节点。这会进入分离 `HEAD` 状态。



## DVCS Terminologies

 Only those files present in the staging area are considered for commit and not all the modified files.

 If a commit has multiple parent commits, then that particular commit has been created by merging two branches

Whenever you make a commit, **HEAD** is updated with the latest commit.



**Push** operation copies changes from a local repository instance to a remote one. This is used to store the changes permanently into the Git repository. This is same as the commit operation in Subversion.



 Uses the **git show** command to view the commit details. The git show command takes **SHA-1** commit ID as a parameter.

```
$ git show cbe1249b140dad24b2c35b15cc7e26a6f02d2277
```





****

The first method to combine work that we will examine is `git merge`. Merging in Git **creates a special commit** that has two unique parents. A commit with two parents essentially means "I want to include all the work from this parent over here and this one over here, *and* the set of all their parents."







Rebasing essentially takes a set of commits, "copies" them, and plops them down somewhere else.



HEAD is the symbolic name for the currently checked out commit

Detaching HEAD just means attaching it to a commit instead of a branch.



- Moving upwards one commit at a time with `^`
- Moving upwards a number of times with `~`



One of the most common ways I use relative refs is to move branches around. You can directly reassign a branch to a commit with the `-f` option. So something like:

```
git branch -f main HEAD~3
```

moves (by force) the main branch to three parents behind HEAD.



To complete this level, move `HEAD`, `main`, and `bugFix` to their goal destinations shown.



`git reset` reverts changes by moving a branch reference backwards in time to an older commit. In this sense you can think of it as "rewriting history;" `git reset` will move a branch backwards as if the commit had never been made in the first place.



To complete this level, reverse the most recent commit on both `local` and `pushed`. You will revert two commits total (one per branch).

Keep in mind that `pushed` is a remote branch and `local` is a local branch -- that should help you choose your methods.





We will overcome this difficulty by doing the following:

- We will re-order the commits so the one we want to change is on top with `git rebase -i`
- We will `git commit --amend` to make the slight modification
- Then we will re-order the commits back to how they were previously with `git rebase -i`
- Finally, we will move main to this updated part of the tree to finish the level (via the method of your choosing)

There are many ways to accomplish this overall goal (I see you eye-ing cherry-pick), and we will see more of them later, but for now let's focus on this technique. Lastly, pay attention to the goal state here -- since we move the commits twice, they both get an apostrophe appended. One more apostrophe is added for the commit we amend, which gives us the final form of the tree

That being said, I can compare levels now based on structure and relative apostrophe differences. As long as your tree's `main` branch has the same structure and relative apostrophe differences, I'll give full credit.



---



`git fetch` is a command used to get files from the remote repository to the local repository but not into the working directory.

`git merge` is a command used to get the files from the local repository into the working directory.

`git pull` is a command used to get files from the remote repository directly into the working directory. It is equivalent to a `git fetch` and a `git merge` .





---

## How to clone specific branch?

```bash
$ git clone https://github.com/zhhp1001/git_practice.git
$ cd git_practice
```



Next, look at the local branches in your repository:

```bash
$ git branch
* master
```



But there are other branches *hiding* in your repository! You can see these using the`-a` flag:

```bash
$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
  remotes/origin/second_branch
```

If you just want to take a quick peek at an upstream branch, you can check it out directly:

```bash
$ git checkout origin/second_branch
```

But if you want to work on that branch, you'll need to create a local tracking branch which is done automatically by:

```bash
$ git checkout second_branch //you can choose any name as you wish.
```



---

Read git log by text based graph 

```bash
git log --graph // better to plus `--oneline` 
```

To read 

[1](https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting#:~:text=For%20this%20reason%2C%20git%20revert,is%20for%20undoing%20uncommitted%20changes.)

[2](https://www.atlassian.com/git/tutorials/undoing-changes)

Use this visual tool...

http://git-school.github.io/visualizing-git/#upstream-changes





---



`HEAD` always refers to the current commit, be it a branch or a specific commit.



Tracks the history of `checkout` :

```bash
git reflog
```



---

In order to checkout a remote branch you have to first fetch the contents of the branch.

```bash
git fetch --all
```

You can  then checkout the remote branch like a local branch.



---



The `git checkout` command simply updates the `HEAD` to point to either the specified branch or commit

When it points to a branch, Git doesn't complain, but when you check out a commit, it switches into a `“detached HEAD”` state.

The point is, your development should always take place on a branch—never on a detached `HEAD`.

This makes sure you *always have a reference to your new commits*. However, if you’re just looking at an old commit, it doesn’t really matter if you’re in a detached `HEAD` state or not.



---



The `git commit --amend` command is a convenient way to modify the most recent commit. It lets you combine staged changes with the previous commit instead of creating an entirely new commit.

But, amending does not just alter the most recent commit, it replaces it entirely



Adding the `-m` option allows you to pass in a new message from the command line without being prompted to open an editor.

---



Rebasing is the process of moving or combining a sequence of commits to a new base commit.



---



`git reset `  

- `--soft`  The staged snapshot and working directory are not altered in any way.
- `--hard`  The staged snapshot and working directory are both updated to match the specified commit.



Unlike `git reset`, `git checkout` doesn’t move any branches around.



`git checkout <commit_hash>` is useful for quickly inspecting an old version of your project. However, since there is no branch reference to the current `HEAD`, this puts you in a detached `HEAD` state. This can be dangerous if you start adding new commits because there will be no way to get back to them after you switch to another branch. For this reason, you should always create a new branch before adding commits to a detached `HEAD`.



Contrast this with `git reset`, which *does* alter the existing commit history. For this reason, `git revert` should be used to undo changes on a public branch, and `git reset` should be reserved for undoing changes on a private branch.



 `git checkout` solely operates on the `HEAD` ref pointer, `git reset` will move the `HEAD` ref pointer and the current branch ref pointer. 



---



## Three trees of Git



### working directory

### staging area

### commit history













