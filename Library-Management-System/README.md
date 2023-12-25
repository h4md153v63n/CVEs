# Library Management System V1.0
Library Management System project is developed using PHP, JavaScript, Bootstrap, and CSS. Talking about the project, it has lots of features. A user can post burrow/return books. It contains a homepage from where users can check their transactions as well as other totals too. From user’s login, he/she should provide Student ID in order to Log in to the system. The student id can be retrieved from Admin Panel. The viewer is only allowed to check book’s availability through Homepage and also admin panel can be accessed from the Menu bar.

## Vulnerabilities:

### CVE-2023-7109
+ **Description:** SQL Injection vulnerability via `/admin/login.php` with 'username' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/libsystem/admin/login.php`
+ **Vulnerable Parameter:** 'username'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Library-Management-System/Library-Management-System_SQL_Injection-1.md

### CVE-2023-7110
+ **Description:** SQL Injection vulnerability via `login.php` with 'student' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/libsystem/login.php`
+ **Vulnerable Parameter:** 'student'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Library-Management-System/Library-Management-System_SQL_Injection-2.md

### CVE-2023-7111
+ **Description:** SQL Injection vulnerability via `index.php?category=1` with 'category' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/libsystem/index.php?category=1`
+ **Vulnerable Parameter:** 'category'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Library-Management-System/Library-Management-System_SQL_Injection-3.md
