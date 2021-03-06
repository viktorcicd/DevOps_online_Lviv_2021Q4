## Task 1

### Part 1

login as root:
```
sudo su
```
```
passwd victor
etc/passwd
etc/shadow
```
Following commands can be used to determine registered
users and history/log of excuted commands:
```
passwd -a -S
w
history
auditd , ac -p -d lascomm
```

To change personal info:
```
usermod -l victor victor2
chfn victor
```
Checked manual on the following commands:
```
man w
man acct
info passwd 

w -i -s  to use the short format and display ip address
ac -p -d  Print totals for each day for each user

man finger
```
Checking list of directories with ls:
```
ls -alh
```
![ls](./images/ls2.png "ls")

### Part 2

I used the following commands:
```
tree -L -P '*c*'
tree -P '*.png' --prune
```
![tree](./images/c.png "tree")

![tree](./images/tree.png "tree")

Checking the file type with the following command:

```
file
```

![file](./images/type.png "file")

To move directly to home directory used:
```
cd
cd ~

Absolute:
cd /home/victor
```
Checking ls with several options:
```
ls -a -l -h
ls github -R

option -a allow to see hidden files and catalogs
option -l provide information about size,permissions,ownership, etc..
```
![lsr](./images/lsr.png "lsr")

Performing following operations:
```
cd
mkdir mytest
cd mytest
ls -alh / > rootinfo
nano rootinfo
cp rootinfo ~/
cp rootinfo /home/victor
cd
rm -R mytest
rm rootinfo
```
Performing the following operations:
```
mkdir test
cp .bash_history test/labwork2
cd test
ln labwork2
ln -s labwork2
```
![link](./images/link.png "link")

![link](./images/link2.png "link")

```
hard link specified path to the body of the file so it was still 
working even after deletion of the original file
```
Using locate:
```
locate -A squid
locate -A traceroute
```
To check partitions:
```
df
```


