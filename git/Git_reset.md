# git reset

The `git reset` command is a complex and versatile tool for undoing changes. It has three primary forms of invocation. These forms correspond to command line arguments `--soft, --mixed, --hard`. The three arguments each correspond to Git's three internal state management mechanism's, The Commit Tree (`HEAD`), The Staging Index, and The Working Directory.

> Refer to:
>
> https://www.atlassian.com/git/tutorials/undoing-changes/git-reset

First of all, git cannot operate **untracked file**.

Following 2 pics can demonstrate this concept clearly: 

![enter image description here](https://i.stack.imgur.com/qRAte.jpg)

![image-20211123153618447](C:\Users\hzhen\AppData\Roaming\Typora\typora-user-images\image-20211123153618447.png)

In other words, 

`--soft` is discarding last commit;

 `--mix` is discarding last commit and add;

` --hard` is discarding last commit,add and any changes you made on the codes which is the same with git checkout HEAD

In other words,

`--soft`: **uncommit** changes, changes are left staged (*index*).

`--mixed` *(default)*: **uncommit + unstage** changes, changes are left in *working tree*.

`--hard`: **uncommit + unstage + delete** changes, nothing left.

>  Refer to :
>
> https://stackoverflow.com/questions/3528245/whats-the-difference-between-git-reset-mixed-soft-and-hard

