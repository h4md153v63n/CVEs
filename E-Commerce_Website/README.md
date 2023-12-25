# E-Commerce Website
E-Commerce Website project is developed using PHP, CSS, Bootstrap, and JavaScript. Talking about the project, it has all the essential features required for an e-commerce website. This project contains the user and admin side. Admin can manage products, suppliers, view logs and many more. From user account, he/she can view products and purchase it easily. The Admin plays the main role in the management of the website. In this project, admin performs all the main functions like managing products, suppliers, users and much more.

## Vulnerabilities

### CVE-2023-7105
+ **Description:** SQL Injection vulnerability via `index_search.php` with 'search' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/Electricks/Electricks-shop/index_search.php`
+ **Vulnerable Parameter:** 'search'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.

### CVE-2023-7106
+ **Description:** SQL Injection vulnerability via `/product_details.php?prod_id=11` with 'prod_id' parameter.
+ **Affected Version:** 1.0
+ **Affected File:** `/Electricks/Electricks-shop/pages/product_details.php?prod_id=11`
+ **Vulnerable Parameter:** 'prod_id'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.

### CVE-2023-7107
+ **Description:** SQL Injection vulnerability via `user_signup.php` with 'firstname', 'middlename', 'email', 'address', 'contact' and 'username' parameters.
+ **Affected Version:** 1.0
+ **Affected File:** `/Electricks/Electricks-shop/pages/user_signup.php`
+ **Vulnerable Parameter:** 'firstname', 'middlename', 'email', 'address', 'contact' and 'username'
+ **Impact:** Attackers can manipulate SQL queries, potentially gaining unauthorized access or manipulating data.
+ **Solution:** Implement parameterized queries and proper input validation for the affected parameters.

### CVE-2023-7108
- **Description:** Stored Cross-Site Scripting (XSS) vulnerability via `user_signup.php` with 'firstname' parameter.
- **Affected Version:** 1.0
- **Affected File:** `Electricks/Electricks-shop/pages/user_signup.php`
- **Vulnerable Parameter:** 'firstname'
- **Impact:** Attackers can inject and execute malicious scripts.
- **Solution:** Implement proper input validation and output encoding.
