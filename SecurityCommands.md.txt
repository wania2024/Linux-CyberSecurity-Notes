# Security-Specific Commands

## File Integrity Verification

```bash
# Generate hash of file
sha256sum file.txt
md5sum file.txt

# Save hash for later comparison
sha256sum file.txt >> file.hash

# Compare two hash files
cmp file1.hash file2.hash
# No output = files identical
# Output = files differ — possible tampering
```

-Use case: Verify downloaded files haven't been tampered with.
Verify evidence files haven't been modified during investigation.

## Cryptography

```bash
# Encrypt a file
openssl aes-256-cbc -pbkdf2 -a -e -in file.txt -out file.encrypted -k password

# Decrypt a file
openssl aes-256-cbc -pbkdf2 -a -d -in file.encrypted -out file.recovered -k password

# Caesar cipher decode (Left Shift 3)
cat encryptedfile | tr "d-za-cD-ZA-C" "a-zA-Z"
```

## Security Auditing

```bash
# Find SUID files (privilege escalation targets)
find / -perm -4000 2>/dev/null

# Find world writable files
find / -perm -o+w -not -path "/proc/*" -not -path "/sys/*" 2>/dev/null

# Save SUID baseline for comparison
find / -perm -4000 2>/dev/null > suid_baseline.txt

# Compare current SUID files against baseline
find / -perm -4000 2>/dev/null > current_suid.txt
diff suid_baseline.txt current_suid.txt

# Remove SUID from file
sudo chmod -s /path/to/file
```

## Log Analysis

```bash
# View auth log
cat /var/log/auth.log
tail -f /var/log/auth.log

# Find failed login attempts
grep "Failed password" /var/log/auth.log

# Count failed attempts
grep "Failed password" /var/log/auth.log | wc -l

# Find attacking IPs
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -rn

# Web server logs
cat /var/log/nginx/access.log

# Find SQL injection attempts in logs
grep -i "union select" /var/log/nginx/access.log
grep -i "' or '1'='1" /var/log/nginx/access.log

# Find XSS attempts
grep -i "<script>" /var/log/nginx/access.log
```

## Subdomain Enumeration

```bash
# Install sublist3r
sudo apt install sublist3r

# Enumerate subdomains
sublist3r -d target.com
```

## Morning Security Check Script

```bash
#!/bin/bash
# morning_check.sh
# Run daily to check system security status

echo "=== FAILED LOGINS LAST 24 HOURS ==="
grep "Failed password" /var/log/auth.log | wc -l

echo "=== TOP ATTACKING IPs ==="
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -rn | head 10

echo "=== CURRENT LISTENING PORTS ==="
ss -tlnp

echo "=== RUNNING SERVICES ==="
systemctl list-units --type=service --state=running

echo "=== SUID FILES ==="
find / -perm -4000 2>/dev/null

echo "=== DISK USAGE ==="
df -h

echo "=== LAST 10 SUDO COMMANDS ==="
grep "sudo" /var/log/auth.log | tail 10
```

Save and make executable:
```bash
chmod +x morning_check.sh
./morning_check.sh
```