# E-commerce Site V1.0
E-commerce site project is developed using PHP, CSS, Bootstrap, and JavaScript. Talking about the project, it has all the required essential features. This project has a user side where he/she can view product category and add products to cart and proceed for checkout whereas from administration side he/she can view sales, number of product, users, daily sales report, add product and categories. The user can also leave comments on each product if he/she wants. In this project, all the main functions are performed from the Admin side.

## Vulnerabilities:

### 🎯 CVE-2023-7124
+ **Description:** Reflected Cross-Site Scripting (XSS) vulnerability via `search.php` with 'keyword' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/ecommerce/search.php`
+ **Vulnerable Parameter:** 'keyword'
+ **Impact:** Attackers can inject and execute malicious scripts.
+ **Solution:** Implement proper input validation, sanitize user-supplied data and output encoding.
+ **Proof of Concept (PoC):** https://github.com/h4md153v63n/CVEs/blob/main/E-commerce_Site/E-commerce_Site-Reflected_Cross_Site_Scripting.md
