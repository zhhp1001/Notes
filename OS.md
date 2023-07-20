byte code

三天时间，大致浏览了两本OS的书（Three easy pieces & Modern OS），感觉还是CSAPP更实用一些，前两本书涉及OS内容很广泛，CSAPP会更接近Programmer的视角...

## Process: An abstraction of a running program

A process is just an instance of an executing program, including the current values of the program counter, registers, and variables.

The real CPU switches back and forth from process to process, but to understand the system, it is much easier to think about a collection of processes running in (pseudo) parallel than to try to keep track of how the CPU switches from program to program.

- A process is an activity of some kind.
- A program is something that may be stored on disk, not doing anything.



In Unix, there is only one system call to create a new process: **fork**. This call creates an exact clone of the calling process. After the fork, the two processes, the parent and the child, have the same memory image, the same environment strings, and the same open files.



## Threads: Share an address space and all of its data among themselves

Each thread has its own **stack**.





## Schedule Activation

The goals of the scheduler activation work are to mimic the functionality of kernel threads, but with the better performance and greater flexibility usually associated with  threads packages implemented in user space.





## Interprocess Communication

If one process is using a shared variable or file, the other processes will be excluded from doing the same thing.



## Semaphore



## Mutex

In practice an integer often is used, with 0 meaning unlocked and all other values meaning locked.



## Address space

We call this abstraction the address space, and it is the running program's view of memory in the system.

Every address you see is virtual.



## Virtual Memory

Conceptually, **virtual memory** is an array of N contiguous bytes stored on disk.



## Malloc & Free

Payload / Overload



## C Pointer Declarations 

CSAPP Lecture 20 Dynamic Memory Allocation Advanced Concepts(67:45)

**C operators 优先级**

`()` `[]` `->`  优先级高于 `*`  `&`  



You look for operators on either side of that variable name, 

and you choose the one that has the highest precedence.

```c
int *p       //P is a pointer to int.
int *p[13]	 //p is an array[13] of pointer to int.
    		//(P is an array of 13 pointers, each of which points to an int	)
int *(p[13]) //p is an array[13] of pointer to int.
int **p		 //p is a pointer to a pointer to int.
int (*p)[13] //p is a pointer to an array[13] of int.
int *f()	 //f is a function returning a pointer to int.
int (*f)() 	 //f is a pointer to a function returning int.
int (*(*f())[13])() //f is a function returning  pointer to pointer to an 					    //array[13] of functions returning int.
```





 



 







