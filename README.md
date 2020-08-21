### House Rental v1.0 - SQL Injection Unauthenticated Code Execution - Change Admin Password
### Exploit Author: Bobby Cooke (boku) & Adeeb Shah (@hyd3sec) 
+ House Rental v1.0 suffers from an unauthenticated SQL Injection vulnerability allowing remote attackers to execute arbitrary code on the hosting webserver via sending a malicious POST request.  
  
<p align="center">
  <img width="1000" height="700" src="/homeRentSQLi.gif">
</p>
  
  - CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')
  - OWASP Top Ten 2017: A1:2017-Injection
  - CVSS Base Score: 10.0 
  - Impact Subscore: 6.0 
  - Exploitability Subscore: 3.9
  - CVSS Vector: AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H
### Vulnerable Source Code:
```php
 /config/config.php
   11  try {
   12     $connect = new PDO("mysql:host=".dbhost."; dbname=".dbname, dbuser, dbpass);
   13     $connect->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
 /index.php
    5   if(isset($_POST['search'])) {
    7     $keywords = $_POST['keywords'];
   11     $keyword = explode(',', $keywords);
   12     $concats = "(";
   13     $numItems = count($keyword);
   15     foreach ($keyword as $key => $value) {
   17       if(++$i === $numItems){
   18          $concats .= "'".$value."'";
   19       }else{
   20         $concats .= "'".$value."',";
   23     $concats .= ")";
   47         $stmt = $connect->prepare("SELECT * FROM room_rental_registrations_apartment WHERE country IN $concats OR country IN $loc OR state IN $concats OR state IN $loc OR city IN $concats OR city IN $loc OR address IN $concats OR address IN $loc OR rooms IN $concats OR landmark IN $concats OR landmark IN $loc OR rent IN $concats OR deposit IN $concats");
   48         $stmt->execute();
```
#### Vendor Homepage: https://projectworlds.in
#### Software Link: https://projectworlds.in/wp-content/uploads/2019/06/home-rental.zip

