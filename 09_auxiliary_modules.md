# Auxiliary Modules

## What are Auxiliary Modules?
- Auxiliary modules are supporting modules in Metasploit Framework
- They do not exploit vulnerabilities directly
- Used for scanning enumeration fuzzing and brute forcing
- Over 1000 auxiliary modules available in Metasploit
- Essential for reconnaissance and information gathering
- Results saved to Metasploit database automatically
- First step before exploitation in penetration testing

---

## Auxiliary Module Categories
- Scanner modules → discover hosts and services
- Brute force modules → crack credentials
- Fuzzer modules → find vulnerabilities by fuzzing
- Server modules → run fake servers for attacks
- Denial of Service modules → test service resilience
- Spoof modules → spoof network traffic
- Gather modules → collect information

---

## Using Auxiliary Modules

### Basic Usage
```bash
# search for auxiliary modules
search type:auxiliary scanner
search type:auxiliary brute
search type:auxiliary fuzz

# use auxiliary module
use auxiliary/scanner/portscan/tcp

# show options
show options

# set required options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run module
run
```

---

## Port Scanning Modules

### TCP Port Scanner
```bash
use auxiliary/scanner/portscan/tcp
set RHOSTS 192.168.1.0/24
set PORTS 1-1000
set THREADS 50
run
```

### SYN Scanner
```bash
use auxiliary/scanner/portscan/syn
set RHOSTS 192.168.1.0/24
set PORTS 1-65535
set THREADS 50
run
```

### ACK Scanner
```bash
use auxiliary/scanner/portscan/ack
set RHOSTS 192.168.1.0/24
set PORTS 1-1000
run
```

### UDP Scanner
```bash
use auxiliary/scanner/portscan/udp
set RHOSTS 192.168.1.0/24
run
```

---

## Host Discovery Modules

### ARP Sweep
```bash
use auxiliary/scanner/discovery/arp_sweep
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### ICMP Sweep
```bash
use auxiliary/scanner/discovery/icmp_sweep
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### UDP Sweep
```bash
use auxiliary/scanner/discovery/udp_sweep
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

---

## Service Version Scanners

### SMB Version Scanner
```bash
use auxiliary/scanner/smb/smb_version
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### SSH Version Scanner
```bash
use auxiliary/scanner/ssh/ssh_version
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### FTP Version Scanner
```bash
use auxiliary/scanner/ftp/ftp_version
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### HTTP Version Scanner
```bash
use auxiliary/scanner/http/http_version
set RHOSTS 192.168.1.0/24
set RPORT 80
set THREADS 10
run
```

### SMTP Version Scanner
```bash
use auxiliary/scanner/smtp/smtp_version
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### MySQL Version Scanner
```bash
use auxiliary/scanner/mysql/mysql_version
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### MSSQL Version Scanner
```bash
use auxiliary/scanner/mssql/mssql_ping
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### RDP Scanner
```bash
use auxiliary/scanner/rdp/rdp_scanner
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### VNC Scanner
```bash
use auxiliary/scanner/vnc/vnc_login
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

---

## Vulnerability Scanners

### EternalBlue Scanner MS17-010
```bash
use auxiliary/scanner/smb/smb_ms17_010
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### BlueKeep Scanner CVE-2019-0708
```bash
use auxiliary/scanner/rdp/cve_2019_0708_bluekeep
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### Heartbleed Scanner
```bash
use auxiliary/scanner/ssl/openssl_heartbleed
set RHOSTS 192.168.1.0/24
set RPORT 443
set THREADS 10
run
```

### SMB Signing Scanner
```bash
use auxiliary/scanner/smb/smb_signing
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### ShellShock Scanner
```bash
use auxiliary/scanner/http/apache_mod_cgi_bash_env
set RHOSTS 192.168.1.0/24
set TARGETURI /cgi-bin/test.cgi
set THREADS 10
run
```

