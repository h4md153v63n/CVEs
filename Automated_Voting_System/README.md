# Automated Voting System V1.0
Automated Voting System project is developed using PHP, JavaScript, Bootstrap, and CSS. Talking about the project, it has lots of features. This project contains a Voter’s login side where a voter can Sign in for voting and Admin Panel where he/she can view candidates list, Voter’s list, Canvassing report, system users and many more. From the voter’s login, he/she should provide Voters ID in order to log in to the system to vote. The voter’s id can be retrieved from the Admin Panel.

## Vulnerabilities:

### 🎯 CVE-2023-7126
+ **Description:** SQL Injection vulnerability via `/admin/` with 'username' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/automated%20voting/admin/`
+ **Vulnerable Parameter:** 'username'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Automated_Voting_System/Automated_Voting_System-SQL_Injection-1.md

### 🎯 CVE-2023-7127
+ **Description:** SQL Injection vulnerability via `/automated%20voting/` with 'idno' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/automated%20voting/`
+ **Vulnerable Parameter:** 'idno'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Automated_Voting_System/Automated_Voting_System-SQL_Injection-2.md
