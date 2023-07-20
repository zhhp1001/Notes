# 32-bit file in 64-bit Linux

I have added ``/usr/local/arm/gcc-linaro-7.5.0-2019.12-i686_aarch64-elf/bin/` to `PATH` , but when I run this file

`/usr/local/arm/gcc-linaro-7.5.0-2019.12-i686_aarch64-elf/bin/aarch64-elf-gcc`

I got error message: 

```bash
hzhen@haipeng-pc:/usr/local/arm/gcc-linaro-7.5.0-2019.12-i686_aarch64-elf/bin$ ./aarch64-elf-gcc
-bash: ./aarch64-elf-gcc: No such file or directory
```

Also :

```bash
hzhen@haipeng-pc:/usr/local/arm/gcc-linaro-7.5.0-2019.12-i686_aarch64-linux-gnu/bin$ ls aarch64-elf-gcc
ls: cannot access 'aarch64-elf-gcc': No such file or directory
```

That's weird!

Then I copy a complied C file `test` to this path, and `./test` works fine...wow, things become interesting...

I use `file` command to detect these files:

```bash
hzhen@haipeng-pc:/usr/local/arm/gcc-linaro-7.5.0-2019.12-i686_aarch64-elf/bin$ file operators
operators: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/l, for GNU/Linux 3.2.0, BuildID[sha1]=ef884d98a72449f9573a2c4ffb5a411da2103653, not stripped
hzhen@haipeng-pc:/usr/local/arm/gcc-linaro-7.5.0-2019.12-i686_aarch64-elf/bin$ file aarch64-elf-gcc
aarch64-elf-gcc: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-, for GNU/Linux 2.6.24, BuildID[sha1]=95a1bca39d817eedef95b11c81d2374c9dce3c5b, stripped 
# This is the file worked on my PC
hzhen@haipeng-pc:/opt/intel/gcc-linaro-7.5.0-2019.12-x86_64_aarch64-elf/bin$ file aarch64-elf-gcc
aarch64-elf-gcc: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/l, for GNU/Linux 2.6.24, BuildID[sha1]=80f8b844b1c4ba69a6d3112c97607ae51df76dd7, stripped
```

and my Ubuntu is 

```bash
hzhen@haipeng-pc:/usr/local/arm/gcc-linaro-7.5.0-2019.12-i686_aarch64-elf/bin$ uname -m
x86_64
```

Things are getting clearer... I googled something about `run elf 32-bit lsb executable` and got the following advice:

>to run a 32-bit executable file on a 64-bit multi-architecture Ubuntu system, you have to add the `i386` architecture and install the three library packages `libc6:i386`, `libncurses5:i386`, and `libstdc++6:i386`
>
>`sudo dpkg --add-architecture i386`

After typing the following commands, the 32bit file became  alive.

```bash
$ sudo apt update
$ sudo apt install build-essential libc6-dev-i386
$ sudo dpkg --add-architecture i386
```



Here is a link about **Multiarch**

https://wiki.debian.org/Multiarch/HOWTO

