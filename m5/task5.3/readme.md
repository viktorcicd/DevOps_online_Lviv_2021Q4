## Part 1

1. How many states could has a process in Linux?
```
5 Possible states:

Running or Runnable (R)
Uninterruptible Sleep (D)
Interruptable Sleep (S)
Stopped (T)
Zombie (Z)
```

![linux](./images/51.png "linux")

![linux](./images/52.png "linux")

2. Examine the pstree command. Make output (highlight) the chain (ancestors) of the current process.
```
pstree is a Linux command that shows the running processes as a tree. It is used as a more visual alternative to the ps command.
```
![linux](./images/53.png "linux")
 
3. What is a proc file system?
```
Proc file system (procfs) is virtual file system created on fly when system boots,
contains useful information about the processes that are currently running
ls -l /proc
```
4. Print information about the processor (its type, supported technologies, etc.).
```
lscpu
cat /proc/cpuinfo
```
![linux](./images/54.png "linux")

![linux](./images/55.png "linux")

5. Use the ps command to get information about the process. The information should be as follows: the owner of the process, 
the arguments with which the process was launched for execution, the group owner of this process, etc.






