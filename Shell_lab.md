# Shell Lab

## Overview

If the first word is a build-in command, the shell immediately executes the command in the current process. Otherwise, the word is assumed to be the pathname of an executable program. In this case, the shell *forks* a child process, then loads and runs the program in the context of the child. The child processes created as a result of interpreting a single command line are known collectively as a *job*. In general, a job can consist of multiple child processes connected by Unix pipes.

If the command line ends with an ampersand `&`, then the job runs in the *background*, which means that the shell does not wait for the job to terminate  before printing the prompt and awaiting the next command line.  Thus, at any point in time, at most one job can be running in the foreground. However, an arbitrary number of jobs can run in the background.



## Specification

The `tsh` shell should have the following features:

- The prompt should be the string `tsh> `.
- The command line typed by the user should consist of a name and zero or more arguments, all separated by one or more spaces. If name is a built-in command, then `tsh` should handle it immediately and wait for the next command line. Otherwise, `tsh` should assume that name is the path of an executable file, which it loads and runs in the context of an initial child process (In this context, the term **job** refers to this initial *child process*).
- `tsh` need not support pipes ( | ) or I/O redirection (< and >).
- Typing `ctrl-c` / `ctrl-z`  should cause a **SIGINT** / **SIGSTP** signal to be *sent to the current foreground job*, as well as any *descendents* of that job (e.g., any child processes that it forked). If there is no foreground job, then the signal should have no effect.
- If the command line ends with an ampersand `&`, then `tsh` should run the job in the background. Otherwise, it should run the job in the foreground. 
- Each job can be identified by either a process ID (PID) or a job ID (JID), which is a positive integer assigned by `tsh`. JIDs should be denoted on the command line by the prefix `%`. For example, `%5` denotes `JID 5`, and `5` denotes `PID 5`. (We have provided you with all of the routines you need for manipulating the job list.)
- 

