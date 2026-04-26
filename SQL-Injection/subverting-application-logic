# 🔐 Subverting Application Logic (Login Bypass) using SQL Injection

## 🧩 Lab Source
This lab is from PortSwigger Web Security Academy.

## 🎯 Objective
Bypass the login functionality using a SQL Injection vulnerability to gain unauthorized access.

## 🧠 Vulnerability Explanation
The application constructs a SQL query like this:

 SELECT * FROM users WHERE username = 'input' AND password = 'input'

The problem is that user input is directly embedded into the query without sanitization.
This allows an attacker to manipulate the query logic

⚔️ Attack Strategy
Instead of providing valid credentials, we inject a payload that alters the WHERE condition to always return true.
Payload used:
administrator'--

## ⚙️ Exploitation Steps
1.Navigate to the login page
2.Enter the following:
  Username: administrator'--
  Password: anything (e.g., task,pass,abc)
3.Submit the request
4.Login is successful as a administrator without valid credentials

## 💥 Payload (Why it works)
-The query becomes:
 SELECT * FROM users WHERE username = 'administrator'--' AND password = 'anything'

-Key points:
 ' → closes the username string
 -- → comments out the rest of the query
 Password check is completely ignored

-So the query effectively becomes:

 SELECT * FROM users WHERE username = 'administrator'

➡️ This logs us in without knowing the password

## 📌 Impact
An attacker can bypass filtering mechanisms and retrieve all data from the database, potentially exposing sensitive information.

## 🛡️ Mitigation
To prevent this vulnerability:
-Use parameterized queries (prepared statements)
-Implement proper input validation & sanitization
-Avoid dynamic SQL query construction
-Use ORM frameworks where possible

## 📘 Key Takeaway
Even simple input fields like search filters can be exploited if user input is not handled securely.
