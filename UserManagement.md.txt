# User Management Commands

## Viewing Users

```bash
cat /etc/passwd          # view all users
cat /etc/shadow          # view hashed passwords (root only)
whoami                   # current user
id                       # current user ID and groups
groups username          # groups a user belongs to
```

## /etc/passwd Format

| Field | Example | Meaning |
|-------|---------|---------|
| Username | kali | login name |
| Password | x | password stored in /etc/shadow |
| UID | 1000 | user ID number |
| GID | 1000 | group ID number |
| Info | (empty) | full name or description |
| Home | /home/kali | user home directory |
| Shell | /usr/bin/zsh | shell assigned to user |

**Example entry:**
```bash
kali:x:1000:1000::/home/kali:/usr/bin/zsh
```

-Note: Real human users always have UID 1000 or above.
System/service accounts have UID below 1000.


Important shells:
| Shell | Meaning |
|-------|---------|
| /bin/bash | can login normally |
| /usr/bin/zsh | can login normally |
| /usr/sbin/nologin | cannot login — service account |
| /bin/false | cannot login — locked |

## Creating Users

```bash
adduser username          # interactive, creates home directory
useradd username          # basic, no home directory by default
useradd -m username       # with home directory
```

## Modifying Users

```bash
usermod -s /bin/bash username     # change shell
usermod -d /home/new username     # change home directory
usermod -d /home/new -m username  # change and move home directory
usermod -l newname oldname        # rename user
usermod -aG sudo username         # add to sudo group
usermod -L username               # lock account
usermod -U username               # unlock account
```

⚠️ Always use -aG not -G when adding to groups.
-G alone removes user from all other groups first.

## Deleting Users

```bash
userdel username              # delete user only
userdel -r username           # delete user and home directory
deluser username              # friendly version
deluser --remove-home username # with home directory
```

## Passwords

```bash
passwd username          # change user password
passwd -l username       # lock password
passwd -u username       # unlock password
```

## Groups

```bash
gpasswd -a username groupname    # add user to group
gpasswd -d username groupname    # remove user from group
cat /etc/group                   # view all groups
```

## sudo

```bash
sudo command             # run as root
sudo -u username command # run as specific user
sudo visudo              # safely edit sudoers file
```

## Switching Users

```bash
su username              # switch to user
su -                     # switch to root
exit                     # return to previous user
```