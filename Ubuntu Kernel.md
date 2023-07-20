Ubuntu Kernel

## Ref https://www.cyberciti.biz/faq/ubuntu-18-04-remove-all-unused-old-kernels/

## Find installed Linux Kernels in Debian, Ubuntu, Pop!_OS

Firstly, type the following dpkg command along with egrep command to display a list of all installed kernels on Ubuntu box:
```bash
dpkg --list | egrep -i --color 'linux-image|linux-headers'

//only list installed kernels
dpkg --list | grep -i -E --color 'linux-image|linux-kernel' | grep '^ii'
```

## Install new kernel
- list installable kernel version
```bash
sudo apt-cache search linux-image | grep generic
```

- install kernel
```bash
sudo apt-get install linux-image-5.4.0-100-generic
```
 
## Remove old kernel
```bash
sudo apt remove(or purge) linux-image-5.4.0-48-generic
sudo apt purge linux-image-5.4.0-48-generic
```