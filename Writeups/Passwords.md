
# Linux Privilege Escalation - Passwords & Keys

## 1. Passwords in History
Users sometimes type passwords directly in commands.

cat ~/.bash_history
cat ~/.zsh_history
*Bad practice:* `mysql -u root -pMyPassword123`  
*Fix:* Use `-p` alone and let it prompt you.

## 2. Passwords in Config Files
Common places to check:
grep -r "password" /var/www/ /opt/ 2>/dev/null
find / -name "*.env" -o -name "config.php" -o -name "*.ovpn" 2>/dev/null
Example: `cat /etc/openvpn/auth.txt`

## 3. SSH Private Keys
Look for readable private keys.
find / -name "id_rsa" -o -name "*_key" -perm /o=r 2>/dev/null
chmod 600 root_key
ssh -i root_key root@IP
*Rule:* Any secret stored as plaintext in a readable file is a vulnerability.

## Quick Enumeration Checklist
grep -r "password" ~/.*history /var/www/ /opt/ 2>/dev/null
find / -name "*.env" -o -name "*.ovpn" -o -name "config.php" 2>/dev/null  
find / -name "id_rsa" -o -name "*_key" -perm /o=r 2>/dev/null
env | grep -i pass

4. Commit message:
Add Passwords and Keys writeup

---

### **Step 5: Update README.md**

1. Open `README.md` > click pencil icon to edit
2. Add this under your existing Contents:

```markdown
## Writeups - THM Linux Privesc
- [Sudo Exploits](Writeups/Sudo.md)
- [Crontab Exploits](Writeups/Crontab.md)
- [SUID Exploits](Writeups/SUID.md)
- [Passwords & Keys](Writeups/Passwords.md)
3. Commit message:
Update README with privesc writeups
---

خلصت كل شيء. الحين عندك 4 ملفات مرتبة تقدر تفتحها في 3 ثواني وقت الاختبار.

تبغى أضيف لك جدول محتويات داخلي لكل ملف عشان التنقل أسهل؟
