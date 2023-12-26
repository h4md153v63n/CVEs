# 2022 CVEs & Vulnerabilities:

## 🎯 Simple Task Managing System V1.0
The Simple Task Managing System in PHP With MySQLi is a simple web system coded in a PHP programming language. This project contains an advance coding script that display fully operational function of the system. The system contain many functionalities that use its purpose. This Simple Task Managing System is a project that can help students taking IT related courses. This is a simple system that tends to help beginners to start their php programming career . This Simple Task Managing System in PHP With MySQLi provide a learning references to help beginners learn to use PHP programming.

### CVE-2022-40032 ✨
+ **Description:** SQL Injection vulnerability via `login.php` with 'login' and 'password' parameters.
+ **Affected Version:** 1.0
+ **Affected File:** `/TaskManagingSystem/login.php`
+ **Vulnerable Parameter:** 'login' and 'password'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVE-2022-40032_Simple-Task-Managing-System-V1.0-SQL-Injection-Vulnerability-Unauthenticated

## 🎯 Intern Record System V1.0
The Intern Record System In PHP is a simple mini project for managing the records of interns. The project contains the admin side. The admin can view all the users and employers. They can add and view the employer details, but cannot delete their accounts. This project is a simple project that makes a convenient way for any company to store details

### CVE-2022-40347 ✨
+ **Description:** SQL Injection vulnerability via `controller.php` with 'phone', 'email', 'deptType' and 'name' parameters.
+ **Affected Version:** 1.0
+ **Affected File:** `/intern/controller.php`
+ **Vulnerable Parameter:** 'phone', 'email', 'deptType' and 'name'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVE-2022-40347_Intern-Record-System-phone-V1.0-SQL-Injection-Vulnerability-Unauthenticated

### CVE-2022-40348 ✨
+ **Description:** Stored Cross-Site Scripting (XSS) vulnerability via `controller.php` with 'name' and 'email' parameters.
+ **Affected Version:** 1.0
+ **Affected File:** `/intern/controller.php`
+ **Vulnerable Parameter:** 'name' and 'email'
+ **Impact:** Attackers can inject and execute malicious scripts.
+ **Solution:** Implement proper input validation, sanitize user-supplied data and output encoding.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVE-2022-40348_Intern-Record-System-Cross-site-Scripting-V1.0-Vulnerability-Unauthenticated

