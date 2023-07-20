# waitpid WNOHANG WUNTRACED



> man: In the case of a terminated child, performing `wait` allows the system to release the resources associated with the child; if a `wait` is not performed, then the terminated child remains a `zombie` state.



There is a legendary explanation from [stackoverflow](https://stackoverflow.com/questions/33508997/waitpid-wnohang-wuntraced-how-do-i-use-these/34845669) .

You usually use WNOHANG and WUNTRACED in different cases.

Case 1: Suppose you have a process which spawns off a bunch of children and **needs to do other stuff while the children are running**. These children sometimes exit or are killed, but the kernel will hold onto their exit status until some other process claims it via wait() or waitpid(). So, your parent process needs to call wait()/waitpid() on occasion to let the kernel rid itself of the remains of the child. But we don't want wait()/waitpid() to *block*, because, in this case, our process has other things that it needs to do. **We just want to collect the status of a dead process *if* there are any**. That's what WNOHANG is for. It prevents wait()/waitpid() from blocking so that your process can go on with other tasks. If a child died, its pid will be returned by wait()/waitpid() and your process can act on that. If nothing died, then the returned pid is 0.

Case 2: Suppose your parent process, instead, wants to do *nothing* while children are running. You don't want to just have it do some thumb-twidling for-loop, so you use a normal wait()/waitpid() without WNOHANG. Your process is taken out of the execution queue until one of the children dies. But what if one of your children is *stopped* via a SIGSTOP? Your child is no longer working on the task you have set it to, but the parent is still waiting. So, you've got a deadlock, in a sense, unless the child is continued by some means external to your parent and that child. WUNTRACED allows your parent to be returned from wait()/waitpid() if a child gets *stopped* as well as exiting or being killed. This way, your parent has a chance to send it a SIGCONT to continue it, kill it, assign its tasks to another child, whatever.

> The **waitpid()** system call suspends execution of the calling process until a child specified by *pid* argument has changed state. By default, **waitpid()** waits **only for terminated children**, but this behavior is modifiable via the *options* argument...

**In a nutshell**

You can use the `WNOHANG` flag to indicate that the parent process **shouldn’t wait**; and the `WUNTRACED` flag to request status information from **stopped** processes as well as processes that have terminated.



