### import log/doc situations
```
/var/log ##where import system log files live
/usr/share/doc/  ##what docs for commands live
```

### users/permissions

- su = sub user OR switch user. thus ```su root``` switch to root

- visudo = alter sudoers files giving specific users specific priviledges
    - requires root priv

```bash
shutdown -r +0 ##reboot now
shutdown -s +0 ##shutdown now
shutdown -c ##cancel
```

- add users.
    - /etc/passwd : accounts stored here
    - /etc/login.defs : config for accounts 
    - /home/<directory_name> : home directories
        - /etc/skel/ : home directories use files from here. has template for .BASH_PROFILE/LOGOUT/RC
    - /etc/passwd : contains user/group other informations about users and applications
        - don't manually update this password: use USERADD
        ```
        user name:password (shows x):user id:group id:comment:home directory:default shell
        ```
    - useradd doesnt set password
    - /etc/shadow : stores hashed passwords, passwords requirements
        ```
        user name:password (hashed):days since password changed:days until changed:number of warn days till password:number of days after pass expired for account disable:days account has been disabled:unused
        ```
        

```bash
useradd [options] [username]

-c ##comment. any string. full name of user typically
-e 2021/12/31 ##set account expiration
-s /bin/csh ##set default shell
-D ##show default config for new users

passwd [options] [username]

chage [options] [username] ##change age of expiration
-l ##list all password change stats
-E 2023/01/23 ##change date of expiration

usermod [options] [username] ##change user info
-l rstan1 ##change login name

userdel [options] [username] ##change user info
-r rstan1 ##remove home directory and files
-f ##force delete

passwd -l [username] ##lock user
-u ##unlock
```

### groups
- add groups.
    - /etc/group : like passwd but for group
    ```bash
    group name:password(x):group id:group list
    ```

```bash
groupadd [options] [groupname]
groupadd -g 100 instructors

-g ##any string. for human readable group name
-f ##exits 1 if group already exists
-o ##create group with non-unique id

groupmod [options] [groupname] ##change group info
-g ##change group id
-n ##rename group

groupdel [options] [groupdel] ##delete group info, but not USERS
```

#### querying users and groups

```bash
whoami ##print current user

who [options] ##display user info
-u ##idle time. display . for current, old for > 24hrs
am i ##display for only current user (not all shells for example

w ##display details of currently logged users
```
