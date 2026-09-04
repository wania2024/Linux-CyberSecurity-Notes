# Linux File Permissions


## Permission Types

| Symbol | Number | Permission |
|--------|--------|-----------|
| r | 4 | read |
| w | 2 | write |
| x | 1 | execute |
| - | 0 | no permission |

## chmod — Change Permissions

```bash
# Numeric method
chmod 700 file    # owner full, group none, others none
chmod 755 file    # owner full, group rx, others rx
chmod 644 file    # owner rw, group r, others r
chmod 600 file    # owner rw only, nobody else

- Symbolic method
chmod u+x file    # add execute for owner
chmod g-w file    # remove write from group
chmod o-r file    # remove read from others
chmod ug=r file   # set user and group to read only
chmod -s file     # remove SUID bit
```

## SUID — Set User ID (Security Critical)

SUID files run with the file OWNER's permissions 
regardless of who executes them.

```bash
# Identify SUID files (s in permissions)
-rwsr-xr-x   # SUID set (s instead of x)
-rwxr-xr-x   # normal (no SUID)

# Find all SUID files on system
find / -perm -4000 2>/dev/null

# Remove SUID from file
sudo chmod -s /path/to/file
```

⚠️ SECURITY NOTE: SUID files are prime targets for 
privilege escalation attacks. Attackers specifically 
hunt for unexpected SUID files to gain root access.

Reference: gtfobins.github.io — database of SUID exploits.

## World Writable Files (Security Risk)

Files writable by everyone — potential security vulnerability.

```bash
# Find world writable files
find / -perm -o+w -not -path "/proc/*" -not -path "/sys/*" 2>/dev/null
```

⚠️ SECURITY NOTE: If a world writable script runs 
automatically as root via cron, an attacker can 
modify it to execute malicious commands as root.