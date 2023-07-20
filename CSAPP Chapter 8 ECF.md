# CSAPP Chapter 8 ECF



## Zombie process

​	When a process is terminated for any reason, the kernel does not remove it from the system immediately. Instead, the process is kept around in a terminated state until it is *reaped* by its parent.

​	When the parent reaps the terminated child, the kernel passes the child's exit status to the parent and then discards the terminated process, at which point it ceases to exist. A terminated process that has not yet been reaped is called a *zombie*.

​	A zombie process is similar in the sense that although it has already terminated, the kernel maintains some of its state until it can be reaped by the parent.



## Signal

​	A signal is a small message that notifies a process that an event of some type has occurred in the system. Each signal type corresponds to some kind of system event.

​	When a child process **terminates** or **stops**, the kernel sends a **SIGCHLD** signal to the parent.

​	A signal that has been sent but not yet received is called a *pending signal*. At any point in time, there can be **at most one** pending signal of a particular type. If a process has a pending signal of type k, then any subsequent signals of type k sent to that process are not queued; they are simply discarded.

​	A process can selectively ***block*** the receipt of certain signals. When a signal is  blocked, it can be delivered, but the resulting pending signal will not be received until the process unblocks the signal.

​	One of the nonintuitive aspects of signals is that **pending signals are not queued**. Because the pending bit vector contains exactly **one bit for each type of signal**, there can be at most one pending signal of any particular type. Thus, if two signals of type k are sent to a destination process while signal k is blocked because the destination process is currently executing a handler for signal k, then the second signal is simply discarded; it is not queued. The key idea is that the existence of a
pending signal merely indicates that at least one signal has arrived.  

​	To see how this affects correctness, let's look at a simple application that is similar in nature to real programs such as shells and Web servers. The basic structure is that a parent process creates some children that run independently for a while and then terminate. The parent must reap the children to avoid leaving zombies in the system. But we also want the parent to be free to do other work while the children are running. So we also want the parent to be free to do other work while the children are running. So we decide to reap the children with a *SIGCHLD* handler, instead of explicitly waiting for the children to terminate. (Recall that the kernel sends a SIGCHLD signal to the parent whenever one of its children **terminates or stops**.)

 

## waitpid

​	The **waitpid()** system call suspends execution of the calling process until a child specified by *pid* argument has changed state. By default, **waitpid()** waits only for terminated children, but this behavior is modifiable via the *options* argument...
