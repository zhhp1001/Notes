# Signal Concepts

## Pending and Blocked Signals

- A signal is *pending* if sent but not yet received
  - There can be at most one pending signal of any particular type
  - Signals are never queued
    - if a process has a pending signal of type k, then subsequent signals of type k that are sent to that process are discarded
- A process can *block* the receipt of certain signals
  - Blocked signals can be delivered, but will not be received until the signal is unblocked
- A pending signal is received at most once



## Blocking and Unblocking Signals

- **Implicit blocking mechanism**
  - Kernel blocks any pending signals of type currently being handled.
  - E.g., A SIGINT handler can't be interrupted by another SIGINT
- Explicit blocking and unblocking mechanism
  - `sigprocmask` function



## A question about figure 8-42

The code in figure 8-42 (from `csapp P546`) is about `sigsuspend`.

To better understand the concept of `sigsuspend ` I made two modifications as following, and got different output.

1. **Add line 10**

```C
  1 /* $begin sigsuspend */
  2 #include "csapp.h"
  3
  4 volatile sig_atomic_t pid;
  5
  6 void sigchld_handler(int s)
  7 {
  8     int olderrno = errno;
  9     pid = Waitpid(-1, NULL, 0);
 10     printf("Reap child %d\n", pid);
 11     errno = olderrno;
 12 }
 13
 14 void sigint_handler(int s)
 15 {
 16 }
 17
 18 int main(int argc, char **argv)
 19 {
 20     sigset_t mask, prev;
 21
 22     Signal(SIGCHLD, sigchld_handler);
 23     Signal(SIGINT, sigint_handler);
 24     Sigemptyset(&mask);
 25     Sigaddset(&mask, SIGCHLD);
 26
 27     while (1) {
 28         Sigprocmask(SIG_BLOCK, &mask, &prev); /* Block SIGCHLD */
 29         if (Fork() == 0) /* Child */
 30             exit(0);
 31         /* Wait for SIGCHLD to be received */
 32         pid = 0;
 33         while (!pid)
 34             Sigsuspend(&prev);
 35
 36         /* Optionally unblock SIGCHLD */
 37         Sigprocmask(SIG_SETMASK, &prev, NULL);
 38
 39         /* Do some work after receiving SIGCHLD */
 40         printf(".");
 41     }
 42     exit(0);
 43 }
 44 /* $end sigsuspend */
```

Use `kill -9 processID` to kill the process in another terminal, and got the following message, which confused me, why there was two `.` before each `Reap child` ? 

```bash
Reap child 11880
..Reap child 11881
..Reap child 11882
..Reap child 11883
..Reap child 11884
..Reap child 11885
..Reap child 11886
..Reap child 11887
..Reap child 11888
..Reap child 11889
..Reap child 11890
..Reap child 11891
..Reap child 11892
..Reap child 11893
..Reap child 11894
..Reap child 11895
..Reap child 11896
..Reap child 11897
..Reap child 11898
..Reap child 11899
..Reap child 11900
Killed
```



Then, **Add line 30**

```C
  1 /* $begin sigsuspend */
  2 #include "csapp.h"
  3
  4 volatile sig_atomic_t pid;
  5
  6 void sigchld_handler(int s)
  7 {
  8     int olderrno = errno;
  9     pid = Waitpid(-1, NULL, 0);
 10     printf("Reap child %d\n", pid);
 11     errno = olderrno;
 12 }
 13
 14 void sigint_handler(int s)
 15 {
 16 }
 17
 18 int main(int argc, char **argv)
 19 {
 20     sigset_t mask, prev;
 21
 22     Signal(SIGCHLD, sigchld_handler);
 23     Signal(SIGINT, sigint_handler);
 24     Sigemptyset(&mask);
 25     Sigaddset(&mask, SIGCHLD);
 26
 27     while (1) {
 28         Sigprocmask(SIG_BLOCK, &mask, &prev); /* Block SIGCHLD */
 29         if (Fork() == 0) {/* Child */
 30             printf("Create child %d\n", getpid());
 31             exit(0);
 32         }
 33         /* Wait for SIGCHLD to be received */
 34         pid = 0;
 35         while (!pid)
 36             Sigsuspend(&prev);
 37
 38         /* Optionally unblock SIGCHLD */
 39         Sigprocmask(SIG_SETMASK, &prev, NULL);
 40
 41         /* Do some work after receiving SIGCHLD */
 42         printf(".");
 43     }
 44     exit(0);
 45 }
 46 /* $end sigsuspend */

```

Use `kill -9 processID` to kill the process in another terminal, and got the message which exactly what I imaged.

```bash
hzhen@haipeng-pc:~/playground/csapp/ecf$ ./sigsuspend
Create child 15080
Reap child 15080
.Create child 15081
.Reap child 15081
.Create child 15082
.Reap child 15082
.Create child 15083
.Reap child 15083
.Create child 15084
.Reap child 15084
.Create child 15085
Killed
```

Why there could be such difference by only adding a `printf` line?



## Answer

