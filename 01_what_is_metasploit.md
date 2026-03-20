# What is Metasploit?

## Introduction
- Metasploit is the world's most used penetration testing framework
- Developed by H.D. Moore in 2003
- Now maintained by Rapid7
- Open source and free to use
- Written in Ruby programming language
- Used by ethical hackers and security professionals worldwide
- Comes pre-installed on Kali Linux

---

## What Can Metasploit Do?
- Scan and enumerate targets
- Find vulnerabilities in systems
- Exploit vulnerabilities
- Gain access to target systems
- Perform post exploitation activities
- Generate payloads and backdoors
- Conduct social engineering attacks
- Perform password attacks
- Pivot through networks

---

## Metasploit Editions

### Metasploit Framework
- Free and open source version
- Command line interface
- All basic features included
- Used by most security professionals
- Available on Kali Linux by default

### Metasploit Pro
- Paid commercial version
- Web based GUI interface
- Advanced features and automation
- Used by enterprise security teams
- Includes reporting features

---

## Metasploit Components

### Modules
- Reusable pieces of code
- Each module performs specific task
- Five types of modules:
  - Exploits
  - Payloads
  - Auxiliaries
  - Post
  - Encoders

### Exploits
- Code that takes advantage of vulnerability
- Targets specific software and version
- Delivers payload to target system
- Example: EternalBlue for Windows SMB

### Payloads
- Code that runs on target after exploitation
- Gives attacker control of target
- Types: singles stagers stages
- Example: Meterpreter reverse shell

### Auxiliary Modules
- Modules that do not exploit systems
- Used for scanning enumeration and fuzzing
- Example: port scanner version detector

### Post Modules
- Run after successful exploitation
- Used for privilege escalation
- Used for data collection
- Used for persistence

### Encoders
- Encode payloads to avoid detection
- Bypass antivirus and IDS
- Example: shikata_ga_nai encoder

---

## Metasploit Database

### What is it?
- PostgreSQL database used by Metasploit
- Stores scan results and findings
- Stores credentials found
- Stores session information
- Makes organizing large engagements easier

### Starting Database
```bash
sudo service postgresql start
sudo msfdb init
```

---

## How Metasploit Works

### Basic Attack Flow
- Step 1 → Scan target for open ports and services
- Step 2 → Identify vulnerable service and version
- Step 3 → Search for matching exploit module
- Step 4 → Configure exploit options
- Step 5 → Set payload for exploit
- Step 6 → Run exploit against target
- Step 7 → Get shell or Meterpreter session
- Step 8 → Perform post exploitation

---

## Metasploit Use Cases
- Penetration testing authorized systems
- Vulnerability assessment
- Security research
- CTF competitions
- Learning ethical hacking
- Testing patch effectiveness
- Security awareness training

---

## Important Points
- Always use Metasploit only on authorized systems
- Unauthorized use is illegal in most countries
- Metasploit is a tool for defense and offense both
- Understanding Metasploit helps defenders too
- Keep Metasploit updated for latest exploits
- Practice on vulnerable VMs like Metasploitable
```

---
