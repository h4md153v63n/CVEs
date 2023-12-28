# Voting System V1.0
Voting System project is developed using PHP, JavaScript, Bootstrap, and CSS. Talking about the project, it has lots of essential features. This project contains a Voter’s login side where a voter can Sign in to vote and Admin Panel where he/she can view total votes, add and list voters, positions, candidates and many more. While logging in from voter’s login, the user should provide Voters ID in order to log in to the system to vote. The voter’s id can be retrieved from the Admin Panel.

## Vulnerabilities:

### 🎯 CVE-2023-7128
+ **Description:** SQL Injection vulnerability via `/admin/` with 'username' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/votesystem/admin/`
+ **Vulnerable Parameter:** 'username'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Voting_System/Voting_System-SQL_Injection-1.md

### 🎯 CVE-2023-7129
+ **Description:** SQL Injection vulnerability via `/votesystem/` with 'voter' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/votesystem/`
+ **Vulnerable Parameter:** 'voter'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/Voting_System/Voting_System-SQL_Injection-2.md
