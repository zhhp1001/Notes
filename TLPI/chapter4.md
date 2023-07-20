## 4-1

```C
  1	#include <sys/stat.h>
  2 #include <unistd.h>
  3 #include <fcntl.h>
  4 #include "tlpi_hdr.h"
  5 #define BUF_SIZE 1024
  6
  7 int main(int argc, char *argv[]) {
  8     int fd;
  9     char c, buf[BUF_SIZE];
 10     int openFlags, appendFlag;
 11     mode_t filePerms;
 12     ssize_t numRead;
 13
 14     if (argc < 2 || strcmp(argv[1], "--help") == 0)
 15         usageErr("%s [-a] file\n", argv[0]);
 16
 17     while ((c = getopt(argc, argv, ":a")) != -1)
 18         switch(c) {
 19             case 'a':
 20                 appendFlag = 1;
 21                 break; //important
 22             default:
 23                 errExit("invalid flag %c", c);
 24         }
 25
 26     openFlags = O_CREAT | O_WRONLY;
 27     if (appendFlag == 1)
 28         openFlags |= O_APPEND;
 29     else
 30         openFlags |= O_TRUNC;
 31     filePerms = S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP | S_IROTH | S_IWOTH;
 32     fd = open(argv[optind], openFlags, filePerms);
 33     if (fd == -1)
 34         errExit("opening file %s %d", argv[optind], optind);
 35
 36     while ((numRead = read(STDIN_FILENO, buf, BUF_SIZE)) > 0){
 37         if (write(fd, buf, numRead) != numRead)
 38             fatal("write file");
 39         if (write(STDOUT_FILENO, buf, numRead) != numRead)
 40             fatal("write STDOUT");
 41     }
 42
 43     if (close(fd) == -1)
 44         errExit("close file");
 45
 46     exit(EXIT_SUCCESS);
 47 }
```

**处理可变参数**：Line17 `getopt()` 、Line32 `optind` 

`optind` is the index in `argv` of the first argv-element that is not an option.

Here is an example showing how `getopt()` is typically used. The key points to notice are:

- Normally, `getopt()` is called **in a loop**. When `getopt()` returns `-1`, indicating no more options are present, the loop terminates.
- A `switch` statement is used to dispatch on the return value from `getopt()`. In typical use, each case just sets a variable that is used later in the program.
- A second loop is used to process the remaining non-option arguments.(在本例中，`optind`只有一个，所以不需要`second loop`了)

  [Reference1](https://www.gnu.org/software/libc/manual/html_node/Example-of-Getopt.html)   [Reference2](https://man7.org/linux/man-pages/man3/getopt.3.html)

