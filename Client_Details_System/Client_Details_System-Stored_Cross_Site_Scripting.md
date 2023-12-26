# Client_Details_System-Stored_Cross_Site_Scripting
+ **Exploit Title:** Client_Details_System-Stored_Cross_Site_Scripting
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/client-details-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/CLIENT_DETAILS_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE: **CVE-

## References: 

## Description:
Client_Details_System 1.0 allows Stored Cross-Site Scripting via parameters 'fname', 'lname', 'email' and 'contact' in "/clientdetails/admin/regester.php". Client_Details_System is vulnerable to a cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data.
An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Go to the Admin Panel: "http://localhost/clientdetails/admin/"
+ Login with `admin`:`client123`
+ Go to Create Users: "http://localhost/clientdetails/admin/regester.php"
+ Fill the form parameters 'fname', 'lname', 'email' and 'contact' with the payload `"><ScRiPt>confirm(document.cookie)</ScRiPt>h0la`
+ Save and then XSS will be triggered permanently.
+ Refresh and alert will continue to pop-up.

![8](https://github.com/h4md153v63n/CVEs/assets/5091265/2f2c7ec3-ed0c-4d83-810e-4dcb3fa66ebc)

![8-2](https://github.com/h4md153v63n/CVEs/assets/5091265/f0dce129-7d86-40ce-9f02-9f8fb47cb40e)

