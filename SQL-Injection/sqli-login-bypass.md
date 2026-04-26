# 🔐 Subverting Application Logic (Login Bypass) using SQL Injection

## ⚠️ Disclaimer
This writeup is for educational purposes only and is based on labs from PortSwigger Web Security Academy.  
Do not attempt these techniques on real-world applications without proper authorization.  
The author is not responsible for any misuse of this information.

---

## 🧩 Lab Source  
This lab is from PortSwigger Web Security Academy.

---

## 🎯 Objective  
Bypass the login functionality using a SQL Injection vulnerability to gain unauthorized access.

---

## 🧠 Vulnerability Explanation  
The application constructs a SQL query like this:

```sql
SELECT * FROM users WHERE username = 'input' AND password = 'input'
```

The problem is that user input is directly embedded into the query without sanitization.  
This allows an attacker to manipulate the query logic.

---

## ⚔️ Attack Strategy  
Instead of providing valid credentials, we inject a payload that alters the `WHERE` condition to always return true.

**Payload used:**
```sql
administrator'--
```

---

## ⚙️ Exploitation Steps  

1. Navigate to the login page  
2. Enter the following:  
   - **Username:** `administrator'--`  
   - **Password:** anything (e.g., `test`, `pass`, `abc`)  
3. Submit the request  
4. Login is successful as the administrator without valid credentials  

---

## 💥 Payload (Why it works)  

The query becomes:

```sql
SELECT * FROM users WHERE username = 'administrator'--' AND password = 'anything'
```

### Key points:
- `'` → closes the username string  
- `--` → comments out the rest of the query  
- Password check is completely ignored  

So the query effectively becomes:

```sql
SELECT * FROM users WHERE username = 'administrator'
```

➡️ This logs us in without knowing the password.

---

## 📌 Impact  
An attacker can bypass authentication and gain unauthorized access to user accounts, including administrative accounts.

---

## 🛡️ Mitigation  

To prevent this vulnerability:
- Use parameterized queries (prepared statements)  
- Implement proper input validation & sanitization  
- Avoid dynamic SQL query construction  
- Use ORM frameworks where possible  

---

## 📘 Key Takeaway  
Improper handling of user input in authentication logic can lead to complete access bypass.
