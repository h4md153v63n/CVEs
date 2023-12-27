# Record_Management_System-Stored_Cross_Site_Scripting-1
+ **Exploit Title:** Record_Management_System-Stored_Cross_Site_Scripting-1
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/record-management-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/RECORD_MANAGEMENT_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-

## References: 

## Description:
Record Management System 1.0 allows Stored Cross-Site Scripting via parameter 'officename' in "/recordmanagement/main/offices.php". Record Management System is vulnerable to a cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data. An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Go to the login panel: "http://localhost/recordmanagement/"
+ Login with `admin`:`admin`
+ Go to the Offices: "http://localhost/recordmanagement/main/offices.php"
+ Add Office and Name with payload `</pre></pre><script>prompt(document.cookie)</script>`
+ Save and then XSS will be triggered permanently.
+ Refresh and alert will continue to pop-up.

![1-1](https://github.com/h4md153v63n/CVEs/assets/5091265/c725742a-5296-4bf7-af0c-34927ff562d0)
<br>
<br>
![1-2](https://github.com/h4md153v63n/CVEs/assets/5091265/07dc543f-aa3d-478c-9e73-4644e3c28e9f)
