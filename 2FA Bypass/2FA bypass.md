# 2FA Bypass

## Response Manipulation
+ Response is
  ``` 
  HTTP/1.1 404 Not Found
  ...
  {"code": false}
  ```
  Change to 
  ```
  HTTP/1.1 404 Not Found
  ...
  {"code": true}
  ```
+ Change the response 
    - ``false`` to ``true``
    - ``0`` to ``1``
    - ``Invalid`` to ``valid``

## Code Manipulation
+ Response is
  ```
  HTTP/1.1 4XX Not Found
  ...
  {"code": false}
  ```
  Change to
  ```
  HTTP/1.1 200 OK
  ...
  {"code": true}
  ```
  
## Code Reusability
1. Request for 2fa code and use it,
2. Then, try to reuse the same code after sometime
      - If it succeeds **(Vuln)**

+ Try requesting multiple 2fa codes and see if previously requested code expire or not
  - If old code doesn't expire **(Vuln)** 

## Null Payloads
+ Use 0000
  ```
  POST /2fa/
  Host: target.com
  ...
  code=0000
  ```
+ Use null
  ```
  POST /2fa/
  Host: target.com
  ...
  code=null
  ```
  
## Js file Analysis
+ **Rare** JS Files may contain info about the 2FA Code

## No Rate-Limit
+ Bruteforce 2fa code, if there is no rate limit
1. Capture 2fa request and send it to intruder
2. Add payload mark in code place
    - If not 429 in response code **(Vuln)**
  
## CSRF on 2fa
1. go to 2fa page and click on disable
2. capture the request & generate csrf poc
3. open in other browser. if success/2fa removed (vuln)

## referer check bypass
1. go to page after 2fa 
2. add referer header to 2fa page url in request
``Referer: https://target.com/2fa/``

## Forcefull browsing
+ try to access profile directly
+ if url ``target/2fa/profile`` change to ``target/profile``

## Password reset
+ request password reset --> change password --> login without 2fa 

## EMail / Password change
+ Change email or passwd --> log out --> login without 2fa

## code leakage in response
1. request for 2fa code
2. then, check all response for code if any leaked 

## missing 2fa integriti validation
1. request 2fa code from 1st account
2. then, use the code in 2nd account