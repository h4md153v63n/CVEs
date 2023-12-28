# Client Details System 1.0
Client Details System is developed using PHP, CSS, Bootstrap, and JavaScript. Talking about the project, it contains almost all the essential features. This project contains user and admin side where a user can view all client details, enter customer details and admin can manage users, register new users, CRUD client details. The Admin plays an important role in the management of this simple system. A user can also register as a new user if he/she does not have an account.

## Vulnerabilities:

### 🎯 CVE-2023-7137
+ **Description:** SQL Injection vulnerability via `/clientdetails/` with 'uemail' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/clientdetails/`
+ **Vulnerable Parameter:** 'uemail'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Client_Details_System/Client_Details_System-SQL_Injection_1.md

### 🎯 CVE-2023-7138
+ **Description:** SQL Injection vulnerability via `/admin` with 'username' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/clientdetails/admin`
+ **Vulnerable Parameter:** 'username'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Client_Details_System/Client_Details_System-SQL_Injection_2.md

### 🎯 CVE-2023-7139
+ **Description:** SQL Injection vulnerability via `regester.php` with 'fname', 'lname', 'email' and 'contact' parameters.
+ **Affected Version:** 1.0
+ **Affected File:** `/clientdetails/admin/regester.php`
+ **Vulnerable Parameter:** 'fname', 'lname', 'email' and 'contact'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Client_Details_System/Client_Details_System-SQL_Injection_3.md

### 🎯 CVE-2023-7140
+ **Description:** SQL Injection vulnerability via `manage-users.php?id=1` with 'id' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/clientdetails/admin/manage-users.php?id=1`
+ **Vulnerable Parameter:** 'id'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Client_Details_System/Client_Details_System-SQL_Injection_4.md

### 🎯 CVE-2023-7141
+ **Description:** SQL Injection vulnerability via `update-clients.php?uid=3` with 'uid' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/clientdetails/admin/update-clients.php?uid=3`
+ **Vulnerable Parameter:** 'uid'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Client_Details_System/Client_Details_System-SQL_Injection_5.md

### 🎯 CVE-2023-7142
+ **Description:** SQL Injection vulnerability via `clientview.php?ID=2` with 'ID' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/clientdetails/admin/clientview.php?ID=2`
+ **Vulnerable Parameter:** 'ID'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Client_Details_System/Client_Details_System-SQL_Injection_6.md

### 🎯 CVE-2023-7143
+ **Description:** Blind Cross-Site Scripting (XSS) vulnerability via `regester.php` with 'fname', 'lname', 'email' and 'contact' parameters.
+ **Affected Version:** 1.0
+ **Affected File:** `/clientdetails/admin/regester.php`
+ **Vulnerable Parameter:** 'fname', 'lname', 'email' and 'contact'
+ **Impact:** Attackers can inject and execute malicious scripts.
+ **Solution:** Implement proper input validation, sanitize user-supplied data and output encoding.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Client_Details_System/Client_Details_System-Blind_Cross_Site_Scripting.md
