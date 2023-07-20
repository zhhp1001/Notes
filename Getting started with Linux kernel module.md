# Getting started with Linux kernel module

https://www.cyberciti.biz/tips/compiling-linux-kernel-module.html



## Example: hello.c module

1) hello.c C source code. Copy following code and save to hello.c
`$ mkdir demo; cd demo$ vi hello.c`

2)Add following c source code to it:

```C
#include <linux/module.h>
#include <linux/slab.h>
int init_module()
{

    printk(KERN_INFO "KMALLOC_SHILFT_LOW:%d\nKMALLOC_SHILFT_HIGH:%d\nKMALLOC_MIN_SIZE:%d\nKMALLOC_MAX_SIZE:%lu\nPAGE_SHIFT:%d\n",
            KMALLOC_SHIFT_LOW,  KMALLOC_SHIFT_HIGH, KMALLOC_MIN_SIZE, KMALLOC_MAX_SIZE, PAGE_SHIFT);
    return 0;
}

void cleanup_module()
{
    return;
}

MODULE_DESCRIPTION("Test module");
MODULE_AUTHOR("hzhen");
MODULE_LICENSE("GPL v2");
```

3) Save the file. Create new Makefile as follows:
`$ vim Makefile`
Append following make commands:

```
obj-m = hello.o
KVERSION = $(shell uname -r)
all:
        make -C /lib/modules/$(KVERSION)/build M=$(PWD) modules
clean:
        make -C /lib/modules/$(KVERSION)/build M=$(PWD) clean
```

4) Save and close the file.

5) Compile hello.c module:
`$ make`

6) Become a root user (use su or sudo) and load the module:
`$ sudo insmod hello.ko`

Note you can see message on screen if you are logged in as root under run level 3.

7) Verify that module loaded:
`# lsmod | less`

8) See message:
`dmesg`

9) Unload the module:
`sudo rmmod hello`

> 10) Load module when Linux system comes up. File /etc/modules use to load kernel boot time. This file should contain the names of kernel modules that are to be loaded at boot time, one per line. First copy your module to /lib/modules/$(uname -r)/kernel/drivers. Following are suggested steps:
>
> (a) Create directory for hello module:
> `# mkdir -p /lib/modules/$(uname -r)/kernel/drivers/hello`
> (b) Copy module:
> `# cp hello.ko /lib/modules/$(uname -r)/kernel/drivers/hello/`
> (c) Edit /etc/modules file under Debian Linux:
> `# vi /etc/modules`
> (d) Add following line to it:
> `hello`
> (e) Reboot to see changes. Use lsmod or dmesg command to verify module loaded or not.
> `# cat /proc/modules`
> OR
> `# lsmod | less`