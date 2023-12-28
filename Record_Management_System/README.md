# Record Management System V1.0
Record Managment System is developed using PHP, CSS, and JavaScript. Talking about the project, it contains the least but essential features. This project contains an admin side where Admin can manage the transaction, offices, and document type. The Admin plays an important role in the management of the system. In this project, the user has to perform all the main functions from the Admin side.

## Vulnerabilities:

### 🎯 CVE-2023-7135
+ **Description:** Blind Cross-Site Scripting (XSS) vulnerability via `offices.php` with 'officename' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/recordmanagement/main/offices.php`
+ **Vulnerable Parameter:** 'officename'
+ **Impact:** Attackers can inject and execute malicious scripts.
+ **Solution:** Implement proper input validation, sanitize user-supplied data and output encoding.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Record_Management_System/Record_Management_System-Blind_Cross_Site_Scripting-1.md

### 🎯 CVE-2023-7136
+ **Description:** Blind Cross-Site Scripting (XSS) vulnerability via `doctype.php` with 'docname' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/recordmanagement/main/doctype.php`
+ **Vulnerable Parameter:** 'docname'
+ **Impact:** Attackers can inject and execute malicious scripts.
+ **Solution:** Implement proper input validation, sanitize user-supplied data and output encoding.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Record_Management_System/Record_Management_System-Blind_Cross_Site_Scripting-2.md
