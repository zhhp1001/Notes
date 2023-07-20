# setpgid

```c
int setpgid(pid_t pid, pid_t pgid);
```

`setpgid()` sets the PGID of the process specified by `pid` to `pgid`. 

If `pid` is zero, then the process ID of the calling process is used.

If `pgid` is zero, then the PGID of the process specified by `pid` is made the same as its process ID. 





the argument `sig` in sig_handler function 
