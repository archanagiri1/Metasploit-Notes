# Scanning with Metasploit

## What is Scanning in Metasploit?
- Scanning is the process of discovering targets and services
- Metasploit has many built in scanning modules
- Auxiliary modules are used for scanning
- Results are saved to Metasploit database automatically
- Scanning helps find vulnerabilities before exploitation
- First step in penetration testing after reconnaissance

---

## Why Scan with Metasploit?
- Results automatically saved to database
- Easier to manage large scope engagements
- Integrates with exploitation modules directly
- Can import external scan results like Nmap
- Organizes findings by host and service
- Faster workflow from scan to exploit

---

## Types of Scanning in Metasploit

### Port Scanning
- Finding open ports on target hosts
- Identifies running services
- First step in active reconnaissance

### Service Version Detection
- Finding exact version of running services
- Helps identify vulnerable versions
- Used to find matching exploits

### Vulnerability Scanning
- Finding specific vulnerabilities on targets
- Uses auxiliary modules for each vulnerability
- More targeted than general port scanning

### Credential Scanning
- Testing default or weak credentials
- Brute forcing login services
- Used on SSH FTP HTTP SMB etc

---

## Starting Database Before Scanning
```bash
# start postgresql
sudo service postgresql start

# initialize metasploit database
sudo msfdb init

# start msfconsole
msfconsole -q

# verify database connection
db_status
```

---

## Port Scanning Modules

### TCP Port Scanner
```bash
# use TCP port scanner
use auxiliary/scanner/portscan/tcp

# show options
show options

# set target
set RHOSTS 192.168.1.1
set RHOSTS 192.168.1.0/24
set RHOSTS 192.168.1.1-192.168.1.254

# set port range
set PORTS 1-1000
set PORTS 21,22,23,25,80,443,445,3389
set PORTS 1-65535

# set threads for speed
set THREADS 10
set THREADS 50
set THREADS 100

# run scan
run
```

### SYN Port Scanner
```bash
# use SYN scanner stealth scan
use auxiliary/scanner/portscan/syn

# set options
set RHOSTS 192.168.1.0/24
set PORTS 1-1000
set THREADS 50

# run
run
```

### ACK Port Scanner
```bash
# use ACK scanner for firewall detection
use auxiliary/scanner/portscan/ack

# set options
set RHOSTS 192.168.1.1
set PORTS 1-1000

# run
run
```

### UDP Port Scanner
```bash
# use UDP scanner
use auxiliary/scanner/discovery/udp_sweep

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### FIN Port Scanner
```bash
# use FIN scanner
use auxiliary/scanner/portscan/ftpbounce

# set options
set RHOSTS 192.168.1.1
set PORTS 1-1000

# run
run
```

---

## Host Discovery Modules

### ARP Sweep
```bash
# discover hosts on local network
use auxiliary/scanner/discovery/arp_sweep

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### ICMP Sweep
```bash
# discover hosts using ping
use auxiliary/scanner/discovery/icmp_sweep

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### UDP Sweep
```bash
# discover hosts using UDP
use auxiliary/scanner/discovery/udp_sweep

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

---

## Service Specific Scanners

### SMB Scanner
```bash
# scan for SMB service
use auxiliary/scanner/smb/smb_version

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### SSH Scanner
```bash
# scan for SSH version
use auxiliary/scanner/ssh/ssh_version

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### FTP Scanner
```bash
# scan for FTP version
use auxiliary/scanner/ftp/ftp_version

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### HTTP Scanner
```bash
# scan for HTTP version
use auxiliary/scanner/http/http_version

# set options
set RHOSTS 192.168.1.0/24
set RPORT 80
set THREADS 10

# run
run
```

### RDP Scanner
```bash
# scan for RDP service
use auxiliary/scanner/rdp/rdp_scanner

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### MySQL Scanner
```bash
# scan for MySQL service
use auxiliary/scanner/mysql/mysql_version

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### MSSQL Scanner
```bash
# scan for MSSQL service
use auxiliary/scanner/mssql/mssql_ping

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

---

## Vulnerability Specific Scanners

### EternalBlue Scanner MS17-010
```bash
# check for MS17-010 vulnerability
use auxiliary/scanner/smb/smb_ms17_010

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### BlueKeep Scanner CVE-2019-0708
```bash
# check for BlueKeep vulnerability
use auxiliary/scanner/rdp/cve_2019_0708_bluekeep

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### SMB Signing Scanner
```bash
# check SMB signing configuration
use auxiliary/scanner/smb/smb_signing

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

### Heartbleed Scanner
```bash
# check for Heartbleed vulnerability
use auxiliary/scanner/ssl/openssl_heartbleed

# set options
set RHOSTS 192.168.1.0/24
set RPORT 443
set THREADS 10

