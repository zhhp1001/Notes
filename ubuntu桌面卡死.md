## ubuntu桌面卡死

- `Ctrl-Alt-F3` enter to`tty3`
- `ps -t tty2 | grep Xorg` 
- kill `Xorg's PID` 
- Back to `tty1` 











**The Console Behind the Curtain**

Even if we have no terminal emulator running, several terminal sessions continue to run behind the graphical desktop. We can access these sessions, called **virtual terminals or virtual consoles**, by pressing `Ctrl-Alt-F1` through `Ctrl-Alt-F6` on most Linux distributions. When a session is accessed, it presents a login prompt into which we can enter our username and password. To switch from one virtual console to another, press `Alt-F1` through `Alt-F6`. On most system we can return to the graphical desktop by pressing `Alt-F7`.