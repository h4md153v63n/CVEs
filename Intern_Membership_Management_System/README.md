# Intern Membership Management System 2.0
Intern Membership Mangement System project is a simple using PHP, CSS, Bootstrap, and JavaScript. Talking about the project, it has all the essential features of the Intern company. This project contains both the admin and the student side where the admin can manage the job titles and post. The Admin plays the main role in the management of the system. In this project, all the main functions are performed from the Admin side.

## Vulnerabilities:

### 🎯 CVE-2023-7131
+ **Description:** SQL Injection vulnerability via `/user_registration/` with 'userName', 'firstName', 'lastName', and 'gender' parameters.
+ **Affected Version:** 1.0
+ **Affected File:** `/intern/user_registration/`
+ **Vulnerable Parameter:** 'userName', 'firstName', 'lastName', and 'gender'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Intern_Membership_Management_System/Intern_Membership_Management_System-SQL-Injection.md

### 🎯 CVE-2023-7132
+ **Description:** Stored Cross-Site Scripting (XSS) vulnerability via `/user_registration/` with 'userName', 'firstName', 'lastName', and 'userEmail' parameters.
+ **Affected Version:** 1.0
+ **Affected File:** `/intern/user_registration/`
+ **Vulnerable Parameter:** 'userName', 'firstName', 'lastName', and 'userEmail'
+ **Impact:** Attackers can inject and execute malicious scripts.
+ **Solution:** Implement proper input validation, sanitize user-supplied data and output encoding.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Intern_Membership_Management_System/Intern_Membership_Management_System-Stored_Cross_site_Scripting.md
