# Networking Commands

## Checking Network Configuration

```bash
ip a                    # show all interfaces and IPs
ifconfig                # older alternative
ip route                # show routing table
```

## Testing Connectivity

```bash
ping 8.8.8.8            # test internet connectivity
ping google.com         # test DNS and connectivity
traceroute google.com   # trace route to destination
```

## Checking Ports and Connections

```bash
ss -tlnp                        # show listening ports
ss -tlnp | grep 80              # check specific port
netstat -an                     # all connections
netstat -an | grep ESTABLISHED  # active connections
```

## DNS Lookups

```bash
nslookup google.com     # DNS lookup
dig google.com          # detailed DNS lookup
host google.com         # simple DNS lookup
```

## curl — Fetching Web Content

```bash
curl https://google.com          # fetch webpage
curl -I https://google.com       # headers only
curl -v https://google.com       # verbose output
curl -O https://site.com/file    # download file
curl -L https://site.com         # follow redirects
```

-Cybersecurity use:
```bash
# Check web server type and version
curl -I http://target.com
# Response reveals: Server: nginx/1.30.1

# Check security headers
curl -I https://target.com | grep -i "strict\|content\|x-frame"
```

## Network Capture

```bash
sudo tcpdump -i eth0                  # capture all traffic
sudo tcpdump -i eth0 port 80          # capture HTTP only
sudo tcpdump -i eth0 src 192.168.1.5  # from specific IP
sudo tcpdump -i eth0 -w capture.pcap  # save to file
```

## SSH

```bash
ssh username@192.168.1.5        # connect to remote system
ssh -p 2222 username@host       # custom port
scp file.txt user@host:/path/   # copy file over SSH
```