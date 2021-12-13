###Task1

Part1

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
auditd , acct (ac -p -d) lascomm
```

usermod -l victor victor2
chfn victor

man w -i -s
man acct
info passwd 


tree -P '*.png' --prune

