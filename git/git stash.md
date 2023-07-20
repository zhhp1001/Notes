# git stash

`git stash pop` **throws away** the (topmost, by default) stash after applying it, whereas `git stash apply` **leaves it in the stash list** for possible later reuse (or you can then `git stash drop` it).

This happens unless there are conflicts after `git stash pop`, in which case it will not remove the stash, leaving it to behave exactly like `git stash apply`.

Another way to look at it: `git stash pop` is `git stash apply && git stash drop`.

If there are conflicts when a stash is popped, pop will not remove the stash (and will behave exactly like apply) 