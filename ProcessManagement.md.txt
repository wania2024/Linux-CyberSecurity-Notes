# Process Management Commands

## Viewing Processes

```bash
ps aux                    # all running processes
ps aux | grep nginx       # find specific process
top                       # live process monitor
htop                      # better live monitor
ps aux | grep root      # find all root processes
ps aux | grep -v root   # find all non-root processes
```

##ps aux output explained:

| Field | Example | Meaning |
|-------|---------|---------|
| USER | kali | user running the process |
| PID | 1234 | process ID number — unique identifier |
| %CPU | 0.0 | percentage of CPU being used |
| %MEM | 0.1 | percentage of RAM being used |
| VSZ | 4096 | virtual memory size in kilobytes |
| RSS | 1024 | actual RAM being used in kilobytes |
| TTY | ? | terminal associated with process (? means none) |
| STAT | Ss | process status |
| START | 14:01 | time process started |
| TIME | 0:00 | total CPU time used |
| COMMAND | nginx | the actual program running |

##STAT codes explained:

| Code | Meaning |
|------|---------|
| S | sleeping — waiting for something |
| s | session leader |
| R | running actively |
| Z | zombie — finished but not cleaned up |
| T | stopped |
| + | foreground process |

-Cybersecurity use:
Checking for suspicious processes running on the system.
Malware often disguises itself with names similar to 
legitimate system processes.



## Killing Processes

```bash
kill PID              # graceful stop
kill -9 PID           # force kill immediately
killall processname   # kill by name
```

## systemctl — Service Management

```bash
sudo systemctl start service      # start now
sudo systemctl stop service       # stop now
sudo systemctl restart service    # restart
sudo systemctl status service     # check status
sudo systemctl enable service     # start on boot
sudo systemctl disable service    # don't start on boot
sudo systemctl enable --now service  # enable and start together

# List services
systemctl list-units --type=service
systemctl list-units --type=service --state=running
```

## Scheduled Tasks — Cron

```bash
crontab -l            # list your cron jobs
crontab -e            # edit your cron jobs
cat /etc/crontab      # system-wide cron jobs
```


⚠️ SECURITY NOTE: Malware often installs itself 
as a cron job for persistence. Always check crontab 
during incident investigation.
