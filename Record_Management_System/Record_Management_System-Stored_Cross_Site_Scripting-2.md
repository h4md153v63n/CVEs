# Record_Management_System-Stored_Cross_Site_Scripting-2
+ **Exploit Title:** Record_Management_System-Stored_Cross_Site_Scripting-2
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/record-management-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/RECORD_MANAGEMENT_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-

## References: 

## Description:
Record Management System 1.0 allows Stored Cross-Site Scripting via parameter 'docname' in "/recordmanagement/main/doctype.php". Record Management System is vulnerable to a cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data.
An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Go to the login panel: "http://localhost/recordmanagement/"
+ Login with `admin`:`admin`
+ Go to the Document Type: "http://localhost/recordmanagement/main/doctype.php"
+ Add Doc Type and Name with payload `<img src=1 onerror=alert(document.cookie)>`
+ Save and then XSS will be triggered permanently.
+ Refresh and alert will continue to pop-up.

![2-1](https://github.com/h4md153v63n/CVEs/assets/5091265/584f0f11-b43d-4143-9656-1ffb32e1aebc)

![2-2](https://github.com/h4md153v63n/CVEs/assets/5091265/e1c93d56-9891-4199-ab01-735060851847)

![2-3](https://github.com/h4md153v63n/CVEs/assets/5091265/7955ccb6-3eaf-4adf-8456-099bfec252b3)
