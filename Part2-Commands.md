# Linux Basics - Part 2: Permissions & Search

## 1. File Permissions
`chmod 755 script.sh`  - Give execute permission  
`chmod 644 file.txt`   - Read/write for owner, read for others  
`chown user:group file` - Change owner and group  
`ls -l`                - Check permissions

## 2. Searching
`grep "password" file.txt`     - Search for text inside files  
`find / -name "passwd" 2>/dev/null` - Find files by name  
`locate config.php`            - Fast file search if db exists

## 3. Why it matters for Privesc
Wrong permissions let you read/edit files you shouldn't.  
SUID files found with `find` are the most common way to escalate to root.
