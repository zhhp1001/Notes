# How to Find Zombie Process's Parent





```sh
ps aux | grep -w Z   # returns the zombies PID

ps o ppid {returned PID from previous command}   # returns the parent PID

kill -9 {the parent PID from previous command}
```





