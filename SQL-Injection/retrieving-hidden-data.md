# Retrieving Hidden Data using SQL Injection

## 🧩 Lab Source
This lab is from PortSwigger Web Security Academy.

## 🎯 Objective
Bypass the search filter to retrieve all items from the database.

## 🧠 Vulnerability Explanation
The application is vulnerable to SQL injection because user input is directly included in the SQL query without proper sanitization. This allows an attacker to manipulate the query logic.

## ⚙️ Exploitation Steps
1. Intercept the search request using Burp Suite
2. Modify the `category` (or search) parameter with:
   ' OR '1'='1'--
3. Send the request
4. Observe that all items are returned

## 💥 Payload (Why it works)
- `'1'='1'` is always true, which makes the WHERE condition match all rows  
- `--` is a SQL comment operator that ignores the rest of the query  

## 📌 Impact
An attacker can bypass filtering mechanisms and retrieve all data from the database, potentially exposing sensitive information.

## 🛡️ Mitigation
- Use parameterized queries (prepared statements)
- Implement proper input validation
- Avoid directly concatenating user input into SQL queries

## 📘 Key Takeaway
Even simple input fields like search filters can be exploited if user input is not handled securely.
