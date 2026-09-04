# Linux Navigation Commands

## pwd — Print Working Directory
Shows your current location in the filesystem.

```bash
pwd
# Output example: /home/kali
```

-Cybersecurity use: First command to run after getting 
shell access that tells you exactly where you are on the system.

---

## cd — Change Directory

```bash
cd /etc          # go to specific path
cd ..            # go one folder up
cd ~             # go to home directory
cd -             # go back to previous directory
```

-Important directories to know:
| Directory | Contains |
|-----------|---------|
| /etc | configuration files |
| /var/log | system log files |
| /home | user home directories |
| /tmp | temporary files |
| /bin | essential commands |
| /root | root user home directory |

---

## ls — List Directory Contents

```bash
ls              # basic listing
ls -l           # detailed listing with permissions
ls -la          # includes hidden files
ls -lh          # human readable file sizes
```

-Reading ls -la output:

| Field | Example | Meaning |
|-------|---------|---------|
| Type + Permissions | drwxr-xr-x | d=directory, rwx=owner, r-x=group, r-x=others |
| Links | 2 | number of hard links |
| Owner | kali | user who owns the file |
| Group | kali | group that owns the file |
| Size | 4096 | file size in bytes |
| Date | Aug 15 21:56 | last modified date and time |
| Name | Documents | file or folder name |

#Example output:
```bash
drwxr-xr-x 2 kali kali 4096 Aug 15 21:56 Documents
-rw-r--r-- 1 kali kali  220 Aug 15 21:56 .bash_logout
```

-Cybersecurity use: Finding hidden files starting with `.` 
that attackers might hide malware in:
