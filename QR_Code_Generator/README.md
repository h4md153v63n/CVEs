# QR Code Generator V1.0
QR Code Generator is developed using PHP QR CODE Library with CSS, Bootstrap, and JavaScript. Talking about the project, a user can generate QR codes easily just by providing his/her email address, subject, and message. After generating QR code, the user can download it too. This QR code generator focuses on sharing email address details. For the designing part, it uses Embedded CSS and Bootstrap 3.3.7. After generating QR code, all the images are stored inside the “temp” folder for backups.

## Vulnerabilities:

### 🎯 CVE-2023-7149
+ **Description:** Reflected Cross-Site Scripting (XSS) vulnerability via `download.php?file=author.png` with 'file' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/qr-codegen/download.php?file=author.png`
+ **Vulnerable Parameter:** 'file'
+ **Impact:** Attackers can inject and execute malicious scripts.
+ **Solution:** Implement proper input validation, sanitize user-supplied data and output encoding.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/QR_Code_Generator/QR_Code_Generator-Reflected_Cross_Site_Scripting.md