### Anonymous FTP Scanner
```bash
use auxiliary/scanner/ftp/anonymous
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### Open Relay Scanner SMTP
```bash
use auxiliary/scanner/smtp/smtp_relay
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

---

## Brute Force Modules

### SSH Brute Force
```bash
use auxiliary/scanner/ssh/ssh_login
set RHOSTS 192.168.1.1
set USERNAME root
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set THREADS 10
set VERBOSE false
set STOP_ON_SUCCESS true
run
```

### FTP Brute Force
```bash
use auxiliary/scanner/ftp/ftp_login
set RHOSTS 192.168.1.1
set USER_FILE /usr/share/metasploit-framework/data/wordlists/unix_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set THREADS 10
set VERBOSE false
set STOP_ON_SUCCESS true
run
```

### SMB Brute Force
```bash
use auxiliary/scanner/smb/smb_login
set RHOSTS 192.168.1.1
set USER_FILE /home/kali/users.txt
set PASS_FILE /home/kali/passwords.txt
set THREADS 10
set VERBOSE false
set STOP_ON_SUCCESS true
run
```

### HTTP Login Brute Force
```bash
use auxiliary/scanner/http/http_login
set RHOSTS 192.168.1.1
set RPORT 80
set AUTH_URI /login.php
set USER_FILE /home/kali/users.txt
set PASS_FILE /home/kali/passwords.txt
set THREADS 10
set VERBOSE false
run
```

### Telnet Brute Force
```bash
use auxiliary/scanner/telnet/telnet_login
set RHOSTS 192.168.1.1
set USERNAME admin
set PASS_FILE /home/kali/passwords.txt
set THREADS 10
set VERBOSE false
run
```

### MySQL Brute Force
```bash
use auxiliary/scanner/mysql/mysql_login
set RHOSTS 192.168.1.1
set USERNAME root
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set THREADS 10
set VERBOSE false
run
```

### MSSQL Brute Force
```bash
use auxiliary/scanner/mssql/mssql_login
set RHOSTS 192.168.1.1
set USERNAME sa
set PASS_FILE /home/kali/passwords.txt
set THREADS 10
set VERBOSE false
run
```

### VNC Brute Force
```bash
use auxiliary/scanner/vnc/vnc_login
set RHOSTS 192.168.1.1
set PASS_FILE /home/kali/passwords.txt
set THREADS 10
set VERBOSE false
run
```

### WordPress Login Brute Force
```bash
use auxiliary/scanner/http/wordpress_login_enum
set RHOSTS 192.168.1.1
set TARGETURI /wordpress/
set USERNAME admin
set PASS_FILE /home/kali/passwords.txt
run
```

---

## HTTP Auxiliary Modules

### HTTP Directory Scanner
```bash
use auxiliary/scanner/http/dir_scanner
set RHOSTS 192.168.1.1
set RPORT 80
set THREADS 10
set DICTIONARY /usr/share/metasploit-framework/data/wordlists/directory.txt
run
```

### HTTP File Scanner
```bash
use auxiliary/scanner/http/files_dir
set RHOSTS 192.168.1.1
set RPORT 80
run
```

### HTTP Header Scanner
```bash
use auxiliary/scanner/http/http_header
set RHOSTS 192.168.1.0/24
set RPORT 80
set THREADS 10
run
```

### HTTP Options Scanner
```bash
use auxiliary/scanner/http/options
set RHOSTS 192.168.1.0/24
set RPORT 80
set THREADS 10
run
```

### SSL Certificate Scanner
```bash
use auxiliary/scanner/http/ssl_version
set RHOSTS 192.168.1.0/24
set RPORT 443
set THREADS 10
run
```

### Web Application Firewall Scanner
```bash
use auxiliary/scanner/http/waf_w3edos
set RHOSTS 192.168.1.1
set RPORT 80
run
```

### WordPress Scanner
```bash
use auxiliary/scanner/http/wordpress_scanner
set RHOSTS 192.168.1.1
set TARGETURI /wordpress/
run
```