[Here is answer from stackoverflow](https://stackoverflow.com/questions/67053580/confused-about-the-output-message-about-signal-handler-and-sigsuspend/67053760#67053760)

The key point is `This stdout buffer is inherited by the child process`

**Reference**

[1] TLPI - P445



Disable buffering of stdout `setbuf(stdout, NULL);`  



# TTY process group ID (tpgid)



## How CTRL+C works

The first thing is to understand how CTRL+C works.

When you press CTRL+C, your terminal emulator sends an ETX character (end-of-text / 0x03).
The TTY is configured such that when it receives this character, it sends a SIGINT to the **foreground process group of the terminal**. This configuration can be viewed by doing `stty -a` and looking at `intr = ^C;`. The [POSIX specification](http://pubs.opengroup.org/onlinepubs/000095399/basedefs/xbd_chap11.html#tag_11_01_09) says that when INTR is received, it should send a SIGINT to the foreground process group of that terminal.

## What is the foreground process group?

So, now the question is, how do you determine what the foreground process group is? The foreground process group is simply the group of processes which will receive any signals generated by the keyboard (SIGTSTP, SIGINT, etc).

Simplest way to determine the process group ID is to use `ps`:

```bsh
ps ax -O tpgid
```

The second column will be the process group ID.

## How do I send a signal to the process group?

Now that we know what the process group ID is, we need to simulate the POSIX behavior of sending a signal to the entire group.

This can be done with `kill` by putting a `-` in front of the group ID.
For example, if your process group ID is 1234, you would use:

```bsh
kill -INT -1234
```

## `tpgid` and `pgid` are not the same thing

> Important note: `tpgid` and `pgid` are not the same thing. `pgid` is the process group id, while `tpgid` is the terminal process group id. From within a process you can change its `pgid` using os.setpgid() for example, **but this does not change** the `tpgid`.

In this section, I define  `sigint_handler`  to check whether a child process exit by SIGINT will be processed by `sigchld_handler` , and set child process group ID to it's PID `setpgid(0, 0)`, so the SIGINT will sent to the tty process group id, while the child process is in another group...only the parent process will received the SIGINT.

```C
/* $begin sigsuspend */
#include "csapp.h"

volatile sig_atomic_t pid;
volatile sig_atomic_t parent_pid;

void sigchld_handler(int s)
{
    int olderrno = errno;
    int status;
    while( (pid = waitpid(-1, &status, 0)) > 0 ) {
        if (WIFSIGNALED(status)) {
            printf("Process: %d reaped because signal %d\n", pid, WTERMSIG(status));
        } else {
                printf("Reap child %d\n", pid);
        }
    }

    errno = olderrno;
}

void sigint_handler(int s)
{
    pid_t pid = getpid();
    if ( pid == parent_pid )
        printf("Parent process caught SIGINT\n");
    else {
        /* set sigint_handler to default version */
        Signal(SIGINT, SIG_DFL);
        printf("Caught SIGINT in process %d\n", getpid());
        kill(pid, SIGINT);
        //exit(0);
    }
}

int main(int argc, char **argv)
{
    sigset_t mask, prev;

    Signal(SIGCHLD, sigchld_handler);
    Signal(SIGINT, sigint_handler);
    Sigemptyset(&mask);
    Sigaddset(&mask, SIGCHLD);
        setbuf(stdout, NULL);
    parent_pid = getpid();
    printf("Parent process is %d\n", parent_pid);

    while (1) {
        Sigprocmask(SIG_BLOCK, &mask, &prev); /* Block SIGCHLD */
        if (Fork() == 0) {/* Child */
            setpgid(0, 0);
                        printf("Create child %d\n", getpid());
//          exit(0);
                }
        /* Wait for SIGCHLD to be received */
        pid = 0;
        while (!pid)
            Sigsuspend(&prev);

        /* Optionally unblock SIGCHLD */
        Sigprocmask(SIG_SETMASK, &prev, NULL); /* If you comment this line, remember current block status is `SIGCHLD blocked,
                * when the program excecuting Sigprocmask from the beginning of the loop, `prev` will be saved as `SIGCHLD blocked`
                `*/

        /* Do some work after receiving SIGCHLD */
        printf(".");
//              fflush(stdout);
    }
    exit(0);
}
/* $end sigsuspend */

```



# execve overwrite address space



**Q:**

I wrote a signal handler for a process, and fork() after that, the signal handler will be applied to both parent and child processes. If I replace the child process with "exec", the signal handler is no more.

I know this happens because "exec" call will overwrite the child process address space with it's own. I just want to know if there is a way to make signal handler work even after "exec" call ?

**A:**

No. From the `man` pages:

> execve() does not return on success, and the text, data, bss, and stack of the calling process are overwritten by that of the program loaded. The program invoked inherits the calling process's PID, and any open file descriptors that are not set to close on exec. Signals pending on the calling process are cleared. Any signals set to be caught by the calling process are reset to their default behaviour. The SIGCHLD signal (when set to SIG_IGN) may or may not be reset to SIG_DFL.

In fact, if the signal handler were still active after the code had been replaced with some very different code, you could expect all sorts of mayhem when the signal occurred. The signal handler is, after all, just an address to call when something happens (discounting `SIG_IGN` and `SIG_DFL` for now). Who knows what piece of code would be at that address when you replace the entire text segment?

> Note however that the process signal mask does survive the exec.



[Reference](https://stackoverflow.com/questions/2333637/is-it-possible-to-signal-handler-to-survive-after-exec)



So, in this case, we'd better reap child processes in sigchld handler installed in parent process. 







