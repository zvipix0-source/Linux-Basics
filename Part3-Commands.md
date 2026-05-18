# Linux Basics - Part 3: Text Processing & Processes

## 1. Text Processing
`cat file.txt`         - Print file content  
`head -n 5 file.txt`   - Show first 5 lines  
`tail -n 5 file.txt`   - Show last 5 lines  
`cut -d: -f1 /etc/passwd` - Extract first field from colon-separated file  

## 2. Processes & System Info
`ps aux`               - List all running processes  
`top`                  - Live process viewer  
`uname -a`             - Show kernel and OS info  
`id`                   - Show current user and groups  

## 3. Why it matters for Privesc
- `ps aux` shows if a service is running as root and if you can hijack it.  
- `uname -a` tells you the kernel version to check for kernel exploits.  
- `cut` and `head/tail` help you quickly extract usernames, paths, and keys from files.
