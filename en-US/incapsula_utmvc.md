Here's the translation:

[`Back to Home`](en.md)    [`Previous`](incapsula.md)    [`Next`](incapsula_rbzid.md)    [`中文文档`](../zh-CN/incapsula_utmvc.md)

## Incapsula ( __utmvc )

### Frequently Asked Questions

* Interface (utmvc needs consistent proxy, contact the administrator if there any issues)
    * 1. Provide href and proxy, the service will compute utmvc after request 
* How to find the utmvc script (see the picture below, URL containing the keyword SWJIYLWA)
    * ![incapsula](/images/incapsula/incapsula3.png)
* utmvc script response sample
    * ![incapsula](/images/incapsula/incapsula4.png)

### Request URL (POST):

| Version               | Interface URL                                            |
|-----------------------|----------------------------------------------------------|
| `utmvc`               | `http://api.nocaptcha.io/api/wanda/incapsula/utmvc`     |

### Request Headers:

| Parameter Name       | Description                                                                                       | Required |
|----------------------|---------------------------------------------------------------------------------------------------|----------|
| `User-Token`         | `User secret key, obtained from the main page`                                                    | `Yes`    |
| `Content-Type`       | `application/json`                                                                               | `Yes`    |
| `Developer-Id`       | `Developer ID, used by the developer account, the string from the main page invite link (e.g. xxx/register?c=abcdef, then abcdef is the Developer ID)`  | `No`     |

### POST Data (JSON):

| Parameter Name | Type       | Description                                                                                                                                                                             | Required |
|----------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| `cookies`      | `Object`   | `Cookies returned from the homepage, upload all`                                                                                                                                        | `Yes`    |
| `href`         | `String`   | `URL that returns the utmvc script`                                                                                                                                                     | `Yes`    |
| `user_agent`   | `String`   | `utmvc process requires consistent ua, so please provide the ua you will use`                                                                                                           | `Yes`    |
| `script`       | `String`   | `the response of request href`                                                                                                                                                          | `Yes`    |

#### json example

// ... (No need to translate JSON data)

### Response Data (JSON):

| Parameter Name | Type       | Description                                                                      |
|----------------|------------|----------------------------------------------------------------------------------|
| `status`       | `Integer`  | `Whether the call was successful, 1 for success, 0 for failure, use this value for judgment`   |
| `msg`          | `String`   | `Description of the call result in Chinese`                                      |
| `id`           | `String`   | `Unique request id for this instance, can be used for subsequent record queries` |
| `data.__utmvc` | `String`   | `Computed __utmvc parameter, can be used in subsequent interfaces`               |
| `cost`         | `String`   | `Validation time (in milliseconds)`                                              |

// ... (No need to translate JSON data)

### CURL command

// ... (No need to translate CURL commands)

### Invocation example

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import IncapsulaUtmvcCracker

cracker = IncapsulaUtmvcCracker(
    user_token="xxx",
    href="https://premier.hkticketing.com/_Incapsula_Resource?SWJIYLWA=719d34d31c8e3a6e6fffd425f7e032f3",
    script="the response of request href",
    cookies={ 'incap_ses_406_2314793': 'w399Tycs8xhdpuG+aWeiBWGkYWQAAAAAKCTf+jt4Sq4R0xN0pU9VXA==', 'visid_incap_2314793': 'DVtB0J4PRoG+jHdSiyyjNWKkYWQAAAAAQUIPAAAAAABY5A3D8V2Yp2rCf0Qol0Kd' },
    proxy="usr:pwd@ip:port",
    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
)
ret = cracker.crack()
print(ret)
```
