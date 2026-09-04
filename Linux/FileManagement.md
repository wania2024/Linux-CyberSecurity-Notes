# File Management Commands

## Creating Files and Directories

```bash
touch filename.txt        # create empty file
mkdir foldername          # create directory
mkdir -p path/to/folder   # create nested directories
```

---

## Copying and Moving

```bash
cp file.txt /destination/         # copy file
cp -r folder/ /destination/       # copy entire folder
mv file.txt /destination/         # move file
mv oldname.txt newname.txt        # rename file
```

---

## Deleting

```bash
rm file.txt          # delete file
rm -r foldername     # delete folder and contents
rm -rf foldername    # force delete without confirmation
```

⚠️ WARNING: rm -rf is permanent. No recycle bin. 
No undo. Always double check before running.

---

## Reading Files

```bash
cat file.txt          # print entire file
head file.txt         # first 10 lines
tail file.txt         # last 10 lines
tail -f file.txt      # watch file update live
less file.txt         # scroll through file
```

-Cybersecurity use:
```bash
tail -f /var/log/auth.log    # watch login attempts live
cat /etc/passwd              # view all user accounts
cat /etc/shadow              # view hashed passwords (needs root)
```

---

## Finding Files

```bash
find / -name "*.txt"                    # find by name
find / -iname "*.txt"                   # case insensitive
find / -mtime -3                        # modified last 3 days
find / -mmin -60                        # modified last 60 minutes
find / -perm -4000 2>/dev/null          # find SUID files
find / -perm -o+w 2>/dev/null           # find world writable files
```

-Cybersecurity use cases:
```bash
# Find recently modified files after suspected breach
find / -mtime -1 2>/dev/null

# Find hidden password files
find / -name "*password*" 2>/dev/null

# Find SUID files (privilege escalation targets)
find / -perm -4000 2>/dev/null

# Audit world writable files
find / -perm -o+w -not -path "/proc/*" -not -path "/sys/*" 2>/dev/null
```

---

## Searching Inside Files

```bash
grep "keyword" file.txt           # search in one file
grep -i "keyword" file.txt        # case insensitive
grep -r "keyword" /directory/     # search recursively
grep -n "keyword" file.txt        # show line numbers
grep -v "keyword" file.txt        # show lines NOT containing keyword
grep -c "keyword" file.txt        # count matching lines
```

-Cybersecurity use cases:
```bash
# Find failed login attempts
grep "Failed password" /var/log/auth.log

# Find SQL injection attempts in web logs
grep "union select" /var/log/nginx/access.log

# Search for passwords in config files
grep -r "password" /etc/ 2>/dev/null

# Find specific user in passwd file
grep "kali" /etc/passwd
```

---

## Output Redirection

```bash
command > file.txt     # overwrite file with output
command >> file.txt    # append output to file
command 2>/dev/null    # discard error messages
```

**Examples:**
```bash
ls > filelist.txt
find / -perm -4000 2>/dev/null > suid_files.txt
grep "Failed" /var/log/auth.log >> investigation_notes.txt
```