# run
run
```

### ShellShock Scanner
```bash
# check for ShellShock vulnerability
use auxiliary/scanner/http/apache_mod_cgi_bash_env

# set options
set RHOSTS 192.168.1.0/24
set THREADS 10

# run
run
```

---

## Credential Scanning Modules

### SSH Login Scanner
```bash
# brute force SSH login
use auxiliary/scanner/ssh/ssh_login

# set options
set RHOSTS 192.168.1.1
set USERNAME root
set PASSWORD toor
set USERPASS_FILE /usr/share/metasploit-framework/data/wordlists/default_userpass_for_services_unhashed.txt
set THREADS 10
set VERBOSE false

# run
run
```

### FTP Login Scanner
```bash
# brute force FTP login
use auxiliary/scanner/ftp/ftp_login

# set options
set RHOSTS 192.168.1.1
set USER_FILE /usr/share/metasploit-framework/data/wordlists/unix_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set THREADS 10
set VERBOSE false

# run
run
```

### SMB Login Scanner
```bash
# brute force SMB login
use auxiliary/scanner/smb/smb_login

# set options
set RHOSTS 192.168.1.1
set SMBUser administrator
set SMBPass password123
set USER_FILE /home/kali/users.txt
set PASS_FILE /home/kali/passwords.txt
set THREADS 10
set VERBOSE false

# run
run
```

### HTTP Login Scanner
```bash
# brute force HTTP login
use auxiliary/scanner/http/http_login

# set options
set RHOSTS 192.168.1.1
set RPORT 80
set AUTH_URI /login
set USER_FILE /home/kali/users.txt
set PASS_FILE /home/kali/passwords.txt
set THREADS 10

# run
run
```

### MySQL Login Scanner
```bash
# brute force MySQL login
use auxiliary/scanner/mysql/mysql_login

# set options
set RHOSTS 192.168.1.1
set USERNAME root
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set THREADS 10
set VERBOSE false

# run
run
```

---

## Scanning with Nmap Integration

### db_nmap Command
```bash
# run nmap and save to database
db_nmap -sV 192.168.1.1
db_nmap -sV -sC 192.168.1.0/24
db_nmap -A 192.168.1.1
db_nmap -p 1-65535 -sV 192.168.1.1
db_nmap -sU -p 53,67,68,161 192.168.1.1

# view results
hosts
services
```

### Importing Nmap Results
```bash
# run nmap outside metasploit and save to xml
# in terminal:
nmap -sV -oX scan_results.xml 192.168.1.0/24

# import into metasploit
db_import /home/kali/scan_results.xml

# view imported results
hosts
services
```

---

## Viewing Scan Results

### Hosts Command
```bash
# show all discovered hosts
hosts

# show specific columns
hosts -c address,mac,name,os_name,purpose,info

# search for specific host
hosts -S 192.168.1.1

# export hosts to file
hosts -o /home/kali/hosts.csv
```

### Services Command
```bash
# show all discovered services
services

# show services for specific host
services -H 192.168.1.1

# show services on specific port
services -p 445
services -p 80

# show services by state
services -s open

# show services by name
services -S http
services -S ssh
services -S smb

# export services to file
services -o /home/kali/services.csv
```

---

## Scanning Workflow

### Step 1 - Setup
```bash
# start database
sudo service postgresql start
msfconsole -q
db_status

# create workspace
workspace -a scan_project
```

### Step 2 - Host Discovery
```bash
# find alive hosts
use auxiliary/scanner/discovery/arp_sweep
set RHOSTS 192.168.1.0/24
set THREADS 10
run

# view hosts found
hosts
```

### Step 3 - Port Scanning
```bash
# scan open ports
use auxiliary/scanner/portscan/tcp
set RHOSTS 192.168.1.0/24
set PORTS 1-1000
set THREADS 50
run

# view services found
services
```

### Step 4 - Service Version Detection
```bash
# run nmap version scan
db_nmap -sV 192.168.1.0/24

# view detailed results
services
```

### Step 5 - Vulnerability Scanning
```bash
# check for specific vulnerabilities
use auxiliary/scanner/smb/smb_ms17_010
set RHOSTS 192.168.1.0/24
set THREADS 10
run
```

### Step 6 - Review Results
```bash
# view all findings
hosts
services
vulns
notes
```

---
## Important Points
- Always start postgresql before scanning
- Use workspace to organize scan results
- Set THREADS carefully high threads can crash targets
- Use db_nmap to save nmap results automatically
- Always check services command after scanning
- Combine multiple scanners for complete picture
- Import external scan results with db_import
- Export results with hosts -o and services -o
- Always scan only authorized targets
- Document all findings for reporting
```

---

