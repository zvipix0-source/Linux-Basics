# Linux Basics - Part 1: Navigation & files

## 1. Navigation Commands
'pwd'       - Show current directory
'ls -la'    - List all files with details
'cd /etc'   - Change to /etc directory
'cd ..'     - Go back one directory

## 2. File Operations
'cat file.txt'   - Read file content
'nano file.txt'  - Edit file in terminal
'touch new.txt'  - Create empty file
'rm file.txt'    - Delete file

## 3. Why it matters for Privesc
**Privesc = Privilege Escalation**  
It means moving from a low-privilege user to a high-privilege user like `root` on Linux.

**Why we do it:**  
In labs and real systems, the goal is to gain full control. You often start with a limited account, so you need to find a misconfiguration to become `root` and read protected files.

**How we use these commands:**  
The commands in Part 1 help us explore the system and find those misconfigurations.  
Example: `find / -perm -4000 2>/dev/null` finds SUID files, which are commonly used for privilege escalation.
