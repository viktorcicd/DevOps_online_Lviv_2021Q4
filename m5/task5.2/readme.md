1. Structure etc/passwd and etc/group:

```
victor:x:1000:1000:victor,,123456789,380322204:/home/victor:/bin/bash

victor - username
x - password
1000 - user ID
1000 - group ID
123456789,380322204 - user info
/home/victor - user home directory
/bin/bash - command line 

victor:x:1000:

victor - group name
x - group password 
1000 - group id
also there can be group members field with the list of user that are in this group

```
Pseudo users:

```
pseudo users are pre-defined users such as 'mail', 'uucp, 'nobody', etc...).

