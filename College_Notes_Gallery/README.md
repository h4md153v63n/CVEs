# College Notes Gallery 2.0
College notes gallery project is developed using PHP, JavaScript, Bootstrap, and CSS. Talking about the project, it contains just a user side. All the management are done from the user side like uploading the reading materials. From the user side, the users can view the homepage and see the contents available there. Through this site,  the college can maintain the student’s notes with more ease. He/She can upload them and also can edit them.

## Vulnerabilities:

### 🎯 CVE-2023-7130
+ **Description:** SQL Injection vulnerability via `login.php` with 'user' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/notes/login.php`
+ **Vulnerable Parameter:** 'user'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/College_Notes_Gallery/College_Notes_Gallery-SQL_Injection.md
