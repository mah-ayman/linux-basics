# User and Groups

linux there are 3 types of users

* Super user or root user
  The most powerful user - It's the administrator user
* System user
  Created by the software or applications
* Normal user
  Created by root user
  Only root user has the permission to create or remove a user

Type    | Example          | User ID       | Group ID      | Home Dir         | Shell
------- | ---------------- | ------------- | ------------- | ---------------- | -----------
Root    | root             | 0             | 0             | /root            | /bin/bash
Regular | zold, vagrant    | 1000 to 60000 | 1000 to 60000 | /home/{username} | /bin/bash
Service | ftp, ssh, apache | 1 to 999      | 1 to 999      | /var/ftp etc     | /sbin/nologin

## Show All Users

`cat /etc/passwd` → show all users

``` console
root@Zold:~# cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
```

Explaining syntax, will use the first account to explain

* `root` username
* `x` encrypted password stored in /etc/shadow file
* `0` user id
* `0` group id
* `root` comment
* `/root` home directory
* `/bin/bash` shell

## User Control Commands

At first, you must know something important:
In the commands to add, modify, or delete a user or group, you will find two different commands for the same thing, for example adding a user you will find `useradd` & `adduser` so what is the different between those?

`useradd` is native binary compiled with the system. But, `adduser` is a perl script which uses `useradd` binary in back-end.

`adduser` is more user friendly and interactive than its back-end `useradd`. There's no difference in features provided.

also `adduser` is a wrapper for `useradd`.

* `whoami` print effective userid
* `w` show who is logged on and what they are doing.

``` console
root@Zold:~# whoami
root

root@Zold:~# w
 13:38:04 up 56 min,  0 users,  load average: 0.00, 0.11, 0.07
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
```

* `id` print real and effective user and group IDs
* `id <Username>` Select a specific account username

``` console
root@Zold:~# id
uid=0(root) gid=0(root) groups=0(root)

root@Zold:~# id zold
uid=1000(zold) gid=1000(zold) groups=1000(zold),27(sudo),29(audio),30(dip),44(video),46(plugdev),117(netdev),1001(docker)
```

* `adduser <Username>` add a new user to your current Linux machine

``` console
root@Zold:~# adduser ashraf
Adding user `ashraf' ...
Adding new group `ashraf' (1004) ...
Adding new user `ashraf' (1003) with group `ashraf' ...
Creating home directory `/home/ashraf' ...
Copying files from `/etc/skel' ...
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for ashraf
Enter the new value, or press ENTER for the default
        Full Name []: Ashraf Osaama
        Room Number []: 10
        Work Phone []: 01039382745
        Home Phone []: 01139827388
        Other []:
Is the information correct? [Y/n] y
root@Zold:~# su - ashraf
ashraf@Zold:~$
```

* `deluser <Username>` delete user

``` console
root@Zold:~# deluser ali
Removing user `ali' ...
Done.
root@Zold:~#
```

* `su - <username>` switch user which login to machine

* `su -` or `sudo -i` login to root user

* `exit` Logout