### Robots.txt Scanner
```bash
use auxiliary/scanner/http/robots_txt
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

---

## SMB Auxiliary Modules

### SMB Enumeration
```bash
use auxiliary/scanner/smb/smb_enumshares
set RHOSTS 192.168.1.1
set THREADS 10
run
```

### SMB Users Enumeration
```bash
use auxiliary/scanner/smb/smb_enumusers
set RHOSTS 192.168.1.1
set THREADS 10
run
```

### SMB Lookupsid
```bash
use auxiliary/scanner/smb/smb_lookupsid
set RHOSTS 192.168.1.1
run
```

### NetBIOS Scanner
```bash
use auxiliary/scanner/netbios/nbname
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

---

## DNS Auxiliary Modules

### DNS Enumeration
```bash
use auxiliary/gather/dns_enum
set DOMAIN target.com
run
```

### DNS Bruteforce
```bash
use auxiliary/gather/dns_bruteforce
set DOMAIN target.com
run
```

### DNS Cache Scraping
```bash
use auxiliary/gather/dns_cache_scraper
set RHOSTS 192.168.1.1
run
```

---

## SNMP Auxiliary Modules

### SNMP Scanner
```bash
use auxiliary/scanner/snmp/snmp_login
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### SNMP Enumeration
```bash
use auxiliary/scanner/snmp/snmp_enum
set RHOSTS 192.168.1.1
run
```

---

## Server Modules

### HTTP Server Fake
```bash
use auxiliary/server/capture/http
set SRVHOST 0.0.0.0
set SRVPORT 80
run
```

### HTTPS Server Fake
```bash
use auxiliary/server/capture/https
set SRVHOST 0.0.0.0
set SRVPORT 443
run
```

### FTP Server Fake
```bash
use auxiliary/server/capture/ftp
set SRVHOST 0.0.0.0
set SRVPORT 21
run
```

### SMB Server Fake
```bash
use auxiliary/server/capture/smb
set SRVHOST 0.0.0.0
set SRVPORT 445
run
```

### SOCKS Proxy Server
```bash
use auxiliary/server/socks_proxy
set SRVPORT 1080
set VERSION 5
run -j
```

---

## Fuzzer Modules

### HTTP Fuzzer
```bash
use auxiliary/fuzz/http_form_field
set RHOSTS 192.168.1.1
set RPORT 80
run
```

### FTP Fuzzer
```bash
use auxiliary/fuzz/ftp
set RHOSTS 192.168.1.1
run
```

### SMTP Fuzzer
```bash
use auxiliary/fuzz/smtp
set RHOSTS 192.168.1.1
run
```

---

## Gather Modules

### Email Harvester
```bash
use auxiliary/gather/search_email_collector
set DOMAIN target.com
run
```

### DNS Information Gathering
```bash
use auxiliary/gather/dns_info
set DOMAIN target.com
run
```

### Whois Lookup
```bash
use auxiliary/gather/whois_lookup
set QUERY target.com
run
```

---

## Wordlists Available in Metasploit
```bash
# location of metasploit wordlists
ls /usr/share/metasploit-framework/data/wordlists/

# common wordlists
unix_passwords.txt
unix_users.txt
default_userpass_for_services_unhashed.txt
http_default_users.txt
http_default_pass.txt
common_roots.txt
directory.txt
```

---
## Important Points
- Auxiliary modules do not exploit systems directly
- Always set THREADS carefully to avoid crashing services
- Use STOP_ON_SUCCESS for brute force to save time
- Set VERBOSE false for cleaner brute force output
- Results automatically saved to Metasploit database
- Use services and hosts commands to review scan results
- Combine multiple auxiliary modules for thorough reconnaissance
- Import external scan results with db_import command
- Always use auxiliary modules only on authorized targets
- Document all findings from auxiliary modules for reporting
```

---
