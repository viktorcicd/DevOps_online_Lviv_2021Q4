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
```
 ps -eo user,comm,pid,group,gid
```
![linux](./images/56.png "linux")

6. How to define kernel processes and user processes?
```
ps -u username  (check processes for the specific users)
ps -ef | grep kthreadd (kernel process thread with PID 2)
pstree 2
```
![linux](./images/57.png "linux")

7. Print the list of processes to the terminal. Briefly describe the statuses of the processes. 
 What condition are they in, or can they be arriving in?
```
Almost all processes currently are in state Sleep
ps -aux
top
```
![linux](./images/58.png "linux")

8. Display only the processes of a specific user.
```
ps -u username
```
![linux](./images/59.png "linux")

9. What utilities can be used to analyze existing running tasks (by analyzing the help for the ps command)?
```
top
htop
pstree
grep
awk
```
10. What information does top command display?
```
The top program provides a dynamic real-time view of a running system. 
It can display system summary information as well as a list of processes
```
11. Display the processes of the specific user using the top command
```
top -u victor
```
![linux](./images/60.png "linux")

12. What interactive commands can be used to control the top command? Give a couple of examples.
```
k  :Kill-a-task
You will be prompted for a PID and then the signal to send.
u | U  :Show-Specific-User-Only
You  will be prompted for the uid or name of the user to display.
V  :Forest-View-Mode toggle
In this mode, processes are reordered according to their parents
i  :Idle-Process toggle
Displays all tasks or just active tasks.
```

13. Sort the contents of the processes window using various parameters (for example, the amount of processor time taken up, etc.)
```
he can sort interactively using command "htop" and clicking on the column
```
![linux](./images/61.png "linux")

14. Concept of priority, what commands are used to set priority?
```
The current priority of a process can be displayed using ps command.
The “NI” column in the ps command output indicates the current nice value (i.e priority) of a process.

renice -n -19 -p 3534
```
15. Can I change the priority of a process using the top command? If so, how?
```
Press r. Give PID value of the process you want to change the process value. 
Give renice value (from -20 to +19)
```
16. Examine the kill command. How to send with the kill commandprocess control signal? Give an example of commonly used signals.
```